# plutus-big-picture. 
Attempts to explain what the big picture looks like.  Dapp portals, wallets, Cardano-node, PAB's , on-chain code, off-chain code, on-chain code repos etc.
The first lesson in Plutus piioneer program explains the EUTXO modell used in Cardano blockchain. The understanding of this is crucial for any further work.
However, based on the discord questions, ama's ++, it seems to be lack of information of what the Plutus landscape looks like.
The Pioneer  program uses the Plutus Playground to run the code. This webapplication emulates both the wallet (the off-chain code) and the 'on-chain validating' script to be executed on the validating Cardano Node. The source file in every example (?) contains both on-chain code and the off-code. In real life this will not be the case. Within a tutorial scope , this is all fine, and also simplyfies stuff. However, it's important to outline the big picture of how it looks like in the real world


When a transaction contains a smart contract script (on-chain script), the complete script (Source code) must be contained within the transaction.
It must be the source code. It can not be the compiled code. If this was the case there whould be a new hash of this code every time the Haskell compiler was upgraded and produced a more efficient code, or if the Plutus library beneath has changed implementation of some method. Keep in mind that a smart contract stored on chain must be "valid" in all times to come (100 years+).
Reasons is that whenever a cardano  node is to be synched, all existing (historic) transactions must be validated. If some of these transactions contains a script, that script must be executed (TRUE or FALSE to see that the output generated is correct). 
There are 2 challenges related to this:
1) The script (source code) within the transaction is to be compiled (?) at the validating node. If this is a long time after the script was created, the Plutus library might have been changed (most likely and hopefully, it has). 
This means that the all new plutus versions must be backward compatible with the Plutus version(api) that was used at the time of smart contract introduction and all versions there after.

2) Let's dry-run the case where the script was added into the transaction as compiled Plutus code. Lets assume a use-case where the script is to lock a given amount of ADA for future redeeming. The given amount of ada is locked at an address equal to the hash of the script. Lets simplify this to be HASH-1. 5 Years later when the amount is to be redeemed a new transaction containing this script must be created. The Script (same old source code) is compiled off-chain (in the "Dapp portal) and the compiled version is included within the transaction. Now, lets also assume that the Plutus library has been changed during these 5 years. The compiled output is no longer the same as the original one 5 years ago. Meaning that the hash of this script is different, lets say HASH-2. There exist no address similar to HASH-2 and hence no ADA to redeem. The script will fail to validate.

NOTE: Add the link to a verification that plutus on-chain scripts are stored within a transaction as source code.

Regarding script stored as source code:How is this backward compatibility preserved?

Regarding the size of the script on how much space this currently requires within the transaction is to be solved by using script referencing ( https://cips.cardano.org/cips/cip33/). 
This allows that the transaction only keeps a reference to the script and that the complete script is stored within a transactions already stored on the blockchain.
This will be highly beneficial since a service will make 1000's of transactions using the same script.


And then we have the "wallet". 
The wallet contains the private key(s). Whenever a transaction is to be signed prior to sending it to the blockchain, the off-chain application needs to interact with the wallet in order validate that there is enough funds and to sign the transaction (private key within the wallet).
Typically what we see today (april 2022), there are not all wallets that is interacting with the different dApps (like DEX'es). Some wallets do provide a connection with the given DApp-application (that runs within a web browser). If I currently are using Yoroi as wallet, and want to use a service like MinSwap, I can not use the Yoroi wallet and must instead use i.e. Nami Wallet. 
Point is : not every wallets provides a connecting api.


The "PAB" (Plutus Application Backend" has been briefly mention a few times. What will this do?
The PAB is still (april 2022) a bit vague. As far as I understand, the PAB is not a specific application, but instead a set of functionality that provides all the stuff that a DApp is in need of.
AFAIK, one of the most important services PAB provides is to assemble the transaction that is to use a script. It must put the script code into the transaction and then send it to the BC. (??? verify). Does the PAB framework provides an API that enables a simple integration with applications?
Need more read-up on this....

A drawing that attempts to give an architectual overview:
 
 ![architecture_pab_wallet_cardano-node](https://user-images.githubusercontent.com/49366319/163684405-74d5830c-fec5-4089-b081-4c3c0273c759.png)

 
