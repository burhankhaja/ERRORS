testMode: assertion                                                                                                                                               
corpusDir: repo                                                                                                                                             
balanceContract: 1010e18                                                                                                                                             
allContracts: true                                                                                                                                             
**sender: ["0x10000", "0x20000", "0x5B38Da6a701c568545dCfcB03FcB875f56beddC4"]**

Use that sender flag and the limitation of external testing's single msg.sender is bypassed
That is it

# Proved Using Above Config on This contract

**Target contract**

```solidity
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

contract Sender {
    bool called;
    address boss;

    constructor() {
        boss = msg.sender;
    }

    function getBoss() public view returns (address) {
        return boss;
    }

    function setCalled() public {
        require(
            msg.sender == 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4,
            "who are you"
        );
        called = true;
    }

    function getCalled() public view returns (bool) {
        return called;
    }
}
```


**Echidna Contract**

```solidity

// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

import "../src/sender.sol";

// import "forge-std/Test.sol";

contract Fuzz {
    Sender sender;
    event bowl(bool);
    event boss(address);

    constructor() payable {
        sender = new Sender();
    }

    function testBool() public {
      

        // Testing Who the Deployer is (using events, lazy right)
        emit boss(sender.getBoss());   
        emit boss(address(this));    // deployer is this contract as it deploys it

        // Testing If Sender is Simulated 
        emit bowl(sender.getCalled());
        assert(!sender.getCalled());

        // of Course sender is simulated,
        //where the set function was only callable by ..c4 address and it got triggered
    }
}

//0x5B38Da6a701c568545dCfcB03FcB875f56beddC4
// contract Unit is Test {
//     Sender sender;

//     function setUp() external {
//         sender = new Sender();
//     }

//     function testBool() public {
//         vm.prank(0x5B38Da6a701c568545dCfcB03FcB875f56beddC4);
//         sender.setCalled();
//         assert(sender.getCalled() == true);
//     }
// }

```
