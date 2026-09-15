---
name: lora-training
description: Prepare datasets and manage AI Toolkit LoRA training on RunComfy GPUs. Use for reviewing training YAML, captions, dataset readiness, starting an approved job, monitoring progress and retrieving checkpoints or samples. Verify base-model compatibility and costs before training.
---

# Train and retrieve a LoRA with RunComfy

Use the connected RunComfy MCP tools. If disconnected, use the client's authentication flow; do not request tokens in chat. Explaining LoRA settings alone does not require creating a dataset or starting a job.

## Prepare a reproducible configuration

1. Establish the user's training purpose, base model, dataset, desired output and spending limit. Verify supported base-model/trainer settings in current RunComfy documentation or the user's known working AI Toolkit config. An inference model's availability does not imply that it supports training.
2. Use `list_datasets` to find the intended dataset. For a new dataset, create and upload files only within the user's authorization. Preserve exact filenames and matching caption names.
3. `upload_dataset_file_from_url` imports media from an accessible URL; `upload_dataset_text_file` writes caption text. For local files, `get_dataset_upload_urls` provides signed upload destinations. Upload through a supported client tool without exposing signed URLs or credentials in prose. If no upload tool is available, explain that limitation.
4. Verify the resulting file inventory and `get_dataset_status` readiness before submission. Do not treat upload acceptance as a READY dataset.
5. Prepare the complete AI Toolkit YAML from verified configuration, including model/adapter compatibility, steps, learning rate, rank, batch size, resolution, checkpoint interval and sample settings. Use a unique job name consistently across the YAML. Do not silently rename an existing job or resume it.
6. Respect the platform path contract: `training_folder` is `/app/ai-toolkit/output`; dataset `folder_path` is `/app/ai-toolkit/datasets/{dataset_name}` using its **name**, not ID. These are remote container paths, not files to create on the user's computer.
7. Check current GPU options/rates and `get_balance`. Show the exact YAML, GPU type/count, dataset, estimated cost, spending limit and monitoring/stop conditions. Proceed only with the user's approval of that concrete run; previously approved unchanged settings do not need repeated confirmation.

## Submit, monitor and report

- Call `submit_training_job` once with the unchanged YAML and approved GPU settings. Record its job ID immediately.
- Monitor `get_training_job_status` with reasonable spacing. A timeout or client interruption does not justify another submission. Reconcile the existing job first.
- Use `cancel_training_job` only for user cancellation or an agreed stopping condition. `resume_training_job`, `edit_training_job`, dataset deletion and additional jobs require authorization appropriate to their effects.
- Retrieve `get_training_job_result` and report actual checkpoint/config/sample artifacts. A terminal STOPPED state alone does not prove successful training: inspect completed steps, errors and available artifacts.
- When the task includes stopping GPU charges, verify GPU release from available status or the RunComfy job page; distinguish that from process completion. Report an unavailable release signal honestly.
- Inspect samples when supported. A downloaded checkpoint or completed training job is not a separate inference/reload test or proof of output quality.
- If the user wants to run the LoRA, verify a compatible base model and its current `get_model` input schema, then obtain approval for that additional inference cost. Never assume every model accepts the same LoRA field.

## Useful requests

- “Inspect my dataset and review a short LoRA training configuration and GPU cost. Do not start yet.”
- “Check this training job's progress and return its checkpoints and final sample without resuming it.”

[AI Toolkit LoRA training](https://www.runcomfy.com/trainer/ai-toolkit) · [Trainer API documentation](https://docs.runcomfy.com/trainer-apis/introduction)
