#   How to setup project - Inbox

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

## **create a inbox.sol**
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
## **install specific Solidity Compiler 0.4.17**
-   `npm install solc@0.4.17`
   
## **create compile.js**
-   `compile.js`
    ```
    const path = require("path");
    const fs = require("fs");
    const solc = require("solc");

    const inboxPath = path.resolve(__dirname, "contracts", "Inbox.sol");
    const source = fs.readFileSync(inboxPath, "utf8");

    //  console.log(solc.compile(source, 1));
    module.exports = solc.compile(source, 1).contracts[':Inbox'];
    ```

##  in terminal run `node compile.js`

-   in terminal run `node compile.js`

In the upcoming lecture, we will be logging the compilation of our script to the terminal. If you are using **solc 0.4.17** as shown in the course, you may get these warnings:

*Invalid asm.js: Invalid member of stdlib*

or

*':6:5: Warning: Defining constructors as functions with the same name as the contract is deprecated. Use "constructor(...) { ... }" instead.\n' +*

'    function Inbox(string initialMessage) public {\n' +

'    ^ (Relevant source part starts here and spans across multiple lines).\n'

**These specific warnings can be ignored as they will not cause any issues with the compilation or deployment of the contract we are building.**

##  install mocha ganache-cli web3 (We no longer need a specific version of web3!)

```
npm install --save mocha ganache-cli web3
```

## **create inbox.test.js**
-   `inbox.test.js`
    ```
    const assert = require("assert");
    const ganache = require("ganache-cli");
    const Web3 = require("web3");
    const web3 = new Web3(ganache.provider());
    const { interface, bytecode } = require("../compile");

    let accounts;
    let inbox;

    beforeEach(async () => {
        // Get a list of all accounts
        accounts = await web3.eth.getAccounts();
        inbox = await new web3.eth.Contract(JSON.parse(interface))
            .deploy({
            data: bytecode,
            arguments: ["Hi there!"],
            })
            .send({ from: accounts[0], gas: "1000000" });
    });

    describe("Inbox", () => {
        it("deploys a contract", () => {
            // console.log(inbox);
            assert.ok(inbox.options.address); // Asserting Deployment
        });
    });
    ```
###  Testing with Mocha 

-   change the `package.json`
    ```
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
    }
    ```
    to
    ```
    "scripts": {
        "test": "mocha"
    }
    ```
-   run Mocha test 
    ```
    npm run test
    ```
###  **If the following Error happen**
    ```
    Error: error:0308010C:digital envelope routines::unsupported
        at new Hash (node:internal/crypto/hash:67:19)
        at Object.createHash (node:crypto:130:10)
        at module.exports (/Users/user/Programming Documents/WebServer/untitled/node_modules/webpack/lib/util/createHash.js:135:53)
        at NormalModule._initBuildHash (/Users/user/Programming Documents/WebServer/untitled/node_modules/webpack/lib/NormalModule.js:417:16)
        at handleParseError (/Users/user/Programming Documents/WebServer/untitled/node_modules/webpack/lib/NormalModule.js:471:10)
        at /Users/user/Programming Documents/WebServer/untitled/node_modules/webpack/lib/NormalModule.js:503:5
        at /Users/user/Programming Documents/WebServer/untitled/node_modules/webpack/lib/NormalModule.js:358:12
        at /Users/user/Programming Documents/WebServer/untitled/node_modules/loader-runner/lib/LoaderRunner.js:373:3
        at iterateNormalLoaders (/Users/user/Programming Documents/WebServer/untitled/node_modules/loader-runner/lib/LoaderRunner.js:214:10)
        at iterateNormalLoaders (/Users/user/Programming Documents/WebServer/untitled/node_modules/loader-runner/lib/LoaderRunner.js:221:10)
    /Users/user/Programming Documents/WebServer/untitled/node_modules/react-scripts/scripts/start.js:19
    throw err;
    ^
    ```

**Open terminal and paste these as described :**

-   Linux & Mac OS (windows git bash)-
    ```
    export NODE_OPTIONS=--openssl-legacy-provider
    ```

- [Error message "error:0308010C:digital envelope routines::unsupported"](https://stackoverflow.com/questions/69692842/error-message-error0308010cdigital-envelope-routinesunsupported)