# Made with Token360 · 示例图集

Every image here was generated on **2026-10-11** through [Token360](https://www.token360.ai/en-US/explore?utm_source=github&utm_medium=fork&utm_campaign=ecom-image-skill) with this skill's own `scripts/imagegen.sh` (api mode) and a prompt built from the matching template in `references/scenarios/`. The product is fictional and unbranded. No upstream media was reused.

本目录所有图片均于 2026-10-11 通过 Token360、用本 Skill 的 `scripts/imagegen.sh`（api 模式）和对应场景模板组装的 prompt 生成；产品为虚构、无品牌。未使用任何上游媒体。

| # | Output | Template | Prompt file | Model | Size / quality | Cost (USD) |
|---|---|---|---|---|---|---|
| 1 | [01-hero-image.jpg](01-hero-image.jpg) | `hero-image` | [prompts/01-hero-image.json](prompts/01-hero-image.json) | `gpt-image-2.5-flare` | 1024x1024 / high | 0.069 |
| 2 | [02-lifestyle-scene.jpg](02-lifestyle-scene.jpg) | `lifestyle-scene` | [prompts/02-lifestyle-scene.json](prompts/02-lifestyle-scene.json) | `gpt-image-2.5-flare` | 1536x1024 / high | 0.054 |
| 3 | [03-infographic.jpg](03-infographic.jpg) | `infographic` | [prompts/03-infographic.json](prompts/03-infographic.json) | `gpt-image-2.5-sunburst` | 1024x1536 / high | 0.055 |
| 4 | [04-a-plus-module.jpg](04-a-plus-module.jpg) | `a-plus-modules` | [prompts/04-a-plus-module.json](prompts/04-a-plus-module.json) | `gpt-image-2.5-sunburst` | 1552x960 / high | 0.050 |
| 5 | [05-edit-recolor.jpg](05-edit-recolor.jpg) | `edit-recolor` (multi-SKU grid), reference = #1 | [prompts/05-edit-recolor.json](prompts/05-edit-recolor.json) | `gpt-image-2.5-sunburst` | 1536x1024 / high | 0.065 |
| 6 | [06-motion.gif](06-motion.gif) (from [06-motion-gif-grid.jpg](06-motion-gif-grid.jpg)) | `motion-gif`, reference = #1 | [prompts/06-motion-gif-grid.json](prompts/06-motion-gif-grid.json) | `gpt-image-2.5-sunburst` | 1024x1024 / high | 0.081 |
| 7 | [07-flat-lay.jpg](07-flat-lay.jpg) | `flat-lay` | [prompts/07-flat-lay.json](prompts/07-flat-lay.json) | `dola-seedream-5.0-lite` | 2048x2048 (shown at 1024) | 0.045 |
| 8 | [08-gift-set.jpg](08-gift-set.jpg) | `gift-set` / `packaging` | [prompts/08-gift-set.json](prompts/08-gift-set.json) | `seedream-4.5` | 2048x2048 (shown at 1024) | 0.052 |

Costs are what Token360 charged for each call: token-priced models are usage × the published rate ($6.475/M input text tokens, $10.36/M input image tokens, $38.85/M output image tokens); Seedream is priced per image. Total for the 8 images: about **$0.47**. Images were re-saved as JPEG (quality 86) to keep the repo small.

## Reproduce

```bash
export IMAGE_API_BASE="https://api.token360.ai/v1"
export IMAGE_API_KEY="$TOKEN360_API_KEY"
export IMAGE_REF_FIELD="images"

# 1–4: text-to-image
IMAGE_MODEL=gpt-image-2.5-flare bash scripts/imagegen.sh --mode api \
  --prompt-file examples/token360-gallery/prompts/01-hero-image.json --size 1024x1024 --quality high

# 5–6: edits with a reference image
IMAGE_MODEL=gpt-image-2.5-sunburst bash scripts/imagegen.sh --mode api \
  --prompt-file examples/token360-gallery/prompts/05-edit-recolor.json --size 1536x1024 --quality high \
  --image examples/token360-gallery/01-hero-image.jpg

# 7–8: low-cost Seedream route (watermark off)
IMAGE_MODEL=dola-seedream-5.0-lite IMAGE_EXTRA_BODY='{"watermark":false}' bash scripts/imagegen.sh --mode api \
  --prompt-file examples/token360-gallery/prompts/07-flat-lay.json --size 2048x2048
```

`06-motion.gif`: the 4x4 grid was sliced into 16 cells with Python PIL, each frame re-centered on the product, played forward then backward (ping-pong) at 90 ms/frame, 128-color palette (see `references/motion-gif.md`).
