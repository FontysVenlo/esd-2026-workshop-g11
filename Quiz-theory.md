# Quiz 
### To be used after the theory of the presentation is done (in Quizziz)

1. What core problem does MCP solve?
- Storing chat history between sessions
- LLMs being too slow to answer questions
- *Every AI app needing its own custom integration for every external system (correct)*
- Training models on private company data

**Why?** -> Without a standard, M apps and N systems need MxN custom integrations. MCP lets each side implement the protocol once.

2. With 3 AI apps and 3 external systems, how many implementations are needed with MCP compared with No standard?
- 6 with MCP vs 12 without
- *6 with MCP vs 9 without (correct)*
- 3 with MCP vs 9 without
- 9 with MCP vs 6 without

**Why?** -> Without the standard: 3x3 = 9 custom integrations. With MCP: 3 clients + 3 servers = 6 implementations of one protocol
  
3. Which company originally created an open-sourced MCP, and when?
- OpenAI, March 2025
- Google, May 2025
- Microsoft, December 2025
- *Anthropic, November 2024 (correct)*

**Why?** -> OpenAI adopted MCP in March 2025 and it was donated to the Linux Foundation's Agentic AI Foundation in December 2025

4. In MCP architecture, which component creates one dedicated client per server?
- Authorization server
- Server
- *Host (correct)*
- LLM

**Why?** -> The host is the AI app that the user talks to (in this case VS code). It runs the LLM and creates a separate MCP client for each server, so client and server are always one-to-one.

5. Which protocol is used for the messages exchanged between MCP clients and servers?
- SOAP
- gRPC
- *JSON-RPC (correct)*
- GraphQL

**Why?** -> MCP's data layer uses JSON-RPC. The transport (in this case `stdio` or Streamable HTTP) only decides how the messages travel

6. Which MCP primitive is controlled by the model, meaning LLM decides when to call it?
- Resources
- *Tools (correct)*
- Transports
- Prompts

**Why?** -> Tools are model-controlled functions like `create class`. Resources are application-controlled data, and prompts are user-controlled templates, like slash commands

7. Which statement about the stdio transport is correct?
- It requires a load balancer with sticky sessions
- It is the only transport the latest spec allows
- It serves many clients and uses OAuth 2.1 tokens
- *It runs as a child process on your machine and serves one client (correct)*

**Why?** -> `stdio` runs the server as a local child process for one client, with credentials from the environment. Streamable HTTP is the only one for many clients and OAuth.

8. What was the key architectural change in the latest MCP version (July 2026 spec)?
- *MCP became stateless: protocol sessions were removed and each request carries its own version and capabilities (correct)*
- All servers must now run on stdio
- Tools are replaced by resources
- MCP switched from JSON-RPC to REST

**Why?** -> Removing sessions (the initialize handshake and Mcp-Session-Id) means any instance can answer any request, so servers can scale behind a plain load balancer or run serverless

9. In the OAuth 2.1 setup, what role does the MCP server play?
- Authorization server that logs users in
- *Resource server that validates tokens (correct)*
- OAuth client
- Identity provider

**Why?** -> The MCP server only validates tokens. An external authorization server (Keycloak) handles login, and VS Code acts as the OAuth client

10. Which of these is a known con of MCP mentioned in the slides?
- It's closed-source and proprietary
- It only works with one AI model
- *Many tool definitions consume tokens and can hurt performance and cost (correct)*
- It cannot discover available tools

**Why?** -> The correct answer is Many tool definitions consume tokens and can hurt performance and cost.Large numbers of definitions use up tokens, raising costs and lowering performance on complex tasks. Other cons include prompt injection through tool descriptions and untrusted server output

11. In May 2025, GitHub MCP server was exploit. How was the agent tricked into leaking private data?
- The stdio connection was intercepted
- A bug in the server's code allowed remote code execution
- The developer's OAuth token was stolen
- *Instructions were hidden in an issue in a public repo, which the agent read (correct)*

**Why?** -> Hidden instructions in a public issue (prompt injection) led the agent to read private repos and publish their contents. It was not a code bug: the design of tools plus LLM made it possible

12. How does Google's A2A (Agent2Agent) relate to MCP?
- A direct replacement for MCP
- The older name for MCP
- It only works for code execution in sandboxes
- *A2A connects agents to agents, while MCP connects an agent tools and data (correct)*

**Why?** -> A2A is often seen as a competitor but is complementary: agent ↔ agent communication versus agent ↔ tool communication
