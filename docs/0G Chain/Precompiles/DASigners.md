# DASigners

The `DASigners` contract is an interface through which solidity contracts can interact with 0G chain module DASigners. It is registered as a precompiled contract just like other precompiled EVM extensions.

## Address

`0x0000000000000000000000000000000000001000`

## Contract Params

Testnet:
```
TokensPerVote = 10
MaxVotesPerSigner = 1024
MaxQuorums = 10
EpochBlocks = 5760
EncodedSlices = 3072
```

## Terminology

### Signer 

Signer is address with enough delegations(at least `TokensPerVote` A0GI) registered in `DASigners` module. Each signer should run a DA node to verify DA blob encoding and generate BLS signature for signed blob. The BLS curve used is BN254 and the public keys of signer is registered in the contract.

Please note that for accounts with delegations to more than 10 validators, only 10 of these delegations are counted and accumulated.

### Epoch

The consecutive blocks in 0g chain is divided into groups of `EpochBlocks` and each group is an epoch.

### Quorum

In an epoch, there can be up to `MaxQuorums` quorums, each quorum is a list of signer addresses with size `EncodedSlices`. The i-th signer in the quorum is responsible for validating, signing and storing the i-th row of the encoded blob data assigned to this quorum.

### Vote

Signers can submit their signatures on a registration message to request joining the quorums in the next epoch. At the start of each epoch, the DASigners module calculates the voting power for registered signers based on their delegated token amounts. Each delegated TokensPerVote A0GI counts as one vote, and each signer can have up to MaxVotesPerSigner votes. All votes are then randomly ordered and distributed into quorums.

## Interface

Find the solidity interface in [0g-da-contract repo](https://github.com/0glabs/0g-da-contract/blob/main/contracts/interface/IDASigners.sol).

## ABI

Find the ABI in [0g-chain repo](https://github.com/0glabs/0g-chain/blob/dev/precompiles/dasigners/IDASigners.abi).

## Transactions

### registerSigner

Register signer's information, including signer address, da node service socket address, signer BLS public key on G1 and G2 group, and a signature signed by the BLS private key of following message:

`Keccak256(signerAddress, chainID, "0G_BN254_Pubkey_Registration")`

Here `chainID` is left padded to 32 bytes by zeros.
```
function registerSigner(
    SignerDetail memory _signer, 
    BN254.G1Point memory _signature
) external;
```

### updateSocket 

Update signer's socket address.

```
function updateSocket(string memory _socket) external;
```

### registerNextEpoch

Register to join the quorums in next epoch. The signer need to submit a signature signed by their BLS private key:

`Keccak256(signerAddress, epoch, chainID)`

Here `chainID` is left padded to 32 bytes by zeros and `epoch` is an unsigned 64 bit number in big endian format.

```
function registerNextEpoch(BN254.G1Point memory _signature) external;
```

## Queries

### epochNumber

Get current epoch number.

```
function epochNumber() external view returns (uint);
```

### quorumCount

Get the number of quorums of given epoch.

```
function quorumCount(uint _epoch) external view returns (uint);
```

### isSigner

Check if given address is a registered signer.

```
function isSigner(address _account) external view returns (bool);
```

### getSigner

Get the information of given signers.

```
function getSigner(address[] memory _account) external view returns (SignerDetail[] memory);
```

### getQuorum

Get the signer list of a given epoch and quorum id.

```
function getQuorum(uint _epoch, uint _quorumId) external view returns (address[] memory);
```

### getQuorumRow

Get the signer of a specific row in a given epoch and quorum id.

```
function getQuorumRow(uint _epoch, uint _quorumId, uint32 _rowIndex) external view returns (address);
```

### registeredEpoch

Check if given address is registered to join the given epoch.

```
function registeredEpoch(address _account, uint _epoch) external view returns (bool);
```

### getAggPkG1

Get the aggregated G1 public key for a given signers set. The signers set is specified by the epoch, quorum id and a bitmap. The bitmap has `EncodedSlices` bits and each bit denotes the row is chosen or not.

```
function getAggPkG1(
    uint _epoch,
    uint _quorumId,
    bytes memory _quorumBitmap
) external view returns (BN254.G1Point memory aggPkG1, uint total, uint hit);
```