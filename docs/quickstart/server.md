# pg-mcp-server

## Installation

### Prerequisites

- Python 3.13+
- PostgreSQL database(s)

### Using Docker

```bash
# Clone the repository
git clone https://github.com/stuzero/pg-mcp-server.git
cd pg-mcp-server

# Build and run with Docker Compose
docker-compose up -d
```

### Manual Installation

```bash
# Clone the repository
git clone https://github.com/stuzero/pg-mcp-server.git
cd pg-mcp-server

# Install dependencies and create a virtual environment ( .venv )
uv sync

# Activate the virtual environment
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Run the server
python -m server.app
```

## Testing the Server

The repository includes test scripts to verify server functionality:

```bash
# Basic server functionality test
python test.py "postgresql://username:password@hostname:port/database"

# Claude-powered natural language to SQL conversion
python example-clients/claude_cli.py "Show me the top 5 customers by total sales"
```

The `claude_cli.py` script requires environment variables:

```
# .env file
DATABASE_URL=postgresql://username:password@hostname:port/database
ANTHROPIC_API_KEY=your-anthropic-api-key
PG_MCP_URL=http://localhost:8000/sse
```

## Using with Claude Desktop
Add the following to your `claude_desktop_config.json` file
```json
{
  "mcpServers": {
    "pg-mcp-server": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "http://localhost:8000/sse"
      ]
    }
  }
}
```

## Using with AI Agents

Example prompt for use with agents:

```
Use the PostgreSQL MCP server to analyze the database. 
Available tools:
- connect: Register a database connection string and get a connection ID
- disconnect: Close a database connection
- pg_query: Execute SQL queries using a connection ID
- pg_explain: Get query execution plans

You can explore schema resources via:
pgmcp://{conn_id}/schemas
pgmcp://{conn_id}/schemas/{schema}/tables
pgmcp://{conn_id}/schemas/{schema}/tables/{table}/columns
```