---
layout: post
title: "Smart contract drafting for complete and utter beginners"
date: 2016-09-12
---

So you have heard of the term "smart-contract", probably in the same sentence as "blockchain", "Bitcoin" or "Ethereum". You may have read some articles stating that smart-contracts will revolutionise our legal framework, put lawyers out of work, give lawyers more work to do or create some kind of libertarian-anarcho-capitalist wonderland. Alternatively, you may have read how smart-contracts are insecure, inefficient and completely useless.

Smart-contracts are nothing new. A smart-contract is really just some computer code that plays a role in a transaction, this role may be to facilitate some element of the transaction to lower transaction costs, or it could be to make the contractual terms self-enforceable or self-executable, or something else entirely.

_If you know about blockchains, Bitcoin and Ethereum you can skip this next part and go to **Practical smart-contract coding** below_

### OK. So why am I hearing about smart-contracts all the time now?

All you need for a smart contract is a computer system to which the parties have access. However, this requirement raises problems, if we are to be be party to an agreement that is going to use computer code to execute our agreement (perhaps irrevocably) we must have absolute trust in the system. This level of trust is not impossible to achieve, but it limits the free flowing, arms-length type transactions that can occur in everyday life. The number of entities that we can trust to transact is limited, and these entities also limit the types of transactions that we can perform.

This trust issue was insurmountable until the Bitcoin blockchain was established in 2007. The Bitcoin network has been the proving ground for blockchain technology. Although you may have heard of some high-profile hacks of entities that trade bitcoin, the fundamental integrity of the network itself remains sound, with very large Bitcoin transaction processing operations ("miners") springing up as a new industry. For our purposes here, we only need to say that the blockchain is a computer system that everyone can trust because it does not reside under any specific person or entity's control, rather, its integrity is maintained by a large (or "distributed") network that is practically impossible to corrupt. This has greatly increased the potential range of applications for smart-contracts, and created a possibility that smart-contracts may grow into a major means of carrying out financial transactions.

