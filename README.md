# CoAgents Starter

This example contains a simple starter project which includes two different agents, one written in Python and one in JavaScript.

It uses Langgraph as the agentic framework configured to use LiteLLM as the model gateway to enable running a variety of models (open, local, closed, etc.)

## Running the Agent

First, install the backend dependencies:

### Python Agent

```sh
cd agent-py
poetry install
```

### JS Agent (only if the Python version isn't used)

```sh
cd agent-js
pnpm install
```

Then, create a `.env` file inside `./agent-py` or `./agent-js` by copying `.env.example` and filling out the values

```
PORT=... # the port Langgraph should run on
API_BASE=... # the base URL for the LiteLLM server
API_KEY=... # the API key for LiteLLM
MODEL=... # the LiteLLM configured model name
ORG=... # the LiteLLM configured organization
```

Then, run the demo using langgraph studio:

Python

```sh
langgraph dev
```

A browser window will open to Langgraph Studio that points to the local agent server.  

**IMPORTANT** Make sure to use Chrome, not Safari


## Running the UI

First, install the dependencies:

```sh
cd ./ui
pnpm i
```

Then start the client:

```sh
pnpm run dev
```

To change the port, modify `package.json` and update the port in the `dev` script.

If you're using the **JS** agent, uncomment the code inside the `app/api/copilotkit/route.ts`, `remoteEndpoints` action: 

```ts
// Uncomment this if you want to use LangGraph JS, make sure to 
// remove the remote action url below too.
//
// langGraphPlatformEndpoint({
//   deploymentUrl: "http://localhost:8123",
//   langsmithApiKey: process.env.LANGSMITH_API_KEY || "", // only used in LangGraph Platform deployments
//   agents: [{
//       name: 'sample_agent', 
//       description: 'A helpful LLM agent.'
//   }]
// }),
```

Make sure to comment out the other remote endpoint as this replaces it.

**Running the JS Agent:**
- Run this command to start your LangGraph server `npx @langchain/langgraph-cli dev --host localhost --port 8123`
- Run this command to connect your Copilot Cloud Tunnel to the LangGraph server `npx copilotkit@latest dev --port 8123`


## Usage

Navigate to [http://localhost:3000](http://localhost:3000).

# LangGraph Studio

Run LangGraph studio, then load the `./agent` folder into it.

Make sure to create the `.env` mentioned above first!

# Troubleshooting

A few things to try if you are running into trouble:

1. Configure the right ports in agent-py/.env for the Langgraph port and in package.json for the frontend port.
2. Use Chrome so Langgraph Studio works correctly