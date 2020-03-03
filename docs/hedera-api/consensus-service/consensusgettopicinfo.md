# ConsensusGetTopicInfo

## ConsensusGetTopicInfoQuery

| Field | Type | Description |
| :--- | :--- | :--- |
| header | ​[QueryHeader](../miscellaneous/queryheader.md)​ | Standard info sent from client to node, including the signed payment, and what kind of response is requested \(cost, state proof, both, or neither\). |
| topicID | ​[TopicID](../basic-types/topicid.md)​ | Topic to retrieve info about \(the parameters and running state of\). |

‌

## ConsensusGetTopicInfoResponse <a id="consensusgettopicinforesponse"></a>

‌

Retrieve the parameters of and state of a consensus topic.

| Field | Type | Description |
| :--- | :--- | :--- |
| header | ​[ResponseHeader](../miscellaneous/responseheader.md#responseheader)​ | Standard response from node to client, including the requested fields: cost, or state proof, or both, or neither. |
| topicID | ​[TopicID](../basic-types/topicid.md)​ | Topic identifier. |
| topicInfo | ​[ConsensusTopicInfo](consensustopicinfo.md)​ | Current state of the topic |

​  


