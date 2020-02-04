---
description: >-
  The Hedera Consensus Service (HCS) gRPC API is a public mirror node managed by
  Hedera. It offers the ability to subscribe to HCS topics and receive messages
  for the topic subscribed.
---

# Hedera Consensus Service gRPC API

{% hint style="info" %}
**HCS Mirror Node Endpoints:**  
hcs.testnet.mirrornode.hedera.com:5600   
hcs.mainnet.mirrornode.hedera.com:5600
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

