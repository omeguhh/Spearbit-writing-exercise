## implementation can be called directly

**Severity**: High

Context: [`Implementation.sol#L17`](https://github.com/spearbit-audits/writing-exercise/blob/develop/contracts/Implementation.sol)

The implementation contract can be called directly instead of being restricted through a proxy. This means that a malicious actor could call `delegatecallContract` with a malicious contract that calls selfdestruct() and bricks the implementation, rendering the proxies useless causing loss of funds for the user.

The malicious contract could look like this:

```solidity
contract Hack {

    fallback() external {
        selfdestruct(payable(0x5B38Da6a701c568545dCfcB03FcB875f56beddC4));
    }


}
```
