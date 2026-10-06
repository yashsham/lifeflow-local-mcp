# 🏠 LifeFlow Local FastMCP Servers (Privacy-First On-Device Intelligence)

[![FastMCP](https://img.shields.io/badge/FastMCP-v4.0.11-blue.svg)](https://github.com/jlowin/fastmcp)
[![Python](https://img.shields.io/badge/Python-3.12%2B-brightgreen.svg)](https://python.org)
[![Protocol](https://img.shields.io/badge/Protocol-MCP%20stdio-green.svg)](https://modelcontextprotocol.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**LifeFlow Local MCP** is a collection of privacy-first, on-device **Model Context Protocol (MCP)** servers built with **FastMCP** communicating strictly over the standard **`stdio`** transport.

It enables AI assistants (like **Claude Desktop** and **Cursor IDE**) to track sensitive personal finances and daily productivity routines **100% on your local disk (`data/*.json`) without leaking private data to the cloud**.

---

## 🔒 Why `stdio` Transport for Local Servers?

- **Zero Open Ports**: Unlike HTTP/SSE, `stdio` communicates via standard input/output pipes of a spawned subprocess.
- **Air-Gapped Privacy**: Your banking expenses, salary data, and daily journals never leave your workstation.
- **Operating System Sandboxing**: Operates strictly within user-permission boundaries.

---

## 🛠️ Servers & Tools Catalog

### 1. `LocalExpenseServer` (stdio)
- **Script:** `servers/local_expense.py`
- **Data Persistence:** Local JSON ledger at `data/expenses.json`

| Tool Name | Parameters | Description |
|---|---|---|
| `add_expense` | `category`, `amount`, `note`, `currency` (INR) | Records a new expense in the local ledger with auto-generated ID. |
| `get_monthly_summary` | *none* | Generates total spending, transaction count, and category breakdown. |
| `check_budget_status` | *none* | Evaluates spending against monthly budget limit (₹15,000 threshold alert). |

- **Resource:** `resource://finance/rules` — User's savings targets and financial guidelines.

---

### 2. `LocalHabitServer` (stdio)
- **Script:** `servers/local_habit.py`
- **Data Persistence:** Local JSON state at `data/habits.json`

| Tool Name | Parameters | Description |
|---|---|---|
| `log_habit` | `habit_name`, `completed` (bool) | Increments daily routine streaks (e.g., Morning Workout, Reading, Coding). |
| `get_habit_streaks` | *none* | Shows active habit streaks, weekly targets, and completion status. |
| `add_journal_entry` | `note` | Appends private daily reflection notes with timestamp. |

- **Resource:** `resource://habit/motivation` — Daily atomic habit building quote.

---

## 🔌 How to Connect to Claude Desktop or Cursor IDE

### Step 1: Clone Repository
```bash
git clone https://github.com/yashsham/lifeflow-local-mcp.git
cd lifeflow-local-mcp
pip install -r requirements.txt
```

### Step 2: Configure Claude Desktop
Open `%APPDATA%\Claude\claude_desktop_config.json` (on Windows) or `~/Library/Application Support/Claude/claude_desktop_config.json` (on macOS) and add:

```json
{
  "mcpServers": {
    "local_expense": {
      "command": "python",
      "args": ["-m", "servers.local_expense"],
      "cwd": "C:/path/to/lifeflow-local-mcp"
    },
    "local_habit": {
      "command": "python",
      "args": ["-m", "servers.local_habit"],
      "cwd": "C:/path/to/lifeflow-local-mcp"
    }
  }
}
```
*(Replace `C:/path/to/lifeflow-local-mcp` with your actual directory path).*

Now restart Claude Desktop, and you will see the tools icon (🔨) with all your local expense and habit tools ready to use!

---

## 🧪 Testing Standalone from Terminal

You can test either server using the FastMCP CLI inspector:

```bash
# Test Expense Server tools
fastmcp inspect servers/local_expense.py

# Test Habit Server tools
fastmcp inspect servers/local_habit.py
```

---

## 🔗 Related Ecosystem Projects

- 🌐 **[lifeflow-remote-mcp](https://github.com/yashsham/lifeflow-remote-mcp)**: Standalone cloud-deployable FastMCP servers for live currency, crypto, and weather telemetry via SSE.
- ⚡ **[lifeflow-mcp](https://github.com/yashsham/lifeflow-mcp)**: Full-stack master platform with Custom MCP Client, NVIDIA NIM AI Brain, and Live Protocol Inspector.

---

## 📄 License
Released under the [MIT License](LICENSE).
