# RunComfy for Cursor, Claude Code and Cowork

Run ComfyUI workflows in the cloud on GPU, use RunComfy as an **AI image generator** and **AI video generator**, and manage **LoRA training** from your assistant. This plugin combines RunComfy's hosted MCP connection with four practical skills for reviewing requests, running jobs and retrieving results.

Explore [AI image models and AI video models](https://www.runcomfy.com/models), including FLUX, Seedream, Seedance, Wan, LTX, Nano Banana and Kling. Current model families include FLUX 2, Seedream 5.0, Seedance 2.5, Wan 3.0 and LTX 2.5. Each run uses live model discovery and the selected endpoint's current schema and price; availability and supported settings can change.

## Install and connect

### Claude Code

After this package is merged into the repository's default branch:

```text
/plugin marketplace add runcomfy-com/skills
/plugin install runcomfy@runcomfy
```

Open `/mcp`, select RunComfy and complete its browser authorization. Obtain a RunComfy API token from your [RunComfy profile](https://www.runcomfy.com/profile) if requested by the RunComfy authorization page. Enter it only on that page, not in chat or configuration files.

### Cowork

In **Customize → Plugins → Add marketplace**, add the GitHub marketplace `runcomfy-com/skills`, install **RunComfy**, and complete the connector's sign-in prompt. Organization policy can restrict personal plugin installation. The package uses the documented shared Claude plugin format; verify connection status in your client before running jobs.

### Cursor

Install **RunComfy** from Cursor's marketplace after its listing is approved, then connect the RunComfy MCP server in the client's tool settings. This source package does not by itself establish an approved listing.

For local development, copy or symlink this **plugin directory** to `~/.cursor/plugins/local/runcomfy`, then reload Cursor and check **Customize**. Local imports must be allowed by your organization. See [Cursor local testing](https://cursor.com/docs/plugins).

## Included skills

| Skill | What it helps you do |
| --- | --- |
| `generate-image` | Find an image or editing model, review its inputs and price, submit one job and retrieve its outputs. |
| `generate-video` | Select a video endpoint, review duration/resolution/audio and cost, monitor generation and return a playable output link. |
| `comfyui-workflows` | Inspect owned deployments, map actual workflow inputs, run approved requests and check resource state. |
| `lora-training` | Check datasets and training YAML, monitor an approved AI Toolkit job and retrieve checkpoints and samples. |

In Claude Code, invoke a skill explicitly with `/runcomfy:generate-image`, `/runcomfy:generate-video`, `/runcomfy:comfyui-workflows` or `/runcomfy:lora-training`. Clients can also select a relevant skill from your request.

Try: “Compare current Seedance, Wan and LTX models for a five-second product video. Show price and inputs before running.” Or: “List my ComfyUI deployments and inspect their inputs. Do not run or change anything.”

## Account, costs and data

- A RunComfy account is required for authenticated tools. Paid generation, GPU deployments and training consume RunComfy credits; the plugin's source is MIT-licensed.
- The MCP endpoint is `https://mcp.runcomfy.com/mcp`. No local server, RunComfy CLI, shell hooks or bundled credentials are required.
- Your requests, prompts, referenced media and training configuration are sent to RunComfy when you use its tools. File inputs must be accessible to the remote service; a private local path is not sufficient. Upload or publish private assets only with authorization.
- The connection exposes RunComfy account tools, including persistent resource changes. The skills guide cost review and careful execution; client permissions and service authorization enforce access.
- Slow jobs are monitored by request ID, without automatic paid resubmission. Returned media links may need to be opened directly when inline rendering is unavailable.
- Price estimates and monitoring deadlines are not guaranteed spending caps. Some running model requests cannot be cancelled; report the cancellation outcome and remaining job state.

Read [RunComfy's Privacy Policy](https://www.runcomfy.com/legal/privacy) and [Terms of Service](https://www.runcomfy.com/legal/tos).

## Source and support

Both client manifests point to this self-contained directory. The four skill files are shared; Cursor reads `mcp.json`, while Claude reads `.mcp.json`. Parent-repository CLI skills are not automatically loaded by this plugin.

[MCP documentation](https://docs.runcomfy.com/mcp/introduction) · [ComfyUI workflows](https://www.runcomfy.com/comfyui-workflows) · [LoRA training](https://www.runcomfy.com/trainer/ai-toolkit) · [Report an issue](https://github.com/runcomfy-com/skills/issues) · [hi@runcomfy.com](mailto:hi@runcomfy.com)
