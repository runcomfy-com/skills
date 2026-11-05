---
name: runcomfy
description: Creative work on RunComfy, from upscaling and removing backgrounds to product photoshoots, UGC videos, ad variants, faceless explainers, music, setting up ComfyUI workflows, starting machines and training LoRAs. Use when a request is more than one plain generation.
---

# RunComfy skills

Use the connected RunComfy MCP tools. The client may prefix tool names with the plugin or server name. If disconnected, send the user to the client's RunComfy sign-in control, and never ask for a token in chat.

1. Call `get_skill_instructions` with no arguments to see the current catalog.
2. Call it again with the skill that fits, and follow the steps it returns. They name the models to use, what to ask and how to deliver.
3. For one plain image, video or song, skip the catalog and use `quote_model_run`, then `run_model`.

Do not invent tool names, model ids, inputs or prices. The tools and the skill's steps are the source of truth. Tell the user the model and the price before spending, and wait for their yes.
