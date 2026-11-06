---
name: affogato-studios
description: Use Affogato's studio tools from an agent in one call each — lipsync a video to audio, text-to-speech with library voices, talking-head videos (keyframe → speech → animate), professional headshots, cast swaps (replace the people in a clip), fashion try-ons and product ad shots. Use when the user asks for any of these outcomes rather than a raw model.
license: MIT
metadata:
  author: Affogato
  version: "0.1.0"
  homepage: https://affogato.ai/developers
---

# Affogato studios from an agent

Prefer the MCP tools when the Affogato connector is present; otherwise call
`POST https://api.affogato.ai/v1/studios/<verb>` with `Authorization: Bearer
$AFFOGATO_API_KEY` (see the `affogato-generate` skill for keys, polling and
files). Every verb returns a generation: poll `GET /v1/generations/{id}?wait=25`
until `succeeded`, then show `outputs[].url`.

Inputs are **file ids**: upload with `POST /v1/files` (multipart) or
`/v1/files/from-url`; outputs of earlier generations are files too.

| Outcome | MCP tool / REST verb | Required | Options |
|---|---|---|---|
| Lipsync a video to audio | `lipsync` / `/studios/lipsync` | `video_file`, `audio_file` | `model` (`sync-lipsync-v3` default), `length_mode` cut_off·loop·bounce·silence·remap, `speaker {frame,x,y}` |
| Speech from text | `text_to_speech` / `/studios/text-to-speech` | `text` (≤ 5,000 chars, priced per 1,000) | `voice` from `list_voices` / `GET /studios/voices`, `model` |
| Talking head | `talking_head_keyframe` → `text_to_speech` → `talking_head_video` | face file; script; keyframe + speech files | sets from `list_talking_head_sets`, `framing` close_up·waist_up·wide, `format` landscape·portrait, engine `kling-ai-avatar-v2` (cheaper) or `omnihuman-15` |
| Headshot | `headshot` / `/studios/headshot` | `face_file` or `character_id` | `style_item_id` from `list_headshot_styles`, `controls` (framing, background, wardrobe, lighting, expression, retouch — exact vocabulary in the styles listing), `notes`, `aspect` 3:4·1:1·4:3 |
| Cast swap | `cast_swap` / `/studios/cast-swap` | `source_video_file` (4–30 s), `subjects[{photos}]` | per subject `kind` person·object, `label`, `slot` left·center·right·main, `placement`; `notes`; `resolution` |
| Try-on | `try_on` / `/studios/try-on` | `garment_files` (1–4) | `person_file` (else describe: `gender`, `age`, `build`), `notes`, `aspect` |
| Product ad shot | `product_shot` / `/studios/product-shot` | `product_file`, `template_key` from `list_product_templates` | `brief` (offer copy, direction), `aspect` 1:1·4:5·9:16·16:9, `num_images` |

## Costs and confirmation

Studio prices depend on inputs (lipsync and talking heads bill per second
of audio; headshots and product shots are image prices). On MCP the tool
returns `confirmation_required` with the exact credits when a call exceeds
the workspace's confirm threshold: tell the user the price, then call again
with `confirm_credits` set to that number. On REST, quote with the model's
price from `GET /v1/models/{id}` or accept the `credits_charged` in the
response; failed and cancelled generations are refunded.

## Tips

- Talking heads: keep each script segment under 45 s; one `talking_head_video`
  per segment, then stitch (or ask the user to assemble in Affogato's editor).
- Headshots: pick a style first; add at most one or two controls as overrides.
- Cast swap: 1–4 photos per person, clear frontal faces; clips of 5–15 s work best.
- Try-on: garments on a plain background; one garment per file.
