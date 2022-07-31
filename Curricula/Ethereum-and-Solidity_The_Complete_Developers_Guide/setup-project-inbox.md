#   How to setup project

##  initialize Project - inbox
-   `mkdir inbox`
-   `cd inbox`
-   `npm init`
##  setup Project - inbox directory

- `mkdir contracts`
    -   `touch inbox.sol`
- `mkdir test`
    -   `touch inbox.test.js`

    ![](./imgs/37.1_Project-File-Walkthrough.png)

- **Create a inbox.sol**
    -   `inbox.sol`
    ```
    pragma solidity ^0.4.17;

    contract Inbox {
        string public message;
        
        function Inbox(string initialMessage) public {
            message = initialMessage;
        }
        
        function setMessage(string newMessage) public {
            message = newMessage;
        }    
        
    }
    ```