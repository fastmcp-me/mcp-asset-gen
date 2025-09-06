[![Add to Cursor](https://fastmcp.me/badges/cursor_dark.svg)](https://fastmcp.me/MCP/Details/766/image-generator-openai)
[![Add to VS Code](https://fastmcp.me/badges/vscode_dark.svg)](https://fastmcp.me/MCP/Details/766/image-generator-openai)
[![Add to Claude](https://fastmcp.me/badges/claude_dark.svg)](https://fastmcp.me/MCP/Details/766/image-generator-openai)
[![Add to ChatGPT](https://fastmcp.me/badges/chatgpt_dark.svg)](https://fastmcp.me/MCP/Details/766/image-generator-openai)
[![Add to Codex](https://fastmcp.me/badges/codex_dark.svg)](https://fastmcp.me/MCP/Details/766/image-generator-openai)
[![Add to Gemini](https://fastmcp.me/badges/gemini_dark.svg)](https://fastmcp.me/MCP/Details/766/image-generator-openai)

# mcp-asset-gen
[![npm version](https://badge.fury.io/js/mcp-asset-gen.svg)](https://badge.fury.io/js/mcp-asset-gen)


This tool allows Claude to speak to OpenAI, and use `gpt-image-1` to generate image assets. This can be pretty useful for game or web development, when you need to print individual assets.

# Requirements

- Node 
- An OpenAI [API Key](https://platform.openai.com/settings/organization/api-keys)
    - Note that this requires an organization, with ID verification at the moment.

# Installation

1. Get an API KEY from the [OpenAI website](https://platform.openai.com/settings/organization/api-keys).

2. Export it in your shell as API_KEY.

```bash
export API_KEY=sk-proj-....
```

3. Then, paste this into that same shell:

```bash
jq --arg apiKey "$API_KEY" \
'.mcpServers = (.mcpServers // {}) | 
 .mcpServers["mcp-asset-gen"] = {
   type: "stdio",
   command: "npx",
   args: ["mcp-asset-gen"],
   env: { API_KEY: $apiKey }
 }' ~/.claude.json > ~/.claude.tmp && mv ~/.claude.tmp ~/.claude.json
```

4. You're done! Ask Claude to generate you an image for something, and you'll see

```
> generate a small logo image that i could use for my arcade game

 I'll generate a logo for your arcade game. Please provide a more specific description of what you'd like to see in the logo (colors, style,
  game theme, etc.) for better results.

> It should look like an old school pacman machine (liek a wooden arcade machine)

⏺ mcp-asset-gen:generateImag(outputPathAbsolute: "/Users/jbrower/projects/mcp-asset-gen/arcade-logo.png", prompt: "An old school wooden arcade…
   (MCP)                    machine logo in the style of Pacman, with retro colors and pixelated elements, top-down view of the cabinet,
                            nostalgic arcade gaming feel, vibrant colors against dark background", quality: "high", size: "1024x1024")
  ⎿  The image is now available at /Users/jbrower/projects/mcp-asset-gen/arcade-logo.png.

⏺ Generated arcade logo saved to /Users/jbrower/projects/mcp-asset-gen/arcade-logo.png
```

