# Concepts

## Customers

These actors are the final user within Mintacoin, in this case, the developers who want to use the API. This account will be able to perform all the operations and transactions defined for Mintacoin:

* Create Accounts
* Create Assets
* Make accounts hold assets
* Handle payments between accounts.

## **Accounts**

This entity is the first class citizen, contains the information of the users who belongs to Mintacoin, and is managed by a Customer. With an account is possible to interact and make operations in Mintacoin and the blockchain through the different endpoints. The account is composed of the following information:

* **Address:** Contains public identification within Mintacoin, this address is built with _Ed25519 which_ is a public-key signature system.
* **Signature**: This is the secret to verify the authenticity of the account; This signature is also built with _Ed25519._
* **Wallet:** Each account will contain a wallet that is used to handle the account information within the blockchain.

## **Wallets**

This entity allows us to have control over our assets and their balances within the current working Blockchain. The wallet is composed by:

* **Account**
* **Blockchain**
* **Blockchain Public Key**
* **Blockchain Secret Key**
* **Asset Balances**

## Balances

This entity represents the total amount of an Asset possessed by a Wallet. This means that a Wallet could have many balances as the possessed assets.

## **Encryption**

This is a module that allows us to keep security in the account information and secure the transactions defined in Mintacoin. Is composed of the following services:

**Services:**

* **Cipher:** Main functions for the encryption and decryption process.
* **Keypair:** Main functions for the key creation and management of key cipher operations using words with entropy, called **Mnemonic words**.

## **Assets**

#### Assets

It is the representation of an asset within a blockchain network, which could contain a commercial and economic value; This asset can be exchanged by any other, and it can represent anything like:

\<aside> 📌 **Assets examples** ☕CUP - Coffee Cup 🪙MTK - Mintacoin Token 💵USDC - Dollar

\</aside>

The asset is composed by:

* **Code:** Alphanumeric value composed between 2 and 10 characters.
* **Supply:** This is the amount of the asset.

## Asset Holder

This entity represents the possession of an Asset by a Wallet. This possession is made through a trustline operation in the blockchain.

The Asset Holder entity could be a **Minter,** which represents that the account which holds the assets is the distributor of the asset.

## **Payments**

This context contains all the operations required to create the payment transaction, with the goal of transferring assets from the source account to a destination account. This context is an entity that is composed by:

* **Blockchain**
* **Source Account**
* **Destination Account**
* **Asset to be transferred**
* **Amount**
* **Status**
* **Successful Payment**

Take into account to create a successful payment is required to

## **Blockchains**

#### Blockchains

This entity contains information about the protocol where the blockchain transactions are being executed. Currently, Mintacoin runs over the Stellar Network.

#### BlockchainTx

This entity contains the records of the transactions executed within the Blockchain network, this aims to have a measurable or analyzable result such as account creation, asset creation, payment, etc. Mainly is composed of the following fields:

* **Tx Hash:** This is the identifier of the transaction within the blockchain.
* **Tx Response:** This is the raw information of the transaction.
* **Transaction** **Types**
