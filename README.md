# a-book-for-lily


### Architectural Diagram

┌────────────────────────────────────────────────────────────────────────────┐
│                            YOUR LAPTOP (RTX 5090)                          │
│                                                                            │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                         WSL2 Ubuntu 22.04                           │   │
│  │                                                                     │   │
│  │  ┌────────────────────────────────────────────────────────────────┐ │   │
│  │  │                    flux-coloring-book/                          │ │  │
│  │  │                                                                 │ │  │
│  │  │  src/                                                           │ │  │
│  │  │  ├── core/           # Shared FLUX pipeline                     │ │  │
│  │  │  │   ├── pipeline.py      # Model loading, FP8                  │ │  │
│  │  │  │   ├── generator.py     # Image generation                    │ │  │
│  │  │  │   └── config.py        # Settings                            │ │  │
│  │  │  │                                                              │ │  │
│  │  │  ├── prompts/        # Prompt engineering                       │ │  │
│  │  │  │   ├── templates.py     # Base templates                      │ │  │
│  │  │  │   ├── cultural.py      # Pakistani context                   │ │  │
│  │  │  │   └── styles.py        # Coloring book modifiers             │ │  │
│  │  │  │                                                              │ │  │
│  │  │  └── mcp/            # Claude integration                       │ │  │
│  │  │      └── server.py        # FastMCP server                      │ │  │
│  │  │                                                                 │ │  │
│  │  │  configs/                                                       │ │  │
│  │  │  └── settings.yaml        # Paths, defaults                     │ │  │
│  │  │                                                                 │ │  │
│  │  │  comfyui/                                                       │ │  │
│  │  │  └── workflows/           # Pre-built workflows                 │ │  │
│  │  │      ├── standard.json         # 1024x1024, 20 steps            │ │  │
│  │  │      ├── detailed.json         # 1024x1024, 30 steps            │ │  │
│  │  │      └── pattern.json          # Borders, seamless              │ │  │
│  │  │                                                                 │ │  │
│  │  │  docs/                                                          │ │  │
│  │  │  ├── friend-guide-comfyui.md   # Screenshot walkthrough         │ │  │
│  │  │  ├── friend-guide-claude.md    # MCP setup for friends          │ │  │
│  │  │  └── prompt-examples.md        # Copy-paste templates           │ │  │
│  │  └─────────────────────────────────────────────────────────────────┘ │  │
│  │                                                                      │  │
│  │  ┌─────────────────┐          ┌─────────────────┐                   │  │
│  │  │    ComfyUI      │          │   MCP Server    │                   │  │
│  │  │   Port 8188     │          │   Port 8765     │                   │  │
│  │  │                 │          │                 │                   │  │
│  │  │  Browser UI     │          │  Claude Tools   │                   │  │
│  │  │  for friends    │          │  for friends    │                   │  │
│  │  └────────┬────────┘          └────────┬────────┘                   │  │
│  │           │                            │                            │  │
│  └───────────┼────────────────────────────┼────────────────────────────┘  │
│              │                            │                               │
│              │    ┌───────────────────────┘                               │
│              │    │                                                       │
│              ▼    ▼                                                       │
│         Local Network: 192.168.x.x                                        │
│         (or Tailscale for remote access)                                  │
└────────────────────────────────────────────────────────────────────────────┘
                              │
          ┌───────────────────┼───────────────────┐
          │                   │                   │
          ▼                   ▼                   ▼
    ┌──────────┐        ┌──────────┐        ┌──────────┐
    │ Friend A │        │ Friend B │        │   You    │
    │ Browser  │        │ Claude   │        │  Either  │
    │ ComfyUI  │        │ Desktop  │        │   Path   │
    └──────────┘        └──────────┘        └──────────┘

### Timeline Summary
Day |   Phase      | Tasks
1     Environment   WSL2, CUDA, Python, Miniconda
1-2   ComfyUI       Install, download models, custom nodes
2     Workflows     Create and test 3 workflow templates
2-3   Documentation Friend guides, prompt examples
3-4   MCP Server    Core modules, prompt engineering, server
4     Networking    Firewall, port forwarding, (Tailscale)
5     Testing       End-to-end tests, friend access tests