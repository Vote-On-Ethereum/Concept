# Concept

The goal of this DApp is to work as a full DApp as well as a light DApp by following the user configuration.

## Full DApp

To run in full DApp mode, the user need a computer with a synced Ethereum node and a wallet with some Ether.

The DApp will get the data and sign the transaction by using the local node and wallet.
![full DApp](https://vote-on-ethereum.github.io/Concept/src/fulldApp.svg)

To try it, you can use [Mist wallet and browser](https://github.com/ethereum/mist). Go to https://vote-on-ethereum.github.io/App-Basic with a **fully synced Testnet Mist browser**. Click on the **Connect** button on the top right of the window and select your account and click **Authorize**. Now enter a name in the **Vote as** textfield and click on a **Vote for** button. Mist will prompt a window asking to execute a contract. Enter your account password and **Send transaction**. The DApp should now send the transaction to the blockchain for about 1 minute. When done, your vote should appear in the voters list (check with the hash) and add +1 to your favorite person!

## Light DApp

The light DApp mode does not require the user to have a local node or any wallet! The app will connect to an online node to get data and post transaction, and to an online signer to sign the transaction for the user.

That means, **anyone can use a DApp and interact with it without having anything to install**.

![light DApp](https://vote-on-ethereum.github.io/Concept/src/hybriddApp.svg)

To try it, simply go to https://vote-on-ethereum.github.io/App-Basic with a classic web browser and let the magic happen.

## Technical explanation

### How the DApp knows which node to use?

When browsing the DApp with Mist, Mist injects a web3 instance than can be used by the DApp to access the local node and wallet. When no web3 instance is available, the DApp will use the online node.

Here is the specific code provided by [Mist Doc](https://github.com/ethereum/mist/blob/develop/MISTAPI.md#note-for-dapp-developers):

```node
if(typeof web3 !== 'undefined')
  web3 = new Web3(web3.currentProvider); //use Mist node and wallet
else
  web3 = new Web3(new Web3.providers.HttpProvider("https://URL_TO_ONLINE_NODE")); //use the online node
```

### How the DApp signs transactions without a wallet?

When no wallet is provided to the DApp, it will connect to the online signer and ask to sign transaction. The online signer will use its wallet to sign the transaction. That means that the gas needed for the transaction will be paid by the signer wallet: the DApp become **free to use for the user**.
