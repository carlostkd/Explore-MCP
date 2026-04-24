# Explore MCP Server 
# Using Lumo Api

<img src="explore_mcp.png" alt="mcp banner" width="800">


Connect OpenCode to the Explore API so the LLM uses your server for knowledge, research and real-time data.
## Requirements
- Node.js 18 or higher
- OpenCode installed
- An Explore API key (request one at Threema *0001337)
- Note this is not a Lumo api KEY its an api key  to connect to my server
## Files
- `explorer-mcp.js` 
 the MCP server
- `package.json` 
 Node package config
Place both files in the same directory on your machine, for example `/home/youruser/explorer-mcp/`.
## Setup
### 1. Make the script executable

```
chmod +x /home/youruser/explorer-mcp/explorer-mcp.js
```
### 2. Create OpenCode config
```
nano `~/.opencode/opencode.json` if it does not exist:
```



```
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "explorer": {
      "type": "local",
      "command": ["node", "/home/youruser/explorer-mcp/explorer-mcp.js"],
      "enabled": true,
      "environment": {
        "EXPLORER_API_URL": "https://carlostkd.ch/explore/api/explore.php",
        "CODE_API_URL": "https://carlostkd.ch/explore/api/code.php",
        "ASSISTANT_API_URL": "https://carlostkd.ch/explore/api/assistant.php",
        "EXPLORER_TOKEN": "your_token_here"
      }
    }
```



Replace `/home/youruser/explorer-mcp/explorer-mcp.js` with the full path to your file and `your_token_here` with your actual token.
Api to test will expires soon:  "2c90361af3281447387722c6dfa4ee41872c9ac474b63452f5085274ed77c6d5"


### 3. Create agent rules

`nano ~/.config/opencode/AGENTS.md`


## Tool Usage Rules
```
## Tool Usage Rules
You have three tools:
1. explore_topic 
 research, knowledge, news, weather, prices, history, science
2. code_topic 
 any programming, code generation, scripts, debugging
3. ask_lumo 
 general questions, conversation, identity questions, anything else
When message starts with "explore" 
 use explore_topic
When message starts with "code" 
 use code_topic
For everything else 
 use ask_lumo
Never answer directly without using one of these three tools.
The only exception is direct file editing operations like reading,
writing or modifying files in the current project.
```
### 4. Verify connection
```
opencode mcp list
```
You should see:

```
 explorer connected
    node /home/youruser/explorer-mcp/explorer-mcp.js
```

If it shows failed, kill any old processes and retry:

```
pkill -f explorer-mcp.js
opencode mcp list
``` 
## Usage
### Open the TUI

`opencode`


### Single command terminal mode

`opencode run "your question here"`

## Trigger words

| explore | quantum computing | explore_topic |
| -------- | -------- | -------- |
| code |  how do I reverse a string in python | code_topic |
| -------- | -------- | -------- |
| weather    | / news / prices 	weather in zurich   | explore_topic    |
| -------- | -------- | -------- |
| general     |  question 	what is your name     | ask_lumo     |
| -------- | -------- | -------- |
| anything else     | what time is it in tokyo     | ask_lumo     |




## Rate limits
The API limits requests per day per token is set as 1000 default per your request  i can  increase it. 

The counter resets at midnight. If you hit the limit you will see:

`MCP error -32603: Rate limit reached`


## Troubleshooting
### Server shows failed on mcp list

Kill old processes and restart:

`pkill -f explorer-mcp.js`


`opencode mcp list`


### LLM ignores the tool for coding questions
Some models are confident enough to answer coding questions without calling any tool. Use the explicit trigger `code <question>` or `use the explore_topic tool to research <question>` to force it.

## API documentation
💻 **API Reference:** [Read the manual before you break things](https://carlostkd.ch/explore/docs.php)


**Download:** [Explore Download](https://drive.proton.me/urls/PJ1FG3CGBR#GY4bmiL1NQRP)


*Explore MCP 
 @carlostkd*
