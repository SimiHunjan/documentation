# Hedera Consensus Service API

Clients can connect to the Hedera Consensus Service mirror node to subscribe to a Hedera topic and receive messages for the topic it is has subscribed to

{% hint style="danger" %}
**LIMITED AVAILABILITY**   
Hedera is offering access to its mirror node through the Hedera Consensus Service \(HCS\) early access program. You must be using Hedera Consensus Service to participate. Register for this program [here](https://learn.hedera.com/l/576593/2020-01-13/7z5jb).
{% endhint %}

## Build a Mirror Node Client

| Constructor | Description |
| :--- | :--- |
| `MirrorClient(<endpoint>)` | Initializes the MirrorClient object |

```java
final MirrorClient mirrorClient = new MirrorClient(MIRROR_NODE_ADDRESS);
```

### Subscribe to a topic

| Constructor | Description |
| :--- | :--- |
| `MirrorConsensusTopicQuery()` | Initializes the MirrorConsensusTopicQuery object |

| Method | Type | Description |
| :--- | :--- | :--- |
| `setTopicId(<topicId>)` | ConsensusTopicId | ID of the topic |
| `subscribe(<mirrorClient, onNext, onError>)` | MirrorClient, Consumer&lt;MirrorConsensusTopicResponse&gt;, Consumer&lt;Throwable&gt; | Subscribe to a topic |
| `setStartTime(<startTime>)` | Instant | The time to start receiving messages from the topic |
| `setEndTime(<endTime>)` | Instant | The time to stop receiving messages from the topic |
| `setLimit(<limit>)` | long | The limit to the number of messages to receive for that topic |

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

