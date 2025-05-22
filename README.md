# FastMCP Docker Image Architecture Checker

This project provides a Model Context Protocol (MCP) server that extends Amazon Q with tools to check Docker image architecture support and perform simple arithmetic operations.

## Features

- **check_image**: Checks if a Docker image supports specific architectures (amd64, arm64)
- **add**: Simple tool to add two numbers (demonstration of basic functionality)

## Requirements

- Python 3.10+
- Amazon Q CLI
- `fastmcp` Python package
- `requests` Python package

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/pareenaverma/fastmcp-docker-checker.git
   cd fastmcp-docker-checker
   ```

2. Create and activate a virtual environment:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. Install the required packages:
   ```bash
   pip install fastmcp requests
   ```

4. Configure Amazon Q to use this MCP server by adding the following to `~/.aws/amazonq/mcp.json`:
   ```json
   {
     "mcpServers": {
       "demoserver": {
         "command": "/path/to/your/venv/bin/python3",
         "args": ["/path/to/your/server.py"],
         "env": {},
         "timeout": 60000
       }
     }
   }
   ```

## Usage

1. Start Amazon Q CLI:
   ```bash
   q chat
   ```

2. View available tools by typing:
   ```
   /tools
   ```
This will display all available tools, including your custom MCP tools from the demoserver.

3. Use the tools in your conversation:

   To check Docker image architecture support:
   ```
   check_image nginx
   ```

   To add two numbers:
   ```
   add 5 3
   ```

## How It Works

The server uses the FastMCP framework to create a Model Context Protocol server that Amazon Q can communicate with. When you make a request to check an image, the server:

1. Parses the image name and tag
2. Gets an authentication token from Docker Hub
3. Fetches the manifest for the specified image
4. Analyzes the manifest to determine supported architectures
5. Returns a response indicating whether the image supports the target architectures (amd64, arm64)

## Project Structure

- `server.py`: The main MCP server implementation
- `requirements.txt`: Python dependencies
- `mcp.json.example`: Example configuration for Amazon Q


## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
