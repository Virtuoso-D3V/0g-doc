# 0G DA Contracts

DA Contracts mainly consists of the DASigners precompile and the DAEntrance contract.

## DA Signers Contract

See [here](<../0G Chain/Precompiles/DASigners.md>) for details.

## DA Entrance Contract

The DA Entrance contract manages the DA data upload and verification status.

### Interface

Find the solidity interface in [0g-da-contract repo](https://github.com/0glabs/0g-da-contract/blob/main/contracts/interface/IDAEntrance.sol).


### Transactions

#### submitOriginalData

Submit the encoded data and pay the DA fee.

```
function submitOriginalData(bytes32[] memory _dataRoots) external payable;
```

#### submitVerifiedCommitRoots

Submit the aggregated signatures from DA nodes, mark the data as verified.

```
function submitVerifiedCommitRoots(CommitRootSubmission[] memory _submissions) external;
```
