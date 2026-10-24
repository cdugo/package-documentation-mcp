# 📚 DocsFetcher MCP Server

[![LightNow capabilities](https://lightnow.ai/badge/io.github.cdugo/package-documentation-mcp)](https://lightnow.ai/servers/io.github.cdugo/package-documentation-mcp)
[![npm version](https://img.shields.io/npm/v/@cdugo/docs-fetcher-mcp.svg)](https://www.npmjs.com/package/@cdugo/docs-fetcher-mcp)
[![npm downloads](https://img.shields.io/npm/dm/@cdugo/docs-fetcher-mcp.svg)](https://www.npmjs.com/package/@cdugo/docs-fetcher-mcp)

An MCP server that fetches package documentation from multiple language ecosystems for LLMs like Claude without requiring API keys.

<a href="https://glama.ai/mcp/servers/8yfwtryuc5">
  <img width="380" height="200" src="https://glama.ai/mcp/servers/8yfwtryuc5/badge" alt="DocsFetcher Server MCP server" />
</a>

## ✨ Features

- 🌐 Supports multiple programming languages (JavaScript, Python, Java, .NET, Ruby, PHP, Rust, Go, Swift)
- 📦 Fetches documentation for packages by name or URL
- 🔍 Crawls documentation sites to extract comprehensive information
- 📄 Extracts README, API docs, code examples, and repository info
- 🧠 Provides structured data for LLM summarization
- 💬 Includes specialized prompts for documentation analysis
- 🔑 **No API key required** - works natively with Claude Desktop and Cursor IDE

## 🚀 Installation

### Claude Desktop

1. Open Claude Desktop → Settings → Developer
2. Click "Edit Config" and add:

```json
{
  "mcpServers": {
    "docsFetcher": {
      "command": "npx",
      "args": [
        "-y",
        "@smithery/cli@latest",
        "run",
        "@cdugo/mcp-get-docs",
        "--config",
        "'{}'"
      ]
    }
  }
}
```

### Cursor IDE Configuration

1.  Open Cursor IDE → Settings → MCP -> Add New MCP Servier
2.  Add:

```json
    Name: docsFetcher
    Command: npx -y @smithery/cli@latest run @cdugo/mcp-get-docs --config "{}"
```

#### Prerequisites

- 📋 Node.js 18 or later

## 🏃‍♂️ Running Locally

```bash
git clone https://github.com/cdugo/package-documentation-mcp
cd package-documentation-mcp
npm install
npm run build
```

Once installed, you can run the server locally with:

```bash
# From the project root directory
npm start
```

For development with auto-restart on file changes:

```bash
npm run dev
```

The server will start on the default port (usually 3000). You should see output like:

```
🚀 DocsFetcher MCP Server running!
📋 Ready to fetch documentation
```

To specify a custom port:

```bash
PORT=8080 npm start
```

## 🛠️ Available Tools

1. **fetch-url-docs**: 🔗 Fetch docs from a specific URL
2. **fetch-package-docs**: 📦 Fetch docs for a package with optional language specification
3. **fetch-library-docs**: 🧠 Smart tool that works with either package name or URL
4. **fetch-multilingual-docs**: 🌍 Fetch docs for a package across multiple language ecosystems

## 📝 Available Prompts

1. **summarize-library-docs**: 📚 Create a comprehensive library summary
2. **explain-dependency-error**: 🐛 Generate dependency error explanations

## 💡 Example Queries

### Basic Library Information

- "What is Express.js and how do I use it?"
- "Tell me about the React library"
- "How do I use requests in Python?"

### Multi-language Support

- "Show me documentation for lodash in JavaScript"
- "Compare pandas in Python and data.table in R"

### Using Tools

- "@fetch-package-docs with packageName='express' and language='javascript'"
- "@fetch-package-docs with packageName='requests' and language='python'"
- "@fetch-multilingual-docs with packageName='http' and languages=['javascript', 'python', 'rust']"

### Using Prompts

- "@summarize-library-docs with libraryName='express'"
- "@explain-dependency-error with packageName='dotenv'"

## ❓ Troubleshooting

### Local Installation

- **Server not showing up**: ✅ Verify absolute path in configuration
- **Connection errors**: 🔄 Restart Claude Desktop or Cursor IDE
- **Fetch failures**: ⚠️ Some packages may have non-standard documentation
- **Language support**: 🌐 If a language isn't working, try using the package's direct URL

## 📄 License

MIT