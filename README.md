# Gold Price Research Assistant with Live Web Search

An AI research agent built in n8n. It takes a question about gold prices, breaks it into sub-questions (city and karat), searches the live web for each one, and returns a table with the date, unit and source link for every price.

**Example question:** Compare today's 22K and 24K gold price per 10 grams in Hyderabad, Chennai and Mumbai.

## Tools Used
- n8n (workflow automation)
- Google Gemini Chat Model (Flash, temperature 0.2)
- Tavily Search (web search tool)
- Simple Memory (conversation context)
- Edit Fields (saves the final answer)

## Workflow
Manual Trigger -> AI Agent -> Edit Fields

The AI Agent has three connected sub-nodes: Google Gemini Chat Model, Simple Memory and Search in Tavily.

## How It Works
1. The question enters through the trigger with today's date added in the prompt.
2. The agent splits it into city and karat sub-questions.
3. Tavily searches the web for each sub-question (time range: day, topic: news, 5 results).
4. The agent compares the results and checks the dates.
5. Gemini writes a table with prices and source links.

## Key Settings
- Today's date added with `{{ $now.format('dd MMM yyyy') }}`
- System Message: must call Tavily, use only recent results, show a source URL for every price
- Max Iterations set to stop endless search loops
- Memory session key changed for each new test

## Files in This Repository
| File | Description |
| --- | --- |
| `gold-price-research-assistant.json` | Exported n8n workflow |
| `Gold_Research_Assistant-1.docx` | Project document with diagrams |
| `Deep_Research_Assistant_Gold.pptx` | Project presentation |
| `README.md` | This file |

## How to Use
1. Open n8n and create a new workflow.
2. Import the JSON file (menu, Import from file).
3. Add your own Google Gemini and Tavily API credentials.
4. Click **Execute workflow** and read the `answer` field.

## Sample Result (1 October 2026)
| City | 22K (10 g) | 24K (10 g) | Source |
| --- | --- | --- | --- |
| Hyderabad | Rs 1,37,097 | Rs 1,49,560 | LiveMint |
| Chennai | Rs 1,37,216 | Rs 1,49,690 | LiveMint |

Prices change during the day. Verify with a jeweller or bank site before buying.

## Note
No API keys are stored in this repository. Add your own credentials in n8n after importing.
