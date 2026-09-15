---
name: generate-image
description: Generate or edit images with RunComfy AI image models including FLUX, Seedream and Nano Banana. Use for text-to-image, reference images, product photography, illustrations and image edits. Browse current models, review inputs and cost, then run and retrieve results.
---

# Generate and edit images with RunComfy

Use the connected RunComfy MCP tools. The client may prefix tool names with the plugin/server name. If disconnected, direct the user to the client's RunComfy authentication control. Never request an API token in chat or add one to a file.

## Choose and review

1. Establish the subject, intended use, dimensions, number of images and any reference images. Reuse details already provided.
2. Use `list_models` with a targeted `search` and `category` such as `text-to-image` or `image-to-image`. Use `list_model_categories` if unsure of a category. Start with a small page and paginate when needed.
3. Match the user's requested model family. Examples available through RunComfy include FLUX 2, Seedream 5.0 and Nano Banana 2. Use the actual returned `model_id`; do not construct version strings or assume a similarly named endpoint supports edits.
4. Call `get_model` for the selected ID. Read current input schema, required inputs, enums, defaults, pricing unit and output type. Do not reuse another model's field names or hard-code remembered prices.
5. Check `get_balance` before paid work. Present the model, final prompt, reference inputs, dimensions/count and available cost estimate. Proceed within the user's existing authorization and spending limit; ask only when scope or cost is missing or changed. Explain when pricing is an estimate.

## Run and retrieve

- For a file input, use an HTTPS URL accessible to the model service. A local path, browser-only `blob:` URL or authenticated gallery page is not a usable input URL. Do not publish a private image without authorization; if no supported upload route is available, explain what input is needed.
- Call `run_model` once with `model_id`, schema-valid `inputs` and `wait_for_completion: false`. Record the returned request ID.
- Poll `get_model_request_status` for that same ID with reasonable spacing. Retrieve `get_model_request_result` when finished. Use `cancel_model_request` only when the user requested cancellation or an agreed stop condition is reached.
- Inspect the cancellation `outcome`: a running or finished job may be `not_cancellable`. A cancellation attempt is not proof the job stopped or that charges ended. Reconcile status/results and report this limitation; a monitoring deadline is not a guaranteed spending cap.
- A timeout or interrupted response does not prove submission failed. Recover the existing request before considering a new paid call. Never silently submit a replacement or switch models.
- Return the actual output URL and request ID. Display the image when supported; otherwise provide a direct link. Say whether pixels were inspected. A returned URL is not proof that the image rendered correctly.
- Keep planned settings, returned settings and observed output properties separate. If the server fails or a result is unavailable, report the actual status and next recovery step.

## Useful requests

- “Compare current FLUX and Seedream image options for one square product image. Show inputs and price before running.”
- “Edit this image to change only the background, using a supported image-editing model. Keep the product unchanged.”

[AI image models](https://www.runcomfy.com/models) · [Model API documentation](https://docs.runcomfy.com/model-apis/quickstart) · [MCP setup](https://docs.runcomfy.com/mcp/introduction)
