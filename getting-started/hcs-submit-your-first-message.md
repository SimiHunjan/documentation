# HCS: Submit your first message!

## Background

With the Hedera Consensus Service you can develop applications like stock markets, audit logs, stable coins, or new network services that require high throughput and decentralized trust. This is made possible by having direct access to the native speed, security, and fair ordering guarantees of the hashgraph consensus algorithm, with the full trust of the Hedera ledger.

## Components of the Hedera Consensus Service/Terminology

* **Hedera client** - a Hedera client sends transactions to a Hedera network node for consensus. The corresponding transaction types for the Hedera Consensus Service include create a topic, update a topic, submit messages, delete a topic, and get the info for a topic. 
* **Hedera network node** - receives transactions from a client and submits it to the Hedera network for consensus
* **Mirror node client** - a mirror node client is used to subscribe to a topic and get messages that are in consensus order from a mirror node. 
* **Mirror node**: Mirror nodes receive information from Hedera network consensus nodes, but do not participate in consensus themselves. You can get more information about mirror nodes [here](https://docs.hedera.com/guides/core-concepts/mirror-nodes).
* **Topic** - a topic is the subject of information you would like to send messages to and what clients would subscribe to
* **Message** - a message is the content published to the Hedera network 

   to a topic which gets placed in consensus order 

* **Subscriber** - a client that subscribes to a desired topic in order to receive the appropriate messages
* **Publisher -** publishes messages to a topic 

## HCS Flow

Create a topic by submitting a transaction from the Hedera client to a Hedera network node ➡ Mirror node client subscribes to the topic from mirror node ➡ Publish a message to a topic by submitting a transaction from the Hedera client to a Hedera network node for consensus ➡ Mirror node client receives messages published to the topic from the mirror node

## Getting Started with Hedera Consensus Service \(Testnet\)

What you will need to be successful with this tutorial:

💥 [Testnet account ID and associated private key](https://portal.hedera.com/register)  
💥 [Hedera Java SDK](https://github.com/hashgraph/hedera-sdk-java)   
💥 [Mirror node](https://learn.hedera.com/l/576593/2020-01-13/7z5jb) `host:port`    
💥 IDE of your choice

### 1. Get a testnet account

* You will need a testnet account ID and private key to use HCS. If you do not already have one, visit the Hedera [portal](https://portal.hedera.com/register) to create your profile and receive your testnet account ID. A friend already on testnet could also generously create one for you.

### 2. Get access to a mirror node

* You will need a mirror node's `host:port` information so that you can subscribe to topics and receive the associated messages. If you do not have access to a mirror node, you can fill out this [form](https://learn.hedera.com/l/576593/2020-01-13/7z5jb) and join our limited Hedera Consensus Service early access program. 

### 3. Download the hedera-java-sdk and open in your favorite IDE

* Download the hedera-java-sdk [here](https://github.com/hashgraph/hedera-sdk-java)
* Open the hedera-java-sdk in the IDE of your choice

### 4. Set-up your enviornment variables 

* Look in the root folder of the hedera-java-sdk and open the sample.env file
* Update the following:
  * `OPERATOR_ID`: Your testnet account ID goes here 
  * `OPERATOR_KEY`: Your testnet account ID private key goes here
* Add the following:
  * `MIRROR_NODE_ADDRESS:` Insert the mirror node `host:port` information here
* Rename the file from sample.env to .env
* Your environment set-up is now complete 

### 5. Create a new HCS class

* Naviagte to hedera-sdk-java/examples/src/main/java/com/hedera/hashgraph/sdk/ **examples**/
* Create a new class and title it something like HederaConsensusService

### 6. Connect to the Hedera testnet

* Here we are going to connect to the Hedera testnet and and set the operator information with your testnet account ID and private key. The operator is responsible to pay and sign for all transactions that will be generated in this tutorial. Lucikly, this is testnet and you have unlimited hbars to use in this development environment!

```java
// Grab the OPERATOR_ID and OPERATOR_KEY from the .env file
private static final AccountId OPERATOR_ID = AccountId.fromString(Objects.requireNonNull(Dotenv.load().get("OPERATOR_ID")));
private static final Ed25519PrivateKey OPERATOR_KEY = Ed25519PrivateKey.fromString(Objects.requireNonNull(Dotenv.load().get("OPERATOR_KEY")));

// Build Hedera testnet client
Client client = Client.forTestnet();

// Set the operator account ID and operator private key
client.setOperator(OPERATOR_ID, OPERATOR_KEY);
```

### 7. Connect to a Hedera mirror node

```java
// Grab the mirror node endpoint from the .env file
private static final String MIRROR_NODE_ADDRESS = Objects.requireNonNull(Dotenv.load().get("MIRROR_NODE_ADDRESS"));

// Build the mirror node client
final MirrorClient mirrorClient = new MirrorClient(MIRROR_NODE_ADDRESS);
```

### 8. Create your first topic!

* To create you first topic, we will use the CreateTopicTransaction constructor, set its properties, and submit it to the Hedera network
* You will want to grab the topic ID so later you can subscribe to that topic via the mirror node client
* Topic IDs are in the following format: `0.0.10`

```java
//Create a new topic
final TransactionId transactionId = new ConsensusTopicCreateTransaction()
   .execute(client);

//Grab the newly generated topic ID
final ConsensusTopicId topicId = transactionId.getReceipt(client).getConsensusTopicId();

System.out.println("Your topic ID is: " +topicId);
```

### 9. Subscribe to a topic

* Now we will shift our attention the mirror node client and subscribe to the topic created.
* We will acheive this by referencing the topics topic ID 
* We will also print the consensus timestamp and message to the console

```java
new MirrorConsensusTopicQuery()
    .setTopicId(topicId)
    .subscribe(mirrorClient, resp -> {
        String messageAsString = new String(resp.message, StandardCharsets.UTF_8);

        System.out.println(resp.consensusTimestamp + " received topic message: " + messageAsString);
    },
        // On gRPC error, print the stack trace
        Throwable::printStackTrace);
```

### 10. Submit a message to a topic

* Now that we have created a topic and subscribed to that topic, we are ready to submit a message using the ConsensusSubmitTransaction constructor and submit to the Hedera network
* The below example will submit message with the message as "hello, HCS!"

```java
//Submit a message to a topic
    new ConsensusMessageSubmitTransaction()
        .setTopicId(topicId)
        .setMessage("hello, HCS! ")
        .execute(client)
        .getReceipt(client);       
```

* If you have successfully followed the steps in this tutorial, you should see the following print to your console 🤩 :

`2020-01-17T09:01:03.990648Z received topic message: hello, HCS!`

Having trouble or have any comments, suggestions, or feedback?   
Connect with us on [Discord](https://discordapp.com/invite/FFb9YFX)🤓!

