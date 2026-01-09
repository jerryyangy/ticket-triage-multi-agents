# Ticket-triage-multi-agents
This is a project that orchestrates multiple AI agents using Microsoft Foundry Agent Service. It's to design an AI solution that assists with ticket triage. The connected agents will assess the ticket’s priority, suggest a team assignment, and determine the level of effort required to complete the ticket.


​## The background
Run a Python client app that calls multiple agents(priority, team assignment, and effort estimation), then see them collaborate on user‑provided ticket descriptions.
​
### Steps

#### Step 1:
Setup the environment
Create a Foundry project in the Azure AI portal, configure subscription, resource group, region, and (if needed) deploy a gpt‑4.1 model to the project.
​
In the Azure portal Cloud Shell (PowerShell), clone this GitHub repo, create a Python virtual environment, and install packages including azure-ai-projects and azure-ai-agents.
​
#### Step 2:
Configuration and client app
Edit a .env file to set the Foundry project endpoint and model deployment name (for example gpt-4.1).
​
The provided Python app is updated to import Azure AI Agents SDK types, read environment settings, and connect an AgentsClient to the Foundry project using DefaultAzureCredential.
​
#### Step 3:
Defining the agents and orchestration
Three specialized agents are created:

Priority agent: classifies tickets as High/Medium/Low with a brief explanation.
​

Team agent: assigns tickets to one of Frontend, Backend, Infrastructure, or Marketing with a short rationale.
​

Effort agent: estimates effort as Small/Medium/Large with justification.
​

Each of these is wrapped as a ConnectedAgentTool, and a primary “triage” agent is created that uses those tools to determine priority, team, and effort for a given ticket.
​
#### Step 4:
Running, interaction, and cleanup
At runtime, the script creates a thread, prompts the user for a support problem, sends it to the triage agent, then runs the thread so the triage agent can call the connected agents.
​

The app prints out the user message and an aggregated triage response (priority, assigned team, and effort), then deletes all agents and instructs you delete the Azure resource group afterward to avoid costs.
​
