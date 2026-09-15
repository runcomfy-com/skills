# RunComfy skills and plugins

Run ComfyUI workflows in the cloud on GPU, generate and edit images, create videos, and manage LoRA training. Use RunComfy as an AI image generator and AI video generator from your assistant, with AI image models and AI video models including FLUX, Seedream, Seedance, Wan, LTX, Nano Banana and Kling.

## Cursor and Claude plugins

The [RunComfy plugin](plugins/runcomfy/README.md) bundles the hosted MCP endpoint with four focused skills for image generation, video generation, ComfyUI workflows and LoRA training. It supports Cursor and the shared Claude Code/Cowork plugin format. Marketplace approval is separate from publishing this source.

- **Claude marketplace manifest:** [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json)
- **Cursor marketplace manifest:** [`.cursor-plugin/marketplace.json`](.cursor-plugin/marketplace.json)
- **Self-contained plugin:** [`plugins/runcomfy`](plugins/runcomfy)

See the [plugin README](plugins/runcomfy/README.md) for installation, authorization, example prompts and cost handling.

## Individual CLI skills

The existing top-level skill directories provide task-specific and model-specific RunComfy CLI guidance. Install selected skills from this repository:

```bash
npx skills add runcomfy-com/skills --skill ai-image-generation
npx skills add runcomfy-com/skills --skill ai-video-generation
```

[Browse existing skills on skills.sh](https://www.skills.sh/runcomfy-com/skills). Some older skill documents retain historical installation links and model defaults; use this repository name and verify current model inputs and prices before running jobs.

## RunComfy

[AI image models and AI video models](https://www.runcomfy.com/models) · [ComfyUI workflows](https://www.runcomfy.com/comfyui-workflows) · [AI Toolkit LoRA training](https://www.runcomfy.com/trainer/ai-toolkit) · [Documentation](https://docs.runcomfy.com) · [Support](mailto:hi@runcomfy.com)
