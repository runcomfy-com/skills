---
name: generate-video
description: Create videos with RunComfy AI video models including Seedance, Wan, LTX and Kling. Use for text-to-video, image-to-video, reference-to-video and video edits. Check model-specific duration, aspect ratio, audio, inputs and price before submitting one job.
---

# Generate videos with RunComfy

Use the connected RunComfy MCP tools; tool names may have a client-specific prefix. If authentication is needed, use the client's RunComfy sign-in flow. Keep credentials out of chat and files.

## Plan the shot

1. Reuse the user's subject, action, camera motion, duration, aspect ratio, resolution, audio preference and budget. Clarify only the details needed to choose a valid request.
2. Search `list_models` by the requested family and capability. RunComfy includes Seedance 2.5, Wan 3.0 and LTX 2.5, as well as Kling models; current availability comes from the returned model list. Use `list_model_categories` when needed.
3. Call `get_model` for the exact returned `model_id`. Distinguish text-to-video, image-to-video, reference-to-video, first/last-frame and editing endpoints. Do not infer supported inputs from a family name.
4. Read the exact required input names and limits. Match duration, resolution, aspect ratio, audio and seed to the schema. A pricing tier label may differ from the encoded output dimensions.
5. Check `get_balance`. Show the complete request and available price estimate, including per-second pricing when applicable. Use existing user authorization and spending limits; obtain missing authorization before paid submission or publication of private input assets.

## Submit once and monitor

- Use publicly accessible HTTPS URLs for model file inputs. Do not send local paths or private browser links. If the user provides a local file, use an available authorized upload route; otherwise explain the requirement.
- Call `run_model` once with `wait_for_completion: false`. Save its request ID and use `get_model_request_status` to monitor that same job.
- Poll with reasonable spacing. Do not resubmit just because generation is slow, the client times out, or the response is interrupted. Reconcile the existing request first.
- Fetch `get_model_request_result` after completion. Use `cancel_model_request` if the user cancels or an agreed stopping condition is reached.
- Inspect the cancellation `outcome`: an in-progress or finished request may be `not_cancellable`. Report that result and continue reconciling the job. A monitoring deadline does not guarantee cancellation or a hard spending cap, and already-incurred charges remain possible.
- Return the actual video URL and request ID. Open or embed it if the client supports video. When inline playback fails, provide the exact direct output link.
- Distinguish a completed job, successful file retrieval and actual playback verification. Report observed duration, resolution and audio only if inspected; avoid claiming visual quality from status alone.

## Useful requests

- “Compare Seedance, Wan and LTX for a five-second product clip. Show current prices and supported inputs; do not run yet.”
- “Animate this mug image with a slow camera orbit. Review the exact model, duration and cost first.”

[AI video models](https://www.runcomfy.com/models) · [Model API documentation](https://docs.runcomfy.com/model-apis/quickstart)
