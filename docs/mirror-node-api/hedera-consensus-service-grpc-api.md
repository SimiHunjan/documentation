# Hedera Consensus Service GRPC API

Clients can connect to the Hedera Consensus Service mirror node to subscribe to a Hedera topic and receive messages for the topic it is has subscribed to

{% hint style="danger" %}
**LIMITED AVAILABILITY**   
Hedera is offering access to its mirror node through the Hedera Consensus Service \(HCS\) early access program. You must be using Hedera Consensus Service to participate. Register for this program [here](https://learn.hedera.com/HCS-EAP/).
{% endhint %}

## Build a Mirror Node Client

| Constructor | Description |
| :--- | :--- |
| `ConsensusClient(<endpoint>)` | Initializes the ConsensusClient object |

```java
final ConsensusClient consensusClient = new ConsensusClient(MIRROR_NODE_ADDRESS);
```

### Set error handler

| Method | Type | Description |
| :--- | :--- | :--- |
| `setErrorHandler(<errorHandler)` | Consumer&lt;Throwable&gt; | Set a global error handler for all streams. |

```java
final ConsensusClient consensusClient = new ConsensusClient(MIRROR_NODE_ADDRESS)
.setErrorHandler(e -> System.out.println("error in consensus client: " + e));
```

### Subscribe to a topic

<table>
  <thead>
    <tr>
      <th style="text-align:left">Method</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>subscribe(&lt;topicId, listener&gt;)</code>
      </td>
      <td style="text-align:left">TopicID, Consumer&lt;throwable&gt;)</td>
      <td style="text-align:left">Subscribe to a Consensus Service topic; the callback will receive messages
        with consensus timestamps starting now and continuing indefinitely into
        the future.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>subscribe(&lt;topicId, consensusStartTime, listener&gt;)</code>
      </td>
      <td style="text-align:left">TopicId, Instant, Consumer&lt;ConsensusMessage&gt;</td>
      <td style="text-align:left">
        <p>Subscribe to a Consensus Service topic; the callback will receive messages</p>
        <p>with consensus timestamps falling on or after the given Instant</p>
        <p>(which may be in the past or future) and continuing indefinitely afterwards.</p>
        <p></p>
        <p><code>consensusStartTime</code>: the lower bound for timestamps (inclusive),
          may be in the past or future.</p>
      </td>
    </tr>
  </tbody>
</table>```java
consensusClient.subscribe(topicId, message -> {
    System.out.println(message.consensusTimestamp + " received topic message: " + message.getMessageString());
});
```

### Get messages from a topic from a specific Instant

<table>
  <thead>
    <tr>
      <th style="text-align:left">Method</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p><code>getMessasges(&lt;topic, startTime, endTime&gt;)</code>
        </p>
        <p></p>
        <p></p>
      </td>
      <td style="text-align:left">TopicId, Instant, Instant</td>
      <td style="text-align:left">
        <p>Get a blocking iterator which returns messages for the given topic with
          consensus timestamps</p>
        <p>between two Instants.</p>
        <p><code>startTime</code>: the lower bound for timestamps (inclusive), may
          be in the past or future.</p>
        <p><code>endTime</code> : the upper bound for timestamps (exclusive), may
          also be in the past or future.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>getMessageUntil</code>
        </p>
        <p><code>(&lt;topic, endTime&gt;)</code>
        </p>
        <p></p>
        <p></p>
      </td>
      <td style="text-align:left">TopicId, Instant</td>
      <td style="text-align:left">
        <p>Get a blocking iterator which returns messages for the given topic with
          consensus timestamps starting now and continuing until the given Instant</p>
        <p><code>endTime</code> : the upper bound for timestamps (exclusive), may
          be in the past or future.</p>
      </td>
    </tr>
  </tbody>
</table>