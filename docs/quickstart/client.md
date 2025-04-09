# pg-mcp-client

## Installation

### Prerequisites

- Python 3.13+
- A running [pg-mcp-server](./server.md)
- API key from one of the supported AI providers

### Using Docker

```bash
# Clone the repository
git clone https://github.com/stuzero/pg-mcp-client.git
cd pg-mcp-client

# Create a .env file with your application secret
echo "APPLICATION_SECRET=your_secure_random_string" > .env

# Build and run with Docker
docker-compose up -d
```

### Manual Installation

```bash
# Clone the repository
git clone https://github.com/stuzero/pg-mcp-client.git
cd pg-mcp-client

# Install dependencies and create a virtual environment ( .venv )
uv sync

# Activate the virtual environment
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Create a .env file with your application secret
echo "APPLICATION_SECRET=your_secure_random_string" > .env

# Run the application
python -m client.app
```

## Configuration

1. Access the web interface at http://localhost:8080
2. Navigate to the Settings page and configure:
   - **LLM Provider**: Select from Anthropic (Claude), Gemini, or OpenAI
   - **LLM API Key**: Your API key for the selected provider
   - **PG-MCP Server URL**: The URL of your PG-MCP server's SSE endpoint (e.g., http://localhost:8000/sse)
   - **Database URL**: PostgreSQL connection string for the target database

## Usage

1. After configuring settings, go to the Query page
2. Enter your question in natural language (e.g., "Show me the top 10 customers by revenue")
3. Click "Execute Query"
4. View the generated SQL and query results

## Example Queries

Try these example queries to get started:

- "List all tables in the database"
- "Show me the first 5 rows from the customers table"
- "What were the total sales by month in 2023?"
- "Find customers who haven't placed an order in the last 3 months"
- "What product categories have the highest profit margin?"

## Supported LLM Models

- **Anthropic**: Claude 3.7 Sonnet (recommended for best results)
- **Google**: Gemini 2.0 Flash
- **OpenAI**: GPT-4o Mini _(untested)_

For more details, visit the [pg-mcp-client GitHub repository](https://github.com/stuzero/pg-mcp-client).