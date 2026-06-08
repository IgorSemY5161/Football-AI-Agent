An AI-powered sports assistant that seamlessly switches between fetching team/club general data and individual player statistics using dynamic API routing.

 The Technical Challenge (API Limitation)
The free API used (TheSportsDB) features a player search endpoint (searchplayers.php?p=) that strictly requires a proper name to return data. It is not structured to handle queries based on generic terms, roles, or tactical positions.

Consequently, whenever a user asked role-based questions (e.g., "Who is the goalkeeper of Brazil?"), the automation would fail or return empty datasets, because the API attempted to look for an athlete whose literal name was "Goalkeeper."

 The Prompt Engineering Solution
To bypass this limitation without switching APIs or bloating the workflow with complex custom code, the business logic was handled directly within the AI Agent's Prompt Engineering (Guardrails).

Two strict instructions were injected into the model:

Intent Classification: The agent was trained to instantly differentiate whether the user provided a specific player's name or asked about a tactical position.

Instructional Fallback Message: If the user queries a position (triggering the API's limitation), the agent is instructed not to hallucinate (make up data). Instead, it immediately intercepts the flow and returns a user-friendly guidance message:

"No information found in football database. Please try searching by the player's specific name."

 The Result
The automation achieved high resilience. Instead of crashing or throwing a system error when the API returns nothing, the agent takes control of the User Experience (UX), teaching the user how to interact with the bot while keeping the entire workflow execution.

 How to Use
 
Import the workflow_football.json into your n8n instance.

Connect your OpenRouter credential to the Chat Model node.

Open the chat UI and test with:

"Tell me about Brazil team" (Triggers football_club_tool)

"Who is Neymar?" (Triggers football_player_tool)

"Who is the goalkeeper of Corinthias?" (Triggers the fallback guardrail)
