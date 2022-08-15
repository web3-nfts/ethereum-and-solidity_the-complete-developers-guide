# 46. Testing with Mocha

##  Mocha Functions
|            | Mocha Functions                 |
| :--------: | :-----------------------------: |
|Function    | Purpose                         |
|it          | Run a test and make an assertion|
|describe    | Groups together 'it' functions. |
|beforeEach  | Execute some general setup code.|

##  Testing with Mocha - example 1
```
const assert = require("assert");
const ganache = require("ganache-cli");
const Web3 = require("web3");
const web3 = new Web3(ganache.provider());

class Car {
  park() {
    return "stopped";
  }
  drive() {
    return "vroom";
  }
}

let car;

beforeEach(() => {
  car = new Car();
});

describe("Car", () => {
  it("can park", () => {
    assert.equal(car.park(), "stopped");
  });
  it("can drive", () => {
    assert.equal(car.drive(), "vroom");
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
```

**Open terminal and paste these as described :**

-   Linux & Mac OS (windows git bash)-
    ```
    export NODE_OPTIONS=--openssl-legacy-provider
    ```
    
-   [46-testing.zip](https://github.com/web3-nfts/bt-web3/raw/main/Curricula/developers-guide/Resources/46-testing.zip)