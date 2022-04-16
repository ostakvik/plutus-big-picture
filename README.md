# plutus-big-picture. 
Attempts to explain what the big picture looks like. PAB's , on-chain code, off-chain code, on-chain code repos etc.
The first lesson in Plutus piioneer program explains the EUTXO modell used in Cardano blockchain. The understanding of this is crucial for any further work.
However, based on the discord questions, ama's ++, it seems to be lack of information of what the Plutus landscape looks like.
The Pioneer  program uses the Plutus Playground to run the code. This webapplication emulates both the wallet (the off-chain code) and the 'on-chain validating' script to be executed on the validating Cardano Node. The source file in every example (?) contains both on-chain code and the off-code. In real life (according to my understanding) this will not be the case.


When a transaction contains a smart contract script, the complete script (Source code) must be contained within the transaction.
It must be the source code. It can not be the compiled code. If this was the case there whould be a new hash of this code every time the Haskell compiler was upgraded and produced a more efficient code, or if the Plutus library beneath has changed implementation of some method. Keep in mind that a smart contract stored on chain must be "valid" in all times to come (100 years+).
Even though nobody is using it anymore, this specific transaction with this plutus script MUST validate 15 years from now.
How is this backward compatibility preserved?

Regarding the size of the script on how much space this cuurently requires within the transaction is to be solved by using script referencing ( https://cips.cardano.org/cips/cip33/). 
This allows that the transaction only keeps a reference to the script and that the complete script is stored somewhere else.


And then we have the "wallet". 
The wallet contains the private key(s). Whenever a transaction is to be signed prior to sending it to the blockchain, the off-chain application needs to interact with the wallet in order to obtain the signing key.
Typically what we see today (april 2022), there are not all wallets that is interacting with the different dApps (like DEX'es). Some wallets do provide a connection with the given dApp-application (that runs within a web browser). If I currently are using Yoroi as wallet, and want to use a service like MinSwap, I can not use the Yoroi wallet and must instead use i.e. Nami Wallet. 
Point is : not every wallets provides a connecting api.


The "PAB" (Plutus Application Backend" has been briefly mention a few times. What will this do?
The PAB is still (april 2022) a bit vague. As far as I understand, the PAB is not a specific application, but instead a set of functionality that provides all the stuff that a Dapp needs to do.
AFAIK, one of the most important services PAB provides is to assemble the transaction that is to use a script. It must put the script code into the transaction and then send it to the BC. (??? verify). Does the PAB framework provides an API that enables a simple integration with applications?
Need more read-up on this....

A drawing that attempts to give an architectual overview:
 
![architecture_application_pab_wallet_cardano-node](https://user-images.githubusercontent.com/49366319/163685649-473cd60b-7c92-4c4d-9afa-462ccd48660a.png)

 
