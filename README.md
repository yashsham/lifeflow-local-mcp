# 🏠 LifeFlow Local FastMCP Servers (Privacy-First On-Device Intelligence)

[![FastMCP](https://img.shields.io/badge/FastMCP-v4.0.11-blue.svg)](https://github.com/jlowin/fastmcp)
[![Python](https://img.shields.io/badge/Python-3.12%2B-brightgreen.svg)](https://python.org)
[![Protocol](https://img.shields.io/badge/Protocol-MCP%20stdio-green.svg)](https://modelcontextprotocol.io)

Standalone on-device **Model Context Protocol (MCP)** servers built with **FastMCP** communicating strictly over **`stdio`**.

Designed for 100% private personal finance and habit tracking: all files stay exclusively on your local machine with zero cloud leaks.

---

## ⚡ Servers Included

### 1. `LocalExpenseServer` (stdio)
- **Path:** `servers/local_expense.py`
- **Data Location:** Local `data/expenses.json`
- **Tools**:
  - `add_expense(category, amount, note, currency)` — Record a new private expense.
  - `get_monthly_summary()` — Category-wise spending breakdown and transaction totals.
  - `check_budget_status()` — Monthly budget health check (₹15,000 threshold alert).
- **Resource**:
  - `resource://finance/rules` — User savings guidelines.

### 2. `LocalHabitServer` (stdio)
- **Path:** `servers/local_habit.py`
- **Data Location:** Local `data/habits.json`
- **Tools**:
  - `log_habit(habit_name, completed)` — Daily routine completion and streak calculator.
  - `get_habit_streaks()` — Active streaks for workout, reading, and coding.
  - `add_journal_entry(note)` — Private daily reflection notes.
- **Resource**:
  - `resource://habit/motivation` — Daily mindset quote.

---

## 🔌 How to Connect to Claude Desktop / Cursor IDE

Clone the repository:
```bash
git clone https://github.com/yashsham/lifeflow-local-mcp.git
cd lifeflow-local-mcp
pip install -r requirements.txt
```

Add this to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "local_expense": {
      "command": "python",
      "args": ["-m", "servers.local_expense"]
    },
    "local_habit": {
      "command": "python",
      "args": ["-m", "servers.local_habit"]
    }
  }
}
```

Now Claude or Cursor can manage your personal expenses and habits locally without sending private financial data to external servers!
