---
layout: post
title: "A beginners guide to smart-contract drafting for lawyers"
date: 2016-09-12
author: Ari Dyball
---
***
_**Disclaimer**: this post is designed to help people familarise themselves with the concepts of coding smart-contracts on a blockchain. It is intended that the code used in this blog is for demonstration purposes and is to be used on the Ethereum "TEST-NET" only, and not on the actual Ethereum blockchain. I do not make any assurances that this code, or the solidity programming language, is safe to use with digital currency that has an actual monetary value_

_**Explainer**: this post is **long**. It aims to explain how to write code on the blockchain in simple non-technical language, to follow along will involve familiarising yourself with relatively complex tools such as the Ethereum Wallet, and, to actually deploy the smart-contract and see it in action will require you to download and install the wallet and then sync the wallet up to the most recent block in the Ethereum test-net. Synching the wallet to the test-net will take at least 3-4 hours and could take as long as a day, it is probably best to leave the blockchain synching overnight unless you really enjoy watching a progress bar. In short you can read this post in one sitting to get the gist of what we are doing, however, if you want to follow along, then you will need to set aside some time._

***

You may have heard of the term **"smart-contract"**. Possibly it was in the same sentence as **"blockchain"**, **"Bitcoin"** or **"Ethereum"**. You may have read some articles stating that smart-contracts will [revolutionise our legal framework](http://www.afr.com/technology/blockchain-smart-contracts-to-disrupt-lawyers-20160529-gp6f5e), [put lawyers out of work](http://qz.com/459009/the-technology-behind-bitcoin-could-replace-lawyers-too/), give [lawyers more work](http://www.afr.com/technology/king--wood-mallesons-devises-a-smart-contract-which-keeps-lawyers-in-a-job-20160712-gq3wyl), or create some kind of libertarian-anarcho-capitalist [wonderland](https://bitnation.co/). Alternatively, you may have read how smart-contracts are [insecure](https://blog.blockstack.org/solar-storm-a-serious-security-exploit-with-ethereum-not-just-the-dao-a03d797d98fa#.yoh9mxujc), [inefficient](https://forum.ethereum.org/discussion/4942/high-gas-price-is-killing-some-projects-seriously) and completely [useless](http://www.coindesk.com/three-smart-contract-misconceptions/).

Smart-contracts are nothing new. A smart-contract is really just some computer code that plays a role in a transaction, this role may be to facilitate some element of the transaction to lower transaction costs, or it could be to make the contractual terms self-enforceable or self-executable, or something else entirely.

_If you know about blockchains, Bitcoin and Ethereum you can skip this next part and go to **Practical smart-contract coding** below_

### _Why are smart-contracts in the news?_

There have been some changes in the last few years that have made smart-contracts a more attractive proposition than they were previously.

In one sense, your starting point for a smart contract is a computer system to which the parties have access. However, even this simple requirement raises problems, if we are to be be party to an agreement that is going to use computer code to execute our agreement and alter our rights we must have absolute trust in the system and the person maintaining it. This level of trust is not impossible to achieve, but it limits the free-flowing, arms-length type transactions that can occur in everyday life. The number of entities that we can entrust to maintain the integrity of the system we are using is limited, and, naturally, these entities also limit the types of transactions that we can perform, and this trust usually incurs a transaction fee.

This trust issue was insurmountable until the [**Bitcoin**](https://bitcoin.org/bitcoin.pdf) blockchain was established in 2007. The Bitcoin network has been the [proving ground](http://www.coindesk.com/bitcoin-venture-capital/) for blockchain technology. Although you may have heard of some high-profile [hacks](http://satoshilabs.com/news/bitcoin-thefts/) of entities that trade bitcoin, the fundamental integrity of the network itself remains sound, with very large Bitcoin transaction processing operations ("miners") springing up as a new industry. For our purposes here, we only need to say that the blockchain is a computer system that everyone can trust because it does not reside under any specific person or entity's control, rather, its integrity is maintained by a large (or "distributed") network that is practically impossible to corrupt. This has greatly increased the potential range of applications for smart-contracts, and created a possibility that blockchain-based smart-contracts may grow into a major means of carrying out financial [transactions](https://www.ecb.europa.eu/pub/pdf/scpops/ecbop172.en.pdf).

Blockchain technology was pushed exactly in this direction with the release of the [Ethereum](https://github.com/ethereum/wiki/wiki/White-Paper) blockchain in mid-2015. Ethereum adds to the blockchain concept by allowing pieces of code to exist on the blockchain. Bitcoin uses two elements accounts and their balances - this enables amounts of Bitcoin to be moved between accounts. The Ethereum blockchain has roughly the same elements as Bitcoin, accounts and balances, but it also adds another dimension by allowing pieces of code (or "contracts") to exist on the chain and hold value. In this way, smart-contracts can regulate and impose conditions on transactions.

## Practical smart-contract coding - "contract" for sale

This tutorial will be about coding a very simple and very common type of transaction. A typical online shopping transaction where _Party A_ puts up an item for sale, _Party B_ then agrees to the price and pays for the item, _Party A_ must send the item to _Party B_, and _Party B_ then acknowledges receipt of the correct item. If _Party B_ does not confirm receipt of the item, both parties enter into a negotiation.

Readers with a legal frame of mind, who are perhaps wanting to work out what makes these coded "contracts" _contractual_ will be surprised at the lack of legal content in this code. The coded functions that we will create in this tutorial will really be of an instrumental nature, covering the bare building blocks of a simple sale. Common contractual provisions relating to the sale of goods are not included, such as:

* Jurisdiction issues
* A description of the goods
* Payment terms and delinquency charges
* The point at which legal title transfers to the buyer
* Limitation of the seller's liability for damages,
* The assignment or delegation of rights under the contract
* Recovery of expenses and the appointment of an arbitrator

However, as this area continues to develop these functions may be written into future sales contracts. Also absent is a large amount of the greater context of the transaction, this contract will not, for instance provide a space for communication between the buyer and seller so that the seller can provide their postal address. As such, this will be a bare piece of code that must function within a broader context, a context which could include written or unwritten agreements that govern the legal issues outlined above.

### _What is the point of such an incomplete agreement?_

Well, although it is in a legal sense largely incomplete, this "contract" is arguably a workable basis for a decentralised, trustless, and disintermediated transaction between two arms-length individuals, something that has been, until now, impossible to carry out in the world of ecommerce. There are no banks, payment services or online markets involved. This is a new kind of transaction for an economy adapted to the internet.

Regardless of whether we want to get into the minutae of the traditional sales contract, and include everything to make this smart-contract complete and enforceable from a legal standpoint, we need to start at the beginning, with the functions that will facilitate the nuts and bolts of the transaction. Not only will it give us an understanding of the kind of things that are possible, but the instrumental foundations of the transaction itself is the only place from which we can encode, adapt, or discard these contractual legal requirements.

### _To write a smart-contract, do you need to actually "code"?_

Yes. You need to read some code, write some code and understand what it is that the code is doing. At the moment there is no graphical user interface (GUI) that you can use to write smart-contracts on Ethereum, and, to be honest, even if there were you would probably want to understand the actual code anyway, otherwise it would be like negotiating a contract in a foreign language using an unreliable interpreter.

## The Transaction

Lets take a simple face-to-face transaction. This should be familiar. In this case we aren't really worried about our counter-party failing to provide payment or supply the goods because we can see them, the money and the good in question:

![facetoface](/assets/facetoface.png)

Internet commerce greatly expanded the amount of people that we could deal with and created a different kind of transaction, here, surety in the counter-party's performance of the contract was given through the web platform the buyer and seller were using to transact, this surety was a mixture of buyers insurance and the effect that a faulty/late arriving item could have on the sellers _reputation_ on the platform:

![internet](/assets/internet.png)

In contrast a _decentralised_ transaction has no such entity to either insuring or incentivising the parties to execute the transaction properly. The two most obvious dangers could be that the seller takes the buyer's cash and does not send the item, or the buyer says that the item did not arrive when it actually did arrive and but never-the-less demands a refund. Therefore, outside of a larger context for the transaction and external incentives, decentralised transactions require their own internal incentives for parties to uphold their part of the bargain. The most obvious way of doing this is to use money (in this case "Ether") as a security deposit:

![decentralised](/assets/decentralised.png)

***
_Note: following some discussions that I have had with economists this transaction structure has been criticised as inefficient and possibly ineffective as a means of incentivising the parties. This has opened up some interesting lines of enquiry into how a decentralised and essentially anonymous network can facilitate a system of managing the reputations of individual actors on the network. There are a number of blockchain reputation systems in [development](http://dapps.ethercasts.com/) and this will be the subject of my next post. Despite these criticisms we should look at this transaction structure anyway, because it is a simple means of illustrating smart-contract drafting, and, despite its flaws, it may form a standard form of transacting on the blockchain_

***

The smart-contract we are going to code will follow the above decentralised schema, the contract that we will be writing was developed as a protocol for Ethereum trustless sales by the github user and solidity program language developer [chriseth](https://github.com/chriseth). You can find the github entry, including a discussion on limitations and possible additions that can/should be made to it [here](https://gist.github.com/chriseth/b16e8e76a423b7671e99).

Transaction structure:
* The seller will "create" the contract on the Ethereum blockchain and put **double** the sale price into the contract.
* The buyer will then purchase the item by also putting **double** the sale price into the contract.
* At this stage we have _four_ times the sale price in the contract.
* The seller will then send the item.
* When the buyer receives it, they will acknowledge the receipt.
* The contract will then send three times is sale price to the seller, and one sale price value to the buyer, leaving the seller +1 sale price richer, and the buyer -1 sale price poorer.

### Required material

A smart-contract deployed on Ethereum requires an Ethereum **node** that is up-to-date with the latest block.

From our computer comman line interface the Ethereum blockchain looks something like this:

![terminal](/assets/terminal.png)

From here we can run commands and interact with the blockchain, we can check our account balance and send Ether, we can even deploy smart-contracts using a code that might look a bit like this:

![bytecode](/assets/bytecode.png)

However, this is a confusing and intimidating way of looking at it. This is reason why developers have created Ethereum "wallets" which can operate as pleasing graphical user interfaces between you and this command-line type code. For this tutorial we will be using the official Ethereum Wallet, that you can download [here](https://www.ethereum.org/), in essence, the wallet is a means of getting a working Ethereum node as well as space for writing/deploying and interacting with contracts and other Ethereum users without having to deal with the difficulties of the command-line. There are many [tutorials](https://www.youtube.com/watch?v=Y3JfLgjqNU4) on how to get up and running with your own Ethereum node/wallet.

When open, the wallet looks like this:

![wallet](/assets/wallet.png)

The top menu says that I am on the test-net or the playground for writing and experimenting with contracts, it is separate from the actual Ethereum chain but works in the same way, the Ether used on the test-net is only good for the test-net. This is where you want to be because playing around with Ethereum contracts means spending Ether and Ether costs [money](https://www.btcmarkets.net/) and it is actually surprisingly easy to accidentally trap Ether in an contract with no way of getting it back. The text up the top - "4s since last block" - means that the last block my wallet/node received was 4 seconds ago, meaning that my node is up to date with the state of the network as a whole. Depending on how well everything is running you should be on a new block every 30 seconds to two minutes on the test-net.

Below that we have three accounts that are running off the same node and I can access each of the them with a different password. They are independent, and I can perform transactions between them as if they were controlled by different people.

Below that there is a log of the most recent transactions, for instance the last thing I did was send a message (with no Ether attached) to the address of a contract.

The next screen we want to look at is the contracts screen. We can get there by clicking on the blue "CONTRACTS" at the top of the wallet:

![walletcontracts](/assets/walletcontracts.png)

Here is a list of contracts that I have either put onto the blockchain myself, or I have chosen to watch. "Watching" a contract means that you want to interact with it in some way. To do this you need the contract "address" and the "interface" - more on that later.

Click on DEPLOY NEW CONTRACT:

![deploy](/assets/deploy.png)

Here we see a snippet of the Ethereum scripting language "Solidity" for the first time. This is where we write the code that we want to put on the blockchain, above is the address of the wallet you wish to send the contract from (this will be the contract "owner", but a better term could be "originator" or "creator"). Just below that is where you can put Ether when you create the contract.

Now lets go back to the previous screen - CONTRACTS:

![deployed](/assets/deployed.png)

We are jumping slightly ahead into the future here, as this is what we will see when we interact with the decentralised sales contract that we are going to write. At the top we see the name we have given to the contract (people can name the same contract different names), its address, and the amount of Ether stored in the contract at the moment.

To the left we also see who the parties are, that is, the buyer and seller (in this case both parties to my contract are accounts that I control through this wallet and so I see the name of both accounts, if I was dealing with a stranger their account would be some numbers and letters very similar to the contract address above. Here we are "reading" from the contract, in Ethereum's terms we are checking out the "state" of the contract, in more abstract programming terms we are seeing the value of variables.

To the right we see how to write to the contract, or how we change the state of the contract, in other terms, how we change the values of the variables. As we shall see we do this by running functions our wallet reads the code and finds the relevant functions and puts them in a drop down list, here we have selected the "Refund" function, we will see what that function actually does in a couple of minutes, but once we have selected a function we can then tell our wallet what account we want to run the function, and what amount of Ether we wish to attach to the "message" running the function.

### Writing the contract

We are going to write our contract in [Solidity](https://solidity.readthedocs.io/en/develop/). Which is a programming language designed for writing contracts on Ethereum, it has some similarities to JavaScript. There are other programming languages that can do this, such as [Serpent](https://github.com/ethereum/wiki/wiki/Serpent), which is similar to Python. However, the emphasis of late has been toward Solidity, and that is what the Ethereum wallet allows us to write in.

You can write code in a regular text editor, the only difference is that you need to name it with a .sol extension. If you are writing a contract called "example" you would save your text file as "example.sol". However, this would be a difficult way to go, as the only way to test your contract code is actually on the blockchain, loading your code and waiting for it to be uploaded to the blockchain to see if it works can be long and tedious. So, We are going to write our contract using the [browser-solidity](https://ethereum.github.io/browser-solidity/#version=soljson-v0.4.2+commit.af6afb04.js) page. It is a tool that gives us a nice environment to write in but you can also use it to perform tests to make sure that your code works. We are not going to be using it for testing, primarily because we have a very simple contract, but should you want to explore this area more, these tools will come in handy. For our purposes today, a great feature is that if you write some incorrect solidity syntax it will give you an error message on the right of the screen.

![soliditybrowser](/assets/soliditybrowser.png)

For our purposes today, a great feature is that if you happen to write some incorrect solidity syntax it will give you an error message. Remove the text in the browswer-solidity editor and begin with a clean slate.

### The Code

We are going to call our contract "Purchase", and we instantiate our contract like so:

![purchase](/assets/purchase.png)

In law, a contract for sale will probably be incomplete and unenforceable if there is no agreement as to the fundamental terms, for a contract for sale these terms are usually going to be the _identity_ of the parties (names) , the _item_ for sale and the _purchase price_ (denoted in currency). If we want to think of a traditional sales contract as a reuseable agreement, we simply plug these terms into the contract as _variables_, they can change but their nature, and their role and rights under the agreement are always the similar.

In our agreement we will need three variables to make it work. The the _"buyer"_, the _"seller"_ and the _"value"_. These are the things that will be unique to each use of this contract code. Notice that we do not identify the actual item for sale within this contract. This contract will assume that these kind of elements to the transaction (description of the goods, buyers address, etc) will occur "off-chain" and in the broader context of the transaction.

We create our variables, within the {} brackets we wrote earlier:

![variables](/assets/variables.png)

Each of these variable declarations have three parts, the a type ("address", "uint"), a keyword ("public") and a name (eg: "seller"). The type is what kind of variable it is:

* "uint" means "unsigned integer" which basically means a number
* "address" is an Ethereum address, like an account address or a contract address (eg: **0x683082bE79c1765cc06734f99B467766f2Ad1A3f** was the address for the contract I showed you in my wallet above.

Keywords are a little outside of the scope of this tutorial, but in this case calling a variable "public" means that the variable can be directly queried by other users and contracts (but not written). For this tutorial we will keep them public.

And the "name" is the name that we choose to give the variable, we can make it any word we like, but we need to be consistent throughout the contract when we refer to it.

So, we have made some space for our contract to hold a number, and two addresses.

### Doing things with these variables

We use these variables and make changes to them through "functions". For our contract we want to make the seller the person who creates the contract, they load the contract onto the blockchain and add Ether at the same time - setting the value - which is 1/2 of the amount that the seller puts in to the contract.

We will add a function like this just underneath the variable definitions:

![functionpurchase](/assets/functionpurchase.png)

The variables that we made in lines 3, 4 and 5 earlier, were empty. The **Purchase()** function gives two of them values. There is something unusual about this function that will not be the same for the other functions we will write. This function will only run when the contract is first loaded onto the blockchain and it will not appear in the drop down menu of available functions when we are viewing the contract in the Ethereum wallet. Functions like this are called "constructors" and the only way to create a constructor function is to give it the exact same name as the actual contract ("Purchase").

When the Purchase contract is created (contracts are created through a "message" from the creator of the contract to the Ethereum blockchain), **Purchase()** will run and the variable "seller" will be given the value of the address of the account creating the contract (the "sender" of the "message", or in Solidity - the "msg.sender"). Similarly, the "message" creating the contract has a "value" of Ether, because the seller when putting up the item for sale will put 2x the purchase price into the contract when creating it. Hence, the "value" variable (the sale price) will be the value included with the message divided by 2, or "msg.value / 2".

_For the more programming minded, you will notice that this syntax is similar to dot notation, the main object is the "msg", and the "sender" and "value" are attributes of that object._

Now that we have dipped our toe into Solidity code and made a function to assign values the "seller" and "value" variables we should have a look at the structure of the transaction we are trying to code.

![structure](/assets/structure.png)

Each of the functions we need to write are in the white boxes, so far we have done the first. Next we need to make an allowance for the seller to change their mind and get their deposit back from the contract:

![abort](/assets/abort.png)

you will notice the caution sign next to the seller.send(this.balance) line. Solidity (like many common programming languages) is under constant development. This means that we may not be able to use this syntax or do things like this for much longer, but for now it is working.

**abort()** will simply send the balance of the contract back to the seller.

Next, we need to add the function where the buyer confirms the purchase, this means that simply, if the buyer places enough Ether in the contract, their address is placed in the "buyer" variable:

![confirmpurchase](/assets/confirmpurchase.png)

When the person buying this wants to confirm the purchase, they will run this function by selecting it in the wallet and adding a value, if the value is correct, then they will be the "buyer", if the value is not correct, the function cannot be run (it is "thrown").

Next, we make a function where the buyer has paid, but the seller cannot perform the sale, this will return the parties to roughly the pre-transaction situation:

![refund](/assets/refund.png)

[I say roughly the pre-transaction situation because although Ethereum transactions do not have intermediaries, there is still a (small) transaction cost imposed by the network (called "gas") for changing the state variables in a contract. In this case, the seller will get what they paid (2x value) and the buyer will get the balance (roughly 2x the value)].

Finally, we write a function that the buyer will run once they take delivery of the item. This will send the purchase price and the security deposit to the seller, and the the buyer's security deposit back the buyer, it is very similar to **refund()** except for the value sent back to the buyer:

![confirmreceived](/assets/confirmreceived.png)

Lastly we will add a "fallback" function, which will reject any messages that are not associated with any of the functions we have just defined. This is not an issue if all if we can be assured that both parties will be interacting with the contract through the Ethereum wallet, because the wallet interface does not allow it. But as we can interact with the Ethereum blockchain through the command-line, we cannot be sure that people will input the correct function name. You can have one fallback function and it cannot have a name.

![throw](/assets/throw.png)

Now we have a working contract.... sort of.

![entireone](/assets/entireone.png)

### Some problems...

Our contract works, if both parties are pure of heart. Although it has some big drawbacks that you might have noticed, add the contract to the Ethereum wallet, buy going to DEPOY NEW CONTRACT, select the account you want to use, send a value of 2 ether, remove the text that is in the solidity contract source code box and cut and past what you have been working on in browser-solidity:

![deployone](/assets/deployone.png)

Scroll down and deploy the contract. Wait until it uploads to the blockchain and then interact with it (by creating another account in your wallet, watching the contract and running functions, or trying to run other functions with the same account you used to deploy the contract).

***

## Problem - The wrong people can run the wrong functions.

You will find that a seller (or anyone) can run **confirmReceival()** and a buyer (or anyone) can run **refund()**. Less of a worry is that anyone can run **abort()**, but that is more of an nuisance than an opportunity to take swindle a counter-party.

We change this by writing modifiers and inserting them into our functions. Let's make one so that only the seller can run **abort()** and **refund()**

**_Solution: adding modifiers_**

Below the closing } bracket under **Purchase()**, write:

![modifier1](/assets/modifier1.png)

Then at the top of **abort()** and **refund()**, in between the "function" line and the opening curly bracket, simply write "onlySeller"

![modifier2](/assets/modifier2.png)

This is a _conditional_ (we included one in **confirmPurchase()** which threw out any attempt to run that function without the correct msg.value.

Do the same for the buyer:

![modifierbuyer](/assets/modifierbuyer.png)

And add it to **confirmReceived()** in the same way you added the onlySeller modifier to **abort()** and **refund()**.

Deploy your new contract in the same way that you did before, and no, you cannot go back to the contract we uploaded before and edit, once on the blockchain it is on there for good.

You will see that you cannot run certain functions without using the correct address. So the buyer cannot run **confirmReceival()** and so on.

***

## Problem: Functions are allowed to run at the wrong time

There is another problem, even though the right functions can only be run by the right people, functions can still be run at the wrong time.

1. only the seller can run **abort()**, but they should not be able to do this after the buyer has entered the purchase price, as **abort()** will send the contract balance back to the seller (including the buyer's deposit).
2. **confirmPurchase()** can be run at any time, this is a problem if a buyer pays into the contract, then another person also pays into the contract, meaning that their place is usurped in the contract. This would disadvantage the original "buyer" and advantage the seller as the "balance" would contain more than was intended - **confirmPurchase()** must only be run once
3. Similarly, **confirmReceived()** and refund() can be run at any time, this is more of a housekeeping issue, but it will generate an error, so we need to make sure that they can only be run after **confirmPurchase()**.

We can achieve this though another modifier, and we will have to add another, new type of variable, an enum.

**_Solution: Enum and modifiers_**

**WARNING**: this part could get confusing. If you get lost, just follow the instructions and have a look at what happens and it should make sense

First, lets map out our transaction through time. It goes through three stages, Created, Locked and Inactive:

![state](/assets/state.png)

_Created_ is where we should only be able to run **abort()**, and **confirmPurchase()**, after that point it should be _Locked_ and no other users of the Ethereum network can change the values of the seller and buyer variables. _Inactive_ is a bit unnecesary, but it just highlights that the transaction is over.

We will create the enum where we put our other variables (note that we put in two lines here):

![enumvariables](/assets/enumvariables.png)

Here we have a enum State (capital S), that is linked to a variable (lower case s) state

Essentially our enum will cycle through each of the transactions states, it will act like a gate, out enum can be set to the following - **State.Created**, **State.Locked**, **State.Inactive**. We will see the variable displayed in our wallet as either 0, 1, 2 depending on which state the contract is in.

First, the state of the contract depends on what functions have been run, the enum will exist when the contract is created, and it will be set to position 0, which is **State.Created**. We then need to write code to set it to another value in response to a function being run:

1. If **abort()**, **confirmRecieved()** or **refund()** is run: **state = State.Inactive**
2. If **confirmPurchase()** is run: **state = State.Locked**

So put those variable definitions in each of those functions like so, this will change the value of the enum to the desired state:

![enumset](/assets/enumset.png)

So, now we need to make a modifier that sits in a function that will check to see what state the contract is in. It will check the current state against the state that we want the function to be used in. If the contract is in the correct state the function can proceed, otherwise we will throw it out.

![enummodifier](/assets/enummodifier.png)

Now at the top of each function we run our inState() modifier, and we specify what state the contract must be in to allow the function to run. So, as **abort()** should only be run when the contract is in **State.Created**, we write, **inState(State.Created)**, and this will go just below the onlySeller modifier we inserted earlier (what is important is that it is in the space between the "function" line and the opening curly bracket).

![enumgate](/assets/enumgate.png)

1. **abort()** and **confirmPurchase()** : **inState(State.Created)**
2. **confirmReceived()** and **refund()** : **inState(State.Locked)**

## done

Deploy your new contract. It should be ready to roll and safe to use with the most crooked of counterparties (unless of couse, they don't care about the security deposit mechanism for establishing trust, but that is a topic for another post - _soon_).


_if you have any questions or comments please contact me at_ adyball@swin.edu.au
