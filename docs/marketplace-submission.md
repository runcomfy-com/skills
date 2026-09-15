# RunComfy plugin submission notes

The public source contains one self-contained plugin with separate Cursor and Claude manifests. It can be reviewed without access to RunComfy's server implementation or any account credentials.

## Form values

| Field | Value |
| --- | --- |
| Name | RunComfy |
| Plugin identifier | `runcomfy` |
| Author | RunComfy |
| Contact | hi@runcomfy.com |
| Homepage | https://www.runcomfy.com |
| Setup documentation | https://docs.runcomfy.com/mcp/introduction |
| Repository | https://github.com/runcomfy-com/skills |
| Plugin directory | `plugins/runcomfy` |
| Logo within plugin | `assets/logo.png` — existing 512 × 512 RunComfy mark |
| License | MIT |
| Privacy policy | https://www.runcomfy.com/legal/privacy |

Description:

> Run ComfyUI workflows in the cloud on GPU, generate images with FLUX and Seedream, create videos with Seedance, Wan and LTX, and manage LoRA training.

Longer overview:

> Use RunComfy as an AI image generator and AI video generator from your assistant. Explore AI image models including FLUX and Seedream, create videos with Seedance, Wan and LTX, run ComfyUI workflows in the cloud on GPU, and manage AI Toolkit LoRA training. Four focused skills help you review current inputs and costs, submit jobs, track progress, and retrieve images, videos, checkpoints and samples. Connect your RunComfy account through browser authorization; paid runs use RunComfy credits.

## Source layout and submission

- Cursor discovers `plugins/runcomfy` from the root `.cursor-plugin/marketplace.json`; its plugin manifest is `plugins/runcomfy/.cursor-plugin/plugin.json`.
- Claude Code and Cowork discover the same directory from the root `.claude-plugin/marketplace.json`; their plugin manifest is `plugins/runcomfy/.claude-plugin/plugin.json`.
- The package uses only four `skills/*/SKILL.md` files and the hosted MCP connection. Top-level legacy CLI skills are outside the plugin boundary.
- Cursor submission: https://cursor.com/marketplace/publish
- Claude Code/Cowork submission: https://platform.claude.com/plugins/submit

Before submitting a default-branch repository URL, merge the reviewed change into that branch and verify the manifests and logo are publicly retrievable. A pull-request branch is source for review, not evidence that the default branch contains the plugin. If a form explicitly accepts a revision, use the reviewed commit; do not assume it accepts a GitHub `/tree/` URL as a repository URL.

After merge, the logo is available at:

`https://raw.githubusercontent.com/runcomfy-com/skills/main/plugins/runcomfy/assets/logo.png`

For an immutable logo URL, replace `main` with the reviewed commit SHA.

## Model-name evidence

These public RunComfy model pages were checked on 2026-09-15. They support the family/version names in plugin metadata; runtime selection must still use the tools' current model ID, input schema and price. These checks did not generate media or establish provider provenance.

- [FLUX 2 Klein 9B](https://www.runcomfy.com/models/blackforestlabs/flux-2-klein/9b/text-to-image)
- [Seedream 5.0 Lite](https://www.runcomfy.com/models/bytedance/seedream-5/lite/text-to-image)
- [Seedance 2.5](https://www.runcomfy.com/models/bytedance/seedance-2.5/text-to-video/4k)
- [Wan 3.0](https://www.runcomfy.com/models/wan-ai/wan-3.0/image-to-video)
- [LTX 2.5](https://www.runcomfy.com/models/lightricks/ltx-2.5/image-to-video/fast)

## Validation on 2026-09-15

- Claude Code 2.1.251: `claude plugin validate plugins/runcomfy --strict` passed.
- Claude marketplace: `claude plugin validate .claude-plugin/marketplace.json --strict` passed.
- Cursor's official [template validator](https://github.com/cursor/plugin-template/blob/main/scripts/validate-template.mjs), Git blob `5310b9e8743213a7ac6c014d743bb03917dcf020`, passed against this repository. Its only warning was the intentionally absent optional hooks file.
- A real Claude marketplace add/install in a separate temporary `CLAUDE_CONFIG_DIR` succeeded. The installed cache contained the four expected skills, MIT license and RunComfy HTTP MCP configuration. The user's existing plugin settings were not modified.
- Public MCP authorization metadata returned HTTP 200 and advertised S256 PKCE. An unauthenticated `tools/list` request returned HTTP 401 with its protected-resource metadata challenge. No authentication secrets or paid calls were used.
- Skill instructions were checked against the RunComfy tool contract: full deployment payload, distinct deployment/model request status tools, training container paths, asynchronous request IDs, and cancellation outcomes.

Remaining client checks: native Cursor local-import discovery and browser OAuth/tool calls in the target Cursor/Claude Code/Cowork client. Structural validation and cache installation do not prove authenticated tool execution or an approved marketplace listing.

## Native client check

Cursor's [documented local flow](https://cursor.com/docs/plugins): copy or symlink `plugins/runcomfy` to `~/.cursor/plugins/local/runcomfy`, restart Cursor or run **Developer: Reload Window**, then open **Customize** and confirm four skills plus the RunComfy MCP server. Organization policy must allow local plugin imports. Use a fresh destination; do not replace an existing plugin with the same name.

Authenticate in the client, then ask: “Use RunComfy to list my deployments and show my balance. Do not run, create, update, delete, upload or train anything.” Verify actual tool results before reporting connection success.

## Official format references

- [Cursor plugin reference](https://cursor.com/docs/reference/plugins)
- [Claude plugin reference](https://code.claude.com/docs/en/plugins-reference)
- [Claude marketplace reference](https://code.claude.com/docs/en/plugin-marketplaces)
- [Cowork plugin installation](https://claude.com/docs/cowork/guide/plugins)
- [Claude directory submission](https://claude.com/docs/plugins/submit)
