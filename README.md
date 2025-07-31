# DeepSeek Terminal Chat with MCP Integration

A Flask web application that integrates DeepSeek AI with terminal command execution capabilities and Model Context Protocol (MCP) endpoints.

![Image](https://github.com/user-attachments/assets/08bcd194-35e8-4143-b4e2-cae22834b7ca)

## Features

- **AI-Powered Terminal Assistance**: Chat interface where DeepSeek AI can execute shell commands when needed
- **Command Execution**: Safe execution of terminal commands via pexpect
- **Real-time Output Capture**: Monitors and captures command output
- **Process Monitoring**: Tracks CPU usage to detect command completion
- **MCP Protocol Support**: Provides tools via Model Context Protocol
- **Simple Web Interface**: Clean chat UI with message history

## How It Works

1. **User Interaction**:
   - User sends message via web interface
   - Message is sent to `/chat` endpoint

2. **AI Processing**:
   - DeepSeek API processes the conversation history
   - AI may include `CMD:` directives in its response

3. **Command Execution**:
   - System detects `CMD:` lines in AI response
   - Commands are executed in a secure shell session
   - Output is captured and cleaned

4. **Response Generation**:
   - Command outputs are inserted into the response
   - Final response is sent back to user
   - Conversation history is updated

5. **Technical Details**:
   - Uses pexpect for terminal interaction
   - Monitors CPU usage to detect command completion
   - ANSI escape codes and special characters are filtered
   - Includes 20-second timeout for command safety

## Installation

1. Clone this repository
2. Ensure Python 3.8+ is installed
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Create `.env` file with your DeepSeek API key:
   ```
   DEEPSEEK_API_KEY=your_api_key_here
   ```

## Usage

1. Start the server:
   ```bash
   python server.py
   ```
2. Access the web interface at: [http://localhost:5000](http://localhost:5000)
3. Ask questions in the chat interface. The AI may execute commands when needed.

Example queries:
- "What files are in this directory?"
- "Check the Python version"
- "Show running processes"

## Architecture Overview

```
.
├── server.py            # Main Flask application
├── static/
│   └── chat.html        # Web chat interface
├── tools/               # Command execution utilities
│   ├── command_executor.py  # Handles command execution
│   ├── process_tracker.py   # Monitors process activity
│   ├── tty_output_reader.py # Captures terminal output
│   ├── send_control_character.py # Sends control chars
│   └── utils.py         # Utility functions
├── requirements.txt     # Python dependencies
└── .env                 # Configuration
```

## MCP Tools

The server provides these MCP-compatible tools:
- `write_to_terminal`: Execute shell commands
- `read_terminal_output`: Read terminal output
- `send_control_character`: Send control sequences (Ctrl-C, etc.)

## License

MIT License - See [LICENSE](LICENSE) file for details.
