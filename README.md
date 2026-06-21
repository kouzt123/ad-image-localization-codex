# Image Localization

Image Localization is a Codex skill for turning source image creatives into localized, platform-ready ad and social assets.

It prioritizes Codex built-in vision, image generation, and image editing for native visual quality. Local code is used only for deterministic tasks such as resizing, cover-cropping, naming, manifests, and QA sheets.

## Core Value

This skill uses Codex's built-in image capabilities, so it can generate and localize images with your Codex subscription quota. It does not require extra image API setup, API keys, billing configuration, or a separate generation service.

The tradeoff is speed: the built-in Codex image workflow is slower than a dedicated batch image API. For marketing teams and operators, it is still a strong long-running workflow because the setup cost is low, the visual quality is native, and the per-task value is high.

Future work may include a separate high-throughput skill based on the Nano Banana API for faster bulk production.

## What It Does

- Translates visible text inside images into target languages.
- Preserves brand names, product names, logos, subjects, and visual hierarchy.
- Adapts creatives into common ad/social sizes:
  - `1200x1200`
  - `1920x1080`
  - `1080x1350`
  - `1080x1920`
  - `1200x628`
- Handles special resolutions by generating the closest safe aspect ratio, then applying deterministic cover-crop when appropriate.
- Maintains brand/product terminology memory.
- Produces clean, upload-ready filenames and manifests.
- Runs visual QA before delivery.

## Design Philosophy

The goal is native-looking localized creative, not simple masking or mechanical text replacement.

The skill follows this split:

- Model work: recognition, translation, image editing, layout reflow, canvas extension, visual repair.
- Code work: exact resize, cover-crop, file naming, manifests, contact sheets, dimension checks.

Blurred padding is not used as a default delivery strategy.

## Size Handling

For special sizes such as `1200x628`, the recommended workflow is:

1. Generate a strong `16:9` version with top/bottom safe margins.
2. Resize proportionally from `1920x1080` to `1200x675`.
3. Crop the vertical overflow to `1200x628`.

This preserves geometry and avoids non-uniform stretching.

## Terminology Memory

The skill supports a JSON memory file for user-approved terminology:

```json
{
  "version": 1,
  "brands": {
    "example-brand": {
      "display_name": "Example Brand",
      "rules": [
        {"term": "Example Brand", "action": "preserve"}
      ],
      "products": {}
    }
  }
}
```

Brand-level rules apply across products. Product-level rules can override brand rules.

## Example Prompts

```text
Use image-localization to translate this game ad into German, French, Spanish, Japanese, and Korean. Export 1200x1200, 1920x1080, 1080x1350, 1080x1920, and 1200x628.
```

```text
Localize this poster into Arabic and Vietnamese. Preserve the product name in English and make sure the 1200x628 output does not stretch the text.
```

```text
Remember that "Codex" should not be translated for OpenAI assets.
```

## File Structure

```text
image-localization/
├── SKILL.md
├── README.md
├── README.zh-CN.md
├── brand_term_memory.json
└── agents/
    └── openai.yaml
```

## Author

GitHub: [kouzt123](https://github.com/kouzt123)

## License

Add your preferred license before publishing.
