
# MSSQL MCP Server

A local **Model Context Protocol (MCP) server** that connects **Claude Desktop** to your **Microsoft SQL Server** instance.

## Prerequisites

Before you begin, make sure you have the following installed or available:

1. **Node.js 18 or later**
2. **Claude Desktop**
3. Access to a working **Microsoft SQL Server** instance

## Setup Guide

Follow the steps below to set up the MSSQL MCP server locally.

## Step 1 — Create the project folder

```bash
mkdir mssql-mcp-server
cd mssql-mcp-server
```
## Project Files
Download or copy the following files into your project folder:
1. [package.json](https://github.com/ravindercitixsys/Calude-MSSQL-MCP-Server/blob/main/package.json)
2. [index.js](https://github.com/ravindercitixsys/Calude-MSSQL-MCP-Server/blob/main/index.js)

Copy both `package.json` and `index.js` into the `mssql-mcp-server` folder.

After that, update the SQL Server connection details in the index.js file.

## Step 2 — Install dependencies
```bash
npm install
```

## Step 3 — Test the server locally
```bash
node index.js
```
If everything is configured correctly, you should see:

`MSSQL MCP Server running on stdio`

## Step 4 — Register with Claude Desktop

Open your Claude Desktop configuration file.

In `Claude Desktop`, go to:

**Settings > Developer > Edit Config**

Config file locations:

- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`
- **Mac:** `~/Library/Application Support/Claude/claude_desktop_config.json`

Add the following configuration under `mcpServers`.
Update the file path to match your local folder, then save the file and restart Claude Desktop.

```json
{
  "mcpServers": {
    "mssql": {
      "command": "node",
      "args": ["C:/path/to/your/mssql-mcp-server/index.js"]
      ]
    }
  }
}
```    
## Available MCP Tools Once Connected

| Tool | What it does |
|------|--------------|
| `query` | Run `SELECT` queries, returns JSON rows |
| `execute` | Run `INSERT` / `UPDATE` / `DELETE` / DDL |
| `list_tables` | List all tables in `CXSA1CashAndCarry_QA66` |
| `describe_table` | Show columns & types for any table |
| `list_stored_procedures` | List all stored procedures |


## Troubleshooting: MCP could not connect to MS SQL

If the MCP server could not connect to Microsoft SQL Server, check the following:

- **SQL Server service** — Make sure the SQL Server service is running (`services.msc`)
- **TCP/IP enabled** — In `SQL Server Configuration Manager`, verify that TCP/IP is enabled for your SQL Server instance
- **Port 1433** — Confirm that the instance is listening on port `1433`, or use the actual configured port
- **MCP server configuration** — Verify that the server name, instance name, database, username, password, and port are correct in `index.js`
- **Firewall** — Ensure the SQL Server port is allowed through Windows Firewall or any network firewall
- **SQL authentication** — If you are using SQL login, confirm that SQL Server Authentication is enabled and the credentials are correct

## Notes

- This setup is intended for local use with Claude Desktop
- Make sure the path in the Claude Desktop config points to the correct index.js file
- Restart Claude Desktop after every config change