Blockchain technology was pushed exactly in this direction with the release of the Ethereum blockchain in mid-2015. Ethereum adds to the blockchain concept by allowing pieces of code to exist on the blockchain. Where Bitcoin allowed for accounts and their balances to exist on the chain - allowing for amounts of Bitcoin to be moved between accounts. The Ethereum blockchain has roughly the same elements as Bitcoin, accounts and balances (but instead of "Bitcoins" as its' currency it uses "Ether"), but it also adds another dimension by allowing pieces of code (or "contracts") to exist on the chain and hold value. In this way, contracts can regulate, and impose conditions on transactions.

### Practical smart-contract coding

This tutorial will be about coding a very simple and very common type of transaction. A typical online shopping transaction where Party A puts up an item for sale, Party B then agrees to the price and pays for the item, then Party A must send the item to Party B, and Party B acknowledges receipt of the correct item, or they do not, and both parties enter into a negotiation.

Readers with a legal frame of mind, who are perhaps wanting to work out what makes these coded "contracts" contractual will be surprised at the lack of legal content in this code. The coded functions that we create will be of an instrumental nature, covering the bare building blocks of a simple sale. Common contractual provisions relating to the sale of goods are not included, such as:

* Jurisdiction
* Payment terms and delinquency charges
* The point at which legal title transfers to the buyer
* Limitation of the seller's liability for damages,
* The assignment or delegation of rights under the contract
* Recovery of expenses and the appointment of an arbitrator

However, as this area continues to develop these functions may be written into future sales contracts. Also absent is a large amount of the greater context of the transaction, this contract will not, for instance provide a space for communication between the buyer and seller so that the seller can provide their postal address. As such, this will be a bare piece of code that must function within a broader context, a context which could include written or unwritten agreements that govern the legal issues outlined above.

_So then, what is the point of such an incomplete agreement?_

Well, although incomplete, this "contract" is a workable basis for decentralised, and disintermediated transactions between two arms-length individuals. There are no banks, payment services or online markets involved. This is a new kind of transaction for an economy adapted to the internet.

Regardless of whether we want to get into the minutae of the traditional sales contract, and include everything to make this smart-contract complete, we need to start at the beginning, with the functions that will facilitate the nuts and bolts of the transaction. Not only will it give us an understanding of the kind of things that are possible, but it is the only place from which we can encode, include elsewhere, adapt, or discard these contractual norms.

_Ok, I get that, but do I need to actually "code"?_

Yes. You need to read some code, write some code and understand what it is that the code is doing. At the moment there is no graphical user interface (GUI) that you can use to write smart-contracts on Ethereum, and to be honest, even if there were you would probably want to understand the actual code anyway, otherwise it would be like interpreting a contract in a foreign language via an interpreter.

### The transaction

This should be familiar, we aren't really worried about our counterparty failing to provide payment or the goods because we can see them, the money and the item:

![facetoface](/assets/facetoface.png)

Internet commerce greatly expanded the amount of people that we could transact with, the in this case, surety in the counter-party's performance of the contract was given through the platform the buyer and seller were transacting, this surety was a mixture of financial indemnity and the effect that a faulty/late arriving item could have on the sellers reputation on the platform:

![internet](/assets/internet.png)

A decentralised transaction has no such entity to either insuring or incentivise the parties to execute the transaction properly. The two most obvious faults could be that the seller takes the buyers cash and does not send the item, or the buyer says that the item did not arrive when it actually did arrive and but never-the-less demands a refund. Therefore, outside of a larger context for the transaction and external incentives, decentralised transactions require their own internal incentives for parties to uphold their part of the bargain. The most obvious way of doing this is to use money (in this case "Ether") as a security deposit:

![decentralised](/assets/decentralised.png)

The smart-contract we are going to code will follow the above schema, the contract that we will be writing was developed for as a protocol for Ethereum trustless sales, by the github user chriseth. You can find the github entry here, including a discussion on limitations and possible additions that can/should be made to it. The seller will "create" the contract on the Ethereum blockchain and put double the sale price into the contract. The buyer will then purchase the item by also putting double the sale price into the contract. So at this stage we have four times the sale price in the contract. The seller will then send the item, when the buyer receives it, they will acknowledge the receipt. Then the contract will send three times is sale price to the seller, and one sale price value to the buyer, leaving the seller +1 sale price richer, and the buyer -1 sale price poorer.

### Required material

A smart-contract deployed on Ethereum requires an Ethereum "node" that is up-to-date with the latest block. There are many tutorials on how to get up and running with your own Ethereum node. Viewed in its natural environment the blockchain looks something like this:

![terminal](/assets/terminal.png)

From here we can run commands and interact with the blockchain, we can check our account balance and send Ether, we can even deploy smart-contracts using a code that might look a bit like this:

![bytecode](/assets/bytecode.png)

However, this is a confusing and intimidating way of looking at it. This is reason why developers have created Ethereum "wallets" which can operate as pleasing graphical user interfaces between you and this command-line type code. For this tutorial we will be using the official Ethereum wallet, that you can download here. There are a number of tutorials that can show you around the wallet, but in essence it is a way of getting a working Ethereum node as well as writing and deploying contracts without having to deal with the difficulties of the command-line.

A wallet looks like this:

![wallet](/assets/wallet.png)

The top menu says that I am on the TEST-NET or the playground for writing and experimenting with contracts, it is separate from the real, actual Ethereum chain but works in the same way, the Ether shown here is only good for the test-net. This is where you want to be because playing around with Ethereum contracts means spending Ether and Ether costs money it is actually surprisingly easy to trap Ether in an contract with no way of getting it back. The text "4s since last block" means that the last block my wallet/node received was 4 seconds ago, meaning that my node is up to date with the state of the network as a whole. Depending on how well everything is running you should be on a new block every 30 seconds to two minutes on the TEST-NET.

Below that we have three accounts that are running off the same node and I can access each of the them with a different password. They are independent, and I can perform transactions between them.

Below that there is a log of the most recent transactions, for instance the last thing I did was send a message (with no Ether attached) to the address of a contract.

The next screen we want to look at is the contracts screen. We can get there by clicking on the blue "CONTRACTS" at the top of the wallet:

![walletcontracts](/assets/walletcontracts.png)

Here is a list of contracts that I have either put onto the blockchain myself, or I have chosen to watch. Watching a contract means that you want to interact with it in some way. To do this you need the contract "address" and the "interface" - more on that later.

Click on DEPLOY NEW CONTRACT:

![deploy](/assets/deploy.png)

Here we see a snippet of the Ethereum scripting language "Solidity" for the first time. This is where we write the code that we want to put on the blockchain, above is the address of the wallet you wish to send the contract from (this will be the contract "owner", but a better term could be "originator" or "creator"). Just below that is where you can put Ether when you create the contract.

Now lets go back to the previous screen - CONTRACTS:

![deployed](/assets/deployed.png)

We are jumping slightly ahead into the future here, as this is what we will see when we interact with the decentralised sales contract that we are going to write. At the tope we see the name we have given to the contract (people can name the same contract different names), its address, and the amount of Ether stored in the contract at the moment.

To the left we also see who the parties are, that is, the buyer and seller (in this case both parties to my contract are accounts that I control through this wallet and so I see the name of both accounts, if I was dealing with a stranger their account would be some numbers and letters very similar to the contract address above. Here we are reading from the contract, in Ethereum's terms we are checking out the "state" of the contract, in more abstract programming terms we are seeing the value of variables.

To the right we see how to write to the contract, or how we change the state of the contract, in other terms, how we change the values of the variables. As we shall see we do this by running functions our wallet reads the code and finds the relevant functions and puts them in a drop down list, here we have selected the "Refund" function, we will see what that function actually does in a couple of minutes, but once we have selected a function we can then tell our wallet what account we want to run the function, and what amount of Ether we wish to attach to the "message" running the function.

Can we start to write the contract now?

Yes, I think we can.

Good.

We are going to write our contract in Solidity. Which is a programming language designed for writing contracts on Ethereum, it has some similarities to JavaScript. There are other programming languages that can do this, such as Serpent, which is similar to Python. However, the emphasis of late has been toward Solidity, and that is what the Ethereum wallet allows us to write in.

You can write code in a regular text editor, the only difference is that you need to name it with a .sol extension. If you are writing a contract called "example" you would save your text file as "example.sol". However, this would be a difficult way to go, as the only way to test your contract code is actually on the blockchain, loading your code to see if it works or has a bug can be long and tedious. So, We are going to write our contract using the browser-solidity page. It is a tool that gives us a nice environment to write in but you can also use it to perform tests to make sure that your code works. We are not going to be using it for testing, primarily because we have a very simple contract, but should you want to explore this area more, these tools will come in handy. For our purposes today, a great feature is that if you write some incorrect solidity syntax it will give you an error message on the right of the screen.

![soliditybrowser](/assets/soliditybrowser.png)

### The Code

 We are going to call our contract "Purchase", like so:

![purchase](/assets/purchase.png)

In law, a contract for sale will probably be incomplete and unenforceable if there is no agreement as to the fundamental terms, for a contract for sale these terms are usually going to be the identity of the parties (names) , the item for sale and the purchase price (denoted in currency). If we want to think of a traditional sales contract as a reuseable agreement, we simply plug these terms into the contract as variables, they can change but their nature, and their role and rights under the agreement are always similar.

In our agreement we will need three variables to make it work. The the "buyer", the "seller" and the "value". These are the things that will be unique to each use of this contract code. Notice that we do not identify the actual item for sale within this contract. This contract will assume that these kind of elements to the transaction (description of the goods, buyers address, etc) will occur "off-chain" and in the broader context of the transaction.

We create our variables like so, within the {} brackets we wrote earlier:

![variables](/assets/variables.png)

Each of these variable declarations have three parts, the a type, a keyword and a name. The type is what kind of variable it is:

* "uint" means "unsigned integer" which basically means a number
* "address" is an Ethereum address, like an account address or a contract address (eg: **0x683082bE79c1765cc06734f99B467766f2Ad1A3f** was the address for the contract I showed you in my wallet above.

Keywords are a little outside of the scope of this tutorial, but in this case calling a variable "public" means that the variable can be directly queried by other users and contracts (but not written). For this tutorial we will keep them public.

And the name is the name that we choose to give the variable, we can make it any word we like, but we need to be consistent throughout the contract when we refer to it.

So, we have made some space for our contract to hold a number, and two addresses.

We use these variables and make changes to them through "functions", for our contract we want to make the seller the person who creates the contract, and they also set the value - which is 1/2 of the amount that the seller will put in to the contract. So we will add a function like this:

![functionpurchase](/assets/functionpurchase.png)

The variables that we made in lines 3, 4 and 5 earlier, were empty. The Purchase() function gives two of them values. There is something unusual about this function that will not be the same for the other functions we will write. This function will only run when the contract is made and it will not appear in the drop down menu of available functions when we are viewing the contract in the Ethereum wallet. Functions like this are called "constructors" and the only way to create a constructor function is to give it the exact same name as the actual contract ("Purchase").

When the Purchase contract is created (contracts are created through a "message" to the Ethereum blockchain), Purchase() will run and the variable "seller" will be given the value of the address of the account creating the contract (the "sender" of the "message", or in Solidity - the "msg.sender"). Similarly, the "message" creating the contract has a "value" of Ether, because the seller when putting up the item for sale will put 2x the purchase price into the contract when creating it. Hence, the "value" variable (the sale price) will be the value included with the message divided by 2, or "msg.value / 2".

For the more programming minded, you will notice that this syntax is similar to dot notation, the main object is the "msg", and the "sender" and "value" are attributes of that object.

Now that we have dipped our toe into Solidity code and made a function to assign values the "seller" and "value" variables we should have a look at the structure of the transaction we are trying to code.

![structure](/assets/structure.png)

Each of the functions we need to write are in the white boxes, so far we have done the first. Next we need to make an allowance for the seller to change their mind and get their deposit back from the contract:

![abort](/assets/abort.png)

you will notice the caution sign next to the seller.send(this.balance) line. This means that we may not be able to do this much longer, but for now it is working.

abort() will simply send the balance of the contract back to the seller.

Next, we need to add the function where the buyer confirms the purchase, this means that simply, if the buyer places enough Ether in the contract, their address is placed in the "buyer" variable:

![confirmpurchase](/assets/confirmpurchase.png)

When the person buying this wants to confirm the purchase, they will run this function by sending a message and adding a value, if the value is correct, then they will be the "buyer", if the value is not correct, the function cannot be run (it is "thrown").

Next, we make a function where the buyer has paid, but the seller cannot perform the sale, this will return the parties to roughly the pre-transaction situation:

When the person buying this wants to confirm the purchase, they will run this function by sending a message and adding a value, if the value is correct, then they will be the "buyer", if the value is not correct, the function cannot be run (it is "thrown").

Next, we make a function where the buyer has paid, but the seller cannot perform the sale, this will return the parties to roughly the pre-transaction situation:

![refund](/assets/refund.png)

[I say roughly the pre-transaction situation, because although Ethereum transactions do not have intermediaries, there is still a (small) transaction cost imposed by the network (called "gas") for changing the state variables in a contract. In this case, the seller will get what they paid (2x value) and the buyer will get the balance (rougly 2x the value)].

Finally, we write a function that the buyer will run once they take delivery of the item. This will send the purchase price and the security deposit to the seller, and the the buyer's security deposit back the buyer, it is very similar to refund():

![confirmreceived](/assets/confirmreceived.png)

Lastly we will add a "fallback" function, which will reject any messages where there is no function name give, or the function name does not match any of the function identifiers. This is not an issue if all if we can be assured that both parties will be interacting with the contract through the Ethereum wallet. But as we can interact with the Ethereum blockchain through the command-line, we cannot be sure that people will run it properly. You can have one fallback function and it cannot have a name.

![throw](/assets/throw.png)

Now we have a working contract.... sort of.

![entireone](/assets/entireone.png)

Our contract works, if both parties are pure of heart. Although it has some big drawbacks that you might have noticed, add the contract to the Ethereum wallet, buy going to DEPOY NEW CONTRACT, put your account in, give it a value of 2 ether, remove the text that is in the solidity contract source code box and cut and past what you have been working on in browser solidity:

![deployone](/assets/deployone.png)

The wrong people can run the wrong functions. A seller (or anyone) can run confirmReceival() and a buyer (or anyone) can run refund(). Less of a worry is that anyone can run abort(), but that is more of an nuisance than an opportunity to take swindle a counter-party.

We change this by writing modifiers and inserting them into our functions. Let's make one so that only the seller can run abort() and refund()

Below the closing } bracket under Purchase(), write:

![modifier1](/assets/modifier1.png)

modifier onlySeller() { if (msg.sender != seller) throw; _ }

Then at the top of abort() and refund(), in between the "function" line and the opening curly bracket, simply write "onlySeller"

![modifier2](/assets/modifier2.png)

This is a conditional (we included one in confirmPurchase() which threw out any running of that function without the correct msg.value.

Do the same for the buyer:

![modifierbuyer](/assets/modifierbuyer.png)

And add it to confirmReceival() in the same way you added the onlySeller modifier to abort() and refund().

We have fixed that issue, but there is another problem, even though the right functions can only be run by the right people, functions can still be run at the wrong time.

1. only the seller can run abort(), but they should not be able to do this after the buyer has entered the purchase price, as abort will send the contract balance back to the seller (including the buyer's deposit).
2. confirmPurchase() can be run at any time, this is a problem if a buyer pays into the contract, then another person also pays into the contract, meaning that their place is usurped in the contract. This would disadvantage the original "buyer" and advantage the seller as the "balance" would contain more than was intended - confirmPurchse() must only be run once
3. Similarly, confirmReceived() and refund() can be run at any time, this is more of a housekeeping issue, but it will generate an error, so we need to make sure that they can only be run after confirmPurchase().

We can achieve this though another modifier, and we will have to add another, new type of variable, an enum.

WARNING: this part could get confusing. If you get lost, just follow the instructions and have a look at what happens and it should make sense

First, lets map out our transaction through time. It goes through 3 stages, Created, Locked and Inactive:

![state](/assets/state.png)

Created is where we can run abort(), and confirmPurchase(), after that point it is Locked and no other users of the Ethereum network can change the values of the seller and buyer variables. Inactive is a bit unnecesary, but it just highlights that the transaction is over.

We will create the enum where we put our other variables (note that we put in two lines here):

![enumvariables](/assets/enumvariables.png)

Here we have a enum State (capital S), that is linked to a variable (lower case s) state

Essentially our enum will cycle through each of the transactions states, it will act like a gate, out enum can be set to the following - State.Created, State.Locked, State.Inactive. We will see the variable displayed in our wallet as either 0, 1, 2 depending on which state the contract is in.

First, the state of the contract depends on what functions have been run:

1. At the beginning when out contructor function Purchase() is run: state = State.Created
2. If abort(), confirmRecieved() or refund() is run: state = State.Inactive
3. If confirmPurchase() is run: state = State.Locked

So put those variable definitions in each of those functions like so:

![enumset](/assets/enumset.png)

So we need to make a modifier that sits in a function that will check to see what state the contract is in, and will check that current state against the state that we allow the function to be run. If the contract is in the correct state the function can proceed, otherwise we will throw it out.

![enummodifier](/assets/enummodifier.png)

Now at the top of each function we run our inState() modifier, and we specify what state the contract must be in to allow the function to run. So, as abort() should only be run when the contract is in State.Created, we write, inState(State.Created), and this will go just below the onlySeller modifier we inserted earlier (what is important is that it is in the space between the "function" line and the opening curly bracket).

![enumgate](/assets/enumgate.png)

1. abort() and confirmPurchase() : inState(State.Created)
2. confirmReceived() and refund() : inState(State.Locked)
