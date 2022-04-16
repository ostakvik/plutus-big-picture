# plutus-big-picture. Some thoughts after Plutus Pioneer Program cohort2, Session #4
Attempts to explain what the big picture looks like. PAB's , on-chain code, off-chain code, on-chain code repos etc.
The first lesson in Plutus piioneer program explains the EUTXO modell used in Cardano blockchain. The understanding of this is crucial for any further work.
However, based on the discord questions, ama's ++, it seems to be lack of information of what the Plutus landscape looks like.
The Pioneer  program uses the Plutus Playground to run the code. This webapplication emulates both the wallet (the off-chain code) and the 'on-chain validating' script to be executed on the validating Cardano Node. The source file in every example (?) contains both on-chain code and the off-code. In real life (according to my understanding) this will not be the case.

Further we get to hear that the input to a transaction is the hash of the on-chain code, not the code it self. This implies that the actual code to be executed have to be looked up somewhere else. 
EDITED: This is not correct! Currently (april 2022), the whole complete compiled on-schain script has to be included into the transaction that is submitted. based ont he fact that a Cardano block is currently 80KB (increased from 64 KB to 72 KB to 80 KB), it's obvious that a script migth take a significantly part of the available spave in a block. There are a process going on to reference a script. This means that instead of putting the complete script code into the transaction, we add a reference to the script instead. This requires that the script is storede somewhere else. Question is: wher?. Since the transaction ont the blockchain is to live forever, it's obvious that the compiled script code has to be stored permanently as well. And always accessible. I see no other alternative that this script code must also be stored on the blockchain. How?

And then we have the "wallet". 
The wallet contains the private key(s). Whenever a transaction is to be signed prior to sending it to the blockchain, the off-chain application needs to interact with the wallet in order to obtain the signing key.
Typically what we see today (april 2022), there are not all wallets that is interacting with the different dApps (like DEX'es). Some wallets do provide a connection with the given dApp-portal. If I currently are using Yuroi as wallet, and want to use a service like MinSwap, I can not use the Yuroi wallet and must instead use ccVault. (or maybe it was another one). Point is : not every wallets supports connection with the different services.
Question: who makes the "plugin" code to allow a wallet to interact with a given service? Is is the creators of the wallet that needs to decide and then implement, or is it the Service providers that decides to make the plugin for a givens set of wallets?
Needs to investigate more int this.



The "PAB" (Plutus Application Backend" has been briefly mention a few times. What will this do?
The PAB is still (april 2022) a bit vague. As far as I understand, the PAB is not a specific application, but instead a set of functionality that provides all the stuff the PAB needs to do (?).
AFAIK, one of the most important services PAB provides is to assemble the transaction that is to use a script. It must put the script code into the transaction and then send it to the BC. (??? verify).
 
 ![architecture_pab_wallet_Cardano-node](https://user-images.githubusercontent.com/49366319/163684135-85bc9c80-936e-4205-be45-f97e3f0bd57f.png)


 
 
