# Transportation Protocol on the Ethereum Blockchain

Follow these steps to get a dapp on Ethereum up and running.  Eventually this will integrate with The Transportation Protocol.  
The application presents you with a simple web interface that takes in the information related to the item you want transported.  The data is written directly to the blockchain we have deployed on the Ropsten network.

While following these steps will get you and up and running dapps.  There are still a few things missing.  For starters, we cannot confirm what has been added nor is it listed.  Another thing is that strange security warning at the top of the repo.  Do not feel constrained just to improve the existing code base.  Be adventurous and innovative and create a decentralized application that solves a problem in the real world.

### First we need to install our dependencies

[Install Ganache](https://truffleframework.com/ganache).  Your test blockchain that can be run on several networks and is currently configured with this project to give you access to wallet address and test Ether.

[Install Truffle](https://truffleframework.com/docs/truffle/getting-started/installation).  Development framework for Ethereum that will assist with the coding, comilation, migration, and deployment of your smart contracts.

[Install MetaMask](https://metamask.io/). Browser extension where we can interact with our blockchain through Chrome.

[Great Dapp University Tutorial from Start to Finish](http://www.dappuniversity.com/articles/blockchain-app-tutorial)

### Write our smart contract

Before we get started modifying our smart contracts in the `contracts/` folder we need to provide a test environment where we will have access to the data we need to get the project started.  Opening Ganache is all you need to do.  Ganache is a local blockchain which will act as your test environment for execution and testing.

<img width="1148" alt="Screen Shot 2019-04-05 at 5 37 30 PM" src="https://user-images.githubusercontent.com/7444521/55662583-8d2b9f00-57c9-11e9-8c53-98a803153429.png">

Now that we have our testing environment set up let's look at the smart contract that we have written.  [Take a look at `Transportation.sol` written in Solidity](https://github.com/amohnacs15/EthereumProtocol/blob/master/contracts/Transportation.sol).  All we are doing is create a data object that represents what is being transport and it is written to the blockchain using Solidity's `mapping` data structure.

We need to compile our code and deploy it to the Ethereum blockchain.  This is done with the following commands.

````
truffle compile
truffle migrate
````

**You've successfully deployed your contract to the blockchain**.  

The code you have just written has just been compiled down to an Application Binary Interface (ABI) and codified onto the blockchain the same way a bitcoin or any other tokenized asset is.  We can no longer modify with this code.  Luckily, Truffle provides a shortcut to assist with this. We can re-run the migrations like this:
- In your command line navigate to the root folder for Ethereum Protocol and run `truffle migrate --reset`

Notice that your application says "Loading...". That's because we're not logged in to the blockchain yet! In order to connect to the blockchain, we need to import one of the accounts from Ganache into Metamask. You can watch me set up Metamask in this video at [43:55](https://youtu.be/rzvk2kdjr2I?t=43m55s).

### Don't forget to run your tests

These can be found in the folder labeled `test` and run using the `truffle test` command in your console.

<img width="1209" alt="Screen Shot 2019-04-05 at 11 31 25 AM" src="https://user-images.githubusercontent.com/7444521/55653127-6017c600-57a2-11e9-9223-300ab3f17766.png">

### Running the client

Once we're sure everything works, now you're ready for the application to be seen in your browser!
- Enter the command `npm run dev` this will run your local node and front-end on the address and port specified in the `truffle-config.js` file.

<img width="1276" alt="Screen Shot 2019-04-05 at 12 56 49 PM" src="https://user-images.githubusercontent.com/7444521/55653128-61e18980-57a2-11e9-905b-06240be4aa59.png">

- Enter the data in the input fields
- Click Submit!
- You'll see a Metamask confirmation pop up. You must sign this transaction in order to create the task.

### Deploying to the public blockchain

Currently you are having to manage your own Ethereum node locally in order to interact with your smart contract.  For our applications to scale they need to be modular in a way they can be accessed by the public.

Infura can be used as a remote node. So take the time right now to sign up for free and create a new project.  Once that is finished install the `npm install dotenv` module so we can hide our secrets in a file titled `.env` which we will place in our route directroy.  It takes two steps:
- Store the variables `INFURA_API_KEY` which can be found when you click into your created project as **ProjectId** and `MNEMONIC` which you can get from your test blockchain.  Here we get it from Ganache
- Then we reference them we access them in our `truffle-config.js`

<img width="845" alt="Screen Shot 2019-04-05 at 5 48 50 PM" src="https://user-images.githubusercontent.com/7444521/55662822-13e17b80-57cc-11e9-9f72-07310b04709d.png">

<img width="1147" alt="Screen Shot 2019-04-07 at 8 37 20 AM" src="https://user-images.githubusercontent.com/7444521/55685940-662bb500-5910-11e9-9933-c34b6fda98aa.png">

**You're `truffle-config.js` file should look something like this**

````
require('dotenv').config();
const HDWalletProvider = require('truffle-hdwallet-provider');

module.exports = {
  networks: {
    ropsten: {
      //wrapping this in a function is important
      provider: function() {
        return new HDWalletProvider(
          process.env.MNEMONIC,
          `https://ropsten.infura.io/v3/${process.env.INFURA_API_KEY}`
          )
      },
      gasPrice: 2500000000,
      network_id: 3
    }
  },
    development: {
      host: "127.0.0.1",
      port: 7545,
      network_id: "*" // Match any network id
    },
  solc: {
    optimizer: {
      enabled: true,
      runs: 200
    }
  }
}
````

The last thing you need to do is run the command line `truffle migrate --reset --network ropsten`.  Your application is ready and transactions can be searched for on the Ropsten Blockchain using a website such as EtherScan.

This is my confirmation of deployment to the blockchain

<img width="1227" alt="Screen Shot 2019-04-05 at 9 55 31 AM" src="https://user-images.githubusercontent.com/7444521/55685876-c5d59080-590f-11e9-946d-afefc55addb0.png">




