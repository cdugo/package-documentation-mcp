# DocsFetcher MCP Server

[![smithery badge](https://smithery.ai/badge/@cdugo/mcp-get-docs)](https://smithery.ai/server/@cdugo/mcp-get-docs)

An MCP server that fetches npm package documentation and provides it in a format suitable for LLMs like Claude. This server follows standard MCP patterns by handling the data fetching, while providing guidance for the LLM client (Claude Desktop or Cursor IDE) on how to best summarize and present the information.

## Features

- Automatically fetches documentation for npm packages
- Works with both package names and documentation URLs
- Extracts README, API descriptions, and examples
- Retrieves GitHub repository information when available
- Provides structured data for LLM summarization
- Includes specialized prompts for summarization and dependency error analysis
- **No API key required** - designed to work natively with Claude Desktop and Cursor IDE

## How Client-Side Summarization Works

This server uses a best-practice MCP architecture:

1. **Server-Side Responsibility**:

   - Fetch and organize documentation content
   - Structure the raw data for optimal processing
   - Provide specialized prompts for specific scenarios

2. **Client-Side Responsibility**:
   - Process and summarize the documentation data
   - Use the included prompts for better summarization
   - Format the information for the user

The server includes two specialized prompt templates:

- `summarize-library-docs`: Provides a focused summary of a library
- `explain-dependency-error`: Specifically addresses dependency errors

Each tool response includes instructions on how to use these prompts for better analysis.

## Installation

### Installing via Smithery

To install DocsFetcher for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@cdugo/mcp-get-docs):

```bash
npx -y @smithery/cli install @cdugo/mcp-get-docs --client claude
```

### Prerequisites

- Node.js 18 or later

### Quick Installation (Recommended)

The easiest way to install and configure the server is to use our interactive installer:

1. Clone this repository:

   ```bash
   git clone https://github.com/yourusername/docs-fetcher-mcp.git
   cd docs-fetcher-mcp
   ```

2. Run the installer script:

   ```bash
   npm run install-server
   ```

3. Follow the prompts to:
   - Build the project
   - Install the server globally
   - Configure for Claude Desktop and/or Cursor IDE

### Manual Installation

If you prefer to install manually:

1. Clone this repository:

   ```bash
   git clone https://github.com/yourusername/docs-fetcher-mcp.git
   cd docs-fetcher-mcp
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Build the project:
   ```bash
   npm run build
   ```

## Usage with Claude Desktop

1. Open Claude Desktop and navigate to the menu (top-left on macOS)
2. Select "Settings..." and then click on "Developer" in the left sidebar
3. Click "Edit Config" to open the configuration file
4. Add the DocsFetcher MCP server to your config file:

```json
{
  "mcpServers": {
    "docsFetcher": {
      "command": "node",
      "args": ["/ABSOLUTE/PATH/TO/docs-fetcher-mcp/build/index.js"]
    }
  }
}
```

5. Save the file and restart Claude Desktop
6. You should now see the MCP tools available when you click on the hammer icon in the chat interface

## Usage with Cursor IDE

1. Open Cursor IDE
2. Create or edit the Cursor configuration file:

   - On macOS/Linux: `~/.cursor/cursor_config.json`
   - On Windows: `%APPDATA%\Cursor\cursor_config.json`

3. Add the DocsFetcher MCP server to your config file:

```json
{
  "mcpServers": {
    "docsFetcher": {
      "command": "node",
      "args": ["/ABSOLUTE/PATH/TO/docs-fetcher-mcp/build/index.js"]
    }
  }
}
```

4. Save the file and restart Cursor IDE
5. The MCP server tools will now be available to the AI assistant in Cursor

## Available Tools

The server exposes three main tools:

1. **fetch-url-docs**: Fetch documentation from a specific URL

   - Parameters:
     - `url`: The URL of the library documentation
   - Returns: Formatted documentation with prompt suggestions

2. **fetch-package-docs**: Fetch documentation for an npm package

   - Parameters:
     - `packageName`: Name of the npm package
   - Returns: Formatted documentation with prompt suggestions

3. **fetch-library-docs**: Smart tool that works with either a package name or URL
   - Parameters:
     - `library`: Package name or URL to fetch docs for
   - Returns: Formatted documentation with prompt suggestions

## Available Prompts

The server provides two specialized prompts:

1. **summarize-library-docs**: Create a comprehensive summary of a library

   - Parameters:
     - `libraryName`: Name of the library to summarize
     - `documentation`: The raw documentation content
     - `errorStatus` (optional): Error information if fetch failed

2. **explain-dependency-error**: Generate dependency error explanations
   - Parameters:
     - `packageName`: The package with the dependency error
     - `documentation`: The package documentation
     - `errorStatus` (optional): Error information if fetch failed

## Example Queries

### Basic Library Information

- "What is the Express.js framework and how do I use it?"
- "Tell me about the React library"
- "I'd like to learn about the zod validation library"

### Dependency Error Resolution

- "I'm getting an error that says 'Cannot find module 'lodash''"
- "npm ERR! Cannot find module 'dotenv'. What does this mean?"
- "How do I fix a 'module not found' error for axios?"

### Advanced Usage with Prompts

When you receive documentation, you can use the provided prompts for better summarization:

- "@summarize-library-docs with libraryName='express'"
- "@explain-dependency-error with packageName='dotenv'"

## How It Works

When you ask about a library or encounter a dependency error:

1. The MCP server analyzes your query to identify the library name or URL
2. It fetches the documentation from the npm website and associated GitHub repository
3. The structured documentation is returned with guidance on using prompts
4. Claude or Cursor's AI assistant processes the documentation and provides helpful answers
5. For better results, you can use the specialized prompts included with the server

## Architecture and Best Practices

This implementation follows the standard MCP architecture and best practices:

1. **Clean Separation of Concerns**:

   - Server handles data access and formatting
   - Client handles analysis and presentation

2. **Structured Documentation Format**:

   - Clear section headings
   - Metadata for context
   - Organized content sections
   - Content guidance for LLMs

3. **Prompt-Based Guidance**:
   - Built-in prompt templates
   - Contextual recommendations
   - Specialized use case handling

This approach:

- Eliminates the need for API keys
- Leverages the LLM capabilities already in the client
- Follows MCP best practices
- Provides targeted guidance for optimal results

## Troubleshooting

### Common Issues

- **Server not showing up**: Make sure the path in your configuration is absolute and points to the correct location
- **Connection errors**: Restart Claude Desktop or Cursor IDE after making configuration changes
- **Fetch failures**: Some packages may have limited or non-standard documentation structures that are difficult to parse
- **Prompt not working**: Ensure you're using the prompt syntax correctly with the parameters shown in the tool output

### Logs

- **Claude Desktop**: Logs can be found at `~/Library/Logs/Claude/mcp-server-docsFetcher.log`
- **Cursor IDE**: Logs can be found in the Cursor logs directory

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
