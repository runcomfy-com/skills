---
name: comfyui-workflows
description: Inspect and run ComfyUI workflows on RunComfy GPU deployments. Use for workflow inputs, deployment selection, serverless inference, request status and output retrieval. Review the actual workflow schema and GPU settings before paid execution or deployment changes.
---

# Run ComfyUI workflows on RunComfy

Use RunComfy's connected MCP tools. Authenticate through the client's sign-in control when required; never ask for credentials in chat. General questions about local ComfyUI do not require account access or a cloud run.

## Inspect before executing

1. Call `list_deployments` and select the deployment the user owns and intends to use. Use `get_deployment` with `include_payload: true` for its actual workflow graph, inputs, defaults, GPU configuration and current state; the default response omits the full payload.
2. Map the user's requested changes to the workflow's real input names and node IDs. Do not guess which node controls the prompt, seed, dimensions, steps or file input. Preserve unspecified values.
3. File handling depends on the deployment schema and `submit_request` contract. Follow the exposed input contract rather than assuming every ComfyUI file field accepts an arbitrary URL. Do not publish private inputs without permission.
4. Use `get_balance` and current deployment pricing/configuration to explain the available cost estimate. GPU startup, execution and keep-warm time may affect charges; a job timestamp alone does not establish billed runtime.
5. Present deployment ID, requested overrides, expected outputs, GPU settings and budget/stop condition. Reuse the user's existing authorization. Creating, updating or deleting a deployment changes persistent resources; do that only when requested or necessary within the agreed task.

## Execute and recover

- Submit exactly once with `submit_request`, using the actual deployment ID and schema-valid overrides. Prefer asynchronous completion when the tool exposes it.
- Save the request ID. Poll `get_request_status` and retrieve `get_request_result` for that ID. These tools are for deployment requests; hosted Model API jobs use the separate `get_model_request_*` tools.
- A timeout is not evidence that the run was rejected. Reconcile the existing request before submitting any replacement.
- Use `cancel_request` for a user cancellation or an agreed stopping condition. Explain that cancellation may not undo already incurred charges.
- Return actual output URLs and request ID. Check the deployment's state after completion when the task includes releasing GPU resources or controlling ongoing cost. Do not delete the deployment as routine cleanup.
- Describe standby and keep-warm state accurately. Report actual wallet movement only after a relevant recheck, and do not attribute concurrent account activity to this one job.
- Use `call_instance_proxy` only for a specific authorized action whose route and effect are understood; it is not a read-only debugging shortcut.

## Useful requests

- “List my RunComfy deployments and inspect the image workflow's inputs. Do not run or change anything.”
- “Run one image on this deployment with these overrides, within the budget I approved, and return its output.”

[ComfyUI workflows](https://www.runcomfy.com/comfyui-workflows) · [Serverless API documentation](https://docs.runcomfy.com/serverless/introduction)
