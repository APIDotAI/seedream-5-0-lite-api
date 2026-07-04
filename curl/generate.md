# Seedream 5.0 Lite cURL Quickstart

## What this example shows

This example shows how to call Seedream 5.0 Lite through APIDot with a server-side API key.

## Requirements

- An APIDot account.
- An APIDot API key stored server-side.
- `curl` installed locally.
- A backend or terminal environment that does not expose API keys to browser code.

## Environment variables

Use placeholders only. Do not commit real credentials.

```env
APIDOT_API_KEY=YOUR_API_KEY_HERE
```

## How to run

Add `callback_url` only when you have a real webhook receiver.

```bash
export APIDOT_API_KEY="YOUR_API_KEY_HERE"

curl --fail-with-body --request POST \
  --url https://api.apidot.ai/api/generate/submit \
  --header "Authorization: Bearer $APIDOT_API_KEY" \
  --header "Content-Type: application/json" \
  --data '{
  "model": "seedream-5.0-lite",
  "input": {
    "prompt": "A clean ecommerce hero image of a premium wireless speaker on a brushed metal desk, precise typography on a small label reading APIDot, realistic reflections, soft studio lighting, commercial product photography.",
    "size": "16:9",
    "n": 1
  }
}'
```

Store the returned `data.task_id`, then poll status:

```bash
curl --fail-with-body --request GET \
  --url https://api.apidot.ai/api/generate/status/task-unified-example \
  --header "Authorization: Bearer $APIDOT_API_KEY"
```

## Request variants

### seedream-5.0-lite

```json
{
  "model": "seedream-5.0-lite",
  "callback_url": "https://your-domain.com/callback",
  "input": {
    "prompt": "A clean ecommerce hero image of a premium wireless speaker on a brushed metal desk, precise typography on a small label reading APIDot, realistic reflections, soft studio lighting, commercial product photography.",
    "size": "16:9",
    "n": 1
  }
}
```

### seedream-5.0-lite-edit

```json
{
  "model": "seedream-5.0-lite-edit",
  "callback_url": "https://your-domain.com/callback",
  "input": {
    "prompt": "Keep the source product identity. Replace the background with a clean spring campaign setup, preserve realistic shadows, and make the final image suitable for an ecommerce hero asset.",
    "image_urls": [
      "https://your-domain.com/source-image.png"
    ],
    "size": "2K",
    "n": 1
  }
}
```

### custom size object

```json
{
  "model": "seedream-5.0-lite",
  "callback_url": "https://your-domain.com/callback",
  "input": {
    "prompt": "A structured product infographic with readable labels, clean iconography, and balanced spacing.",
    "size": {
      "width": 2304,
      "height": 1728
    },
    "n": 1
  }
}
```

## Expected response

```json
{
  "code": 200,
  "data": {
    "task_id": "task-unified-example",
    "status": "finished",
    "output": {
      "files": [
        {
          "file_url": "https://example.com/generated-image.png",
          "file_type": "image"
        }
      ]
    },
    "error_message": null
  }
}
```

## Production notes

- Keep APIDot API keys on the server side only.
- Store selected model, request payload, user ID, and response metadata together for support and retries.
- Store `data.task_id` before polling or waiting for a webhook.
- Poll at a moderate interval and avoid hot loops.
- Treat `finished` and `failed` as terminal states.

## Common mistakes

- Committing a real API key or `.env` file.
- Calling APIDot directly from browser code.
- Reusing request fields from a different model without checking this model's docs.

## Related links

- Website: https://apidot.ai
- Docs: https://apidot.ai/docs
- Seedream 5.0 Lite docs: https://apidot.ai/docs/seedream-5-0-lite
- Seedream 5.0 Lite model page: https://apidot.ai/models/seedream-5-0-lite
- GitHub: https://github.com/APIDotAI
- Examples: https://github.com/APIDotAI/apidot-examples
