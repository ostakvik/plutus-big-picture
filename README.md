# plutus-big-picture
Attempts to explain what the big picture looks like. PAB's , on-chain code, off-chain code, on-chain code repos etc.
The first lesson in Plutus piioneer program explains the EUTXO modell used in Cardano blockchain. The unserstanding of this is crucial for any further work.
However, based on the discord questions, ama's ++, it seems to be lack of information of what the Plutus landscape looks like.
The Pioneer  program uses the Plutus Playground to run the code. This webapplication emulates both the wallet (the off-chain code) and the 'on-chain validating' script to be executed on the validating Cardano Node. The source file in every example (?) contains both on-chain code and the off-code. In real life (according to my understanding) this will not be the case.

Further we get to hear that the input to a transaction is the hash of the on-chain code, not the code it self. This implies that the actual code to be executed have to be looked up somewhere else. This has been mentioned as publicly available "Cardano on-chain code repository". The concept about this is to me still very vague.
Since release on mainnet is approaching fast, this need to be resolved and information given to everyone that wants to write Cardano smart contracts.

And then we have the "wallet". This is said to run the off-chain code, and generate the transaction. But how can this be a common use case in real life? The wallet we use to today is Daedalus and Yoroi. They will never be able to run the off-chain part of my "smart-contract". My "off-chain" part needs to be "hosted" somewhere else. Do we expect that the wallet we use will be able to retrieve this off-chain code and execute it? It this case we need a bridge between the wallet and the repository containing my off-chain code. And of-course, there will be no transaction generated without access to my private key...which is kept safely within the wallet.  Something I don't understand here.

The "PAB" (Plutus Application Backend" has been briefly mention a few times. What will this do?
Further, I've herd (by Lars B) that currently the PAB needs to communicate to the blockchain using a Cardano Node.
 need more information on this.
 
