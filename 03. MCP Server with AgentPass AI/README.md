# ⚡ MCP Server with AgentPass AI, VSCode Copilot & Claude

This project demonstrates how to create and run an **MCP (Model Context Protocol) Server** using  **AgentPass AI (no-code/low-code)** , and integrate it seamlessly with **VS Code Copilot** and  **Claude AI** .

Instead of writing the full MCP Server code manually, this approach leverages **AgentPass AI’s workflow editor** to create multiple tools (endpoints) visually, host them locally, and connect them directly with AI coding assistants.

---

## 🚀 Features

* 🖥️ **No-Code MCP Server Creation** – Build and host MCP servers with **AgentPass AI** workflows.
* 🔌 **Tool Integration** – Define multiple endpoints like `get_coin_gecko_coin_price`, `get_foods_by_nutrient`, etc.
* ⚙️ **VS Code Copilot + MCP Integration** – Use MCP endpoints inside your coding environment.
* 🤖 **Claude MCP Support** – Directly connect Claude with your MCP server for real-time tool execution.
* ⚡ **Agent Workflows** – Run HTTP requests, APIs, and external calls inside your MCP server.

---

## 🏗️ Architecture

1. **AgentPass AI (MCP Server Builder)**
   * Create and configure tools/endpoints visually.
   * Host the MCP server locally.
2. **VSCode + Copilot MCP Extension**
   * Add your MCP server via `mcp.json`.
   * Access server tools from inside VS Code.
3. **Claude MCP Config**
   * Configure `claude_desktop_config.json` to connect to your server.
   * Enable/disable tools dynamically.

---

## 🛠️ Setup Instructions

### 1. Create MCP Server in AgentPass AI

* Open [AgentPass AI]().
* Navigate to  **Workflows → Create New Tool** .
* Add endpoints (e.g., CoinGecko API, Food Nutrition API).
* Start the **MCP Server** locally.

📸 Example (AgentPass Workflow Editor):

---

### 2. Configure in VS Code

* Install **MCP Servers extension** in VS Code.
* Create or edit `mcp.json`:

```json
{
  "servers": {
    "Demo": {
      "command": "C:\\Program Files\\nodejs\\npx.cmd",
      "args": [
        "-y",
        "@ownid/mcp-remote@latest",
        "https://<your-server-id>.server.agentpass.ai/api/mcp"
      ]
    }
  }
}
```

📸 Example (VS Code MCP Config + Copilot Integration):

---

### 3. Connect to Claude

* Update your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "Demo": {
      "command": "C:\\Program Files\\nodejs\\npx",
      "args": [
        "-y",
        "@ownid/mcp-remote@latest",
        "https://<your-server-id>.server.agentpass.ai/api/mcp"
      ]
    }
  }
}

```

* Restart Claude Desktop → Tools should now appear.

📸 Example (Claude with MCP Tools):

---

## 🎯 Usage Example

Ask Claude or Copilot:

```pgsql
/demo what is the current value of ETH in USD?

```

➡️ MCP Server calls **CoinGecko API** via `get_coin_gecko_coin_price`.

➡️ Returns live data directly inside Claude or Copilot.

---

## 📊 Example Tools

* `get_coin_gecko_coin_price` → Fetch crypto prices from CoinGecko
* `get_foods_by_nutrient` → Search foods by nutrient from USDA API
* `search_food_nutrition_fdc` → Nutrition data lookup

---

## 🔮 Roadmap

* [ ] Add support for private API integrations (Zscaler, Versa, etc.)
* [ ] Multi-agent MCP workflows
* [ ] Deployable MCP server templates for teams

---

