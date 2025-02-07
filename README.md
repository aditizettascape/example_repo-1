
## GridGain Vector Store

This component implements a Vector Store using GridGain with CSV ingestion and search capabilities.

### Inputs

| Name              | Type          | Description                                                                   |
|-------------------|---------------|----------------------------------------------------------------               |
| cache_name        | String        | The name of the cache within GridGain where vectors will be stored. Required. |
| host              | String        | GridGain server host address. Required.                                       |
| port              | Integer       | GridGain server port number. Required.                                        |
| score_threshold   | Float         | Minimum similarity score threshold for search results. Required. Default value: 0.6|
| csv_file          | File          | Optional CSV file for data ingestion                                          |
| embedding         | Embeddings    | Embedding model to use for vector creation                                    |
| search_query      | String        | Query string for similarity search                                            |
| number_of_results | Integer       | Number of results to return in similarity search. Default value: 4            |

### Outputs

| Name           | Type               | Description                                                |
|----------------|--------------------|------------------------------------------------------------|
| vector_store   | GridGainVectorStore| Built GridGain vector store instance                       |
| search_results | List[Data]         | Results of the similarity search as a list of Data objects |

**Important Note**: Unlike other vector store providers that support direct data ingestion through the `ingest_data` parameter, GridGain currently only supports data ingestion through CSV file upload. The CSV file must contain the following columns:
- "id": Unique identifier for the document
- "url": Document URL
- "title": Document title
- "text": Document content

The component will automatically process the CSV file and create document objects with appropriate metadata for storage in GridGain.



## GridGainChatMemory Component

This component creates a chat message history using GridGain, enabling storage and retrieval of chat messages using GridGain's distributed caching capabilities.

### Inputs

| Name         | Type          | Description                                                           |
|--------------|---------------|-----------------------------------------------------------------------|
| host         | String        | GridGain server host address. Required. Default value: "localhost".        |
| port         | String        | GridGain server port number. Required. Default value: "10800".            |
| cache_name   | String        | Name of the GridGain cache that is used to store messages. Required. Default value: "langchain_message_store" |
| session_id   | MessageText   | Chat session ID. Uses current session ID if not provided.             |
| client_type  | String        | Type of client to use. Required. Default value: "pygridgain".                     |


### Outputs

| Name            | Type                    | Description                                               |
|-----------------|-------------------------|-----------------------------------------------------------|
| message_history | BaseChatMessageHistory  | An instance of GridGainChatMessageHistory for the session. |