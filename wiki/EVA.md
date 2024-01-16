# EVA 2.0

## To-Do List
1. ~~Migrate code to ADO~~
2. Run ingestion of repository into a single tool
3. Apply EVA 2.0 backend improvements
4. Apply EVA 2.0 frontend improvements



## User-Chatbot Interaction Flowchart
:::mermaid
flowchart LR

subgraph Backend
    Repository
    ChatGPT
end

    Greetings --> Query
    Query --> Repository
    Query --> ChatGPT
    Repository --> Response
    ChatGPT --> Response
    Response --> Feedback
:::

## BACKEND

### Tools Available and Order of Operations
1. ~~www_search~~
2. ~~sql_search~~
3. doc_search
4. chatgpt_search
5. ~~book_search~~

Remarks:
Combine doc_search and book_search into a single tool.
Rename to knowledge base search / not include any trigger word anymore.
Trigger word only for calling ChatGPT.


### Hyperparameter Tuning
| Tool | Parameter Name | Current Value | Replacement Value | Remarks | For Testing |
|--|--|--|--|--|--|
| llm | temperature | 0.5 | 0 | Less "creative" responses = "absolute" truths | FOR TESTING |
| llm | max_tokens | 1000 | 8000 | Increase to include as much information as possible and links provided | FOR TESTING |
| Tools | name | doc_search | TBA | After combining with book_search determine name for tool | FOR TESTING |
| Tools | description | doc_search | TBA | Set for default reference when inquiry is made | FOR TESTING |

For reference:
- <u>llm</u>:
  - **deployment_name**: this is the deployment name of your Azure OpenAI model. This of course dictates the level of reasoning and the amount of tokens available for the conversation. For a production system you will need gpt-4-32k. This is the model that will give you enough reasoning power to work with agents, and enough tokens to work with detailed answers and conversation memory.
  - **temperature**: How creative you want your responses to be
  - **max_tokens**: How long you want your responses to be. It is recommended a minimum of 500
- <u>Tools</u>: To each tool you can add the following parameters to modify the defaults (set in utils.py), these are very important since they are part of the system prompt and determines what tool to use and when.
  - **name**: the name of the tool
  - **description**: when the brain agent should use this tool
- <u>DocSearchTool</u>: 
  - **k**: The top k results per index from the text search action
  - **similarity_k**: top k results combined from the vector search action
  - **reranker_th**: threshold of the semantic search reranker. Picks results that are above the threshold. Max possible score=4
- <u>BingSearchTool</u>:
  - **k**: The top k results from the bing search action
- <u>SQLDBTool</u>:
  - **k**: The top k results from the SQL search action. Adds TOP clause to the query
  
in `utils.py` you can also tune:
- <u>model_tokens_limit</u>: In this function you can edit what is the maximum allows of tokens reserve for the content. Remember that the remaining will be for the system prompt plus the answer

## FRONTEND

1. Use only MS Teams
2. Improve text upon loading MS Teams

### Prompts Adjustment Checklist

1. WELCOME_MESSAGE
2. CUSTOM_CHATBOT_PREFIX
3. CUSTOM_CHATBOT_SUFFIX
4. COMBINE_CHAT_PROMPT_TEMPLATE
5. COMBINE_CHAT_PROMPT

## Improvements
1. Data Version Control (DVC)
