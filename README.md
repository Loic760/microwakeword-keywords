# microWakeWord Keywords

Personal microWakeWord model collection for ESPHome.

## Models

| Wake word | Manifest | ESPHome model line |
| --- | --- | --- |
| Hey Gabbie | `models/hey_gabbie/hey_gabbie.json` | `- model: https://raw.githubusercontent.com/Loic760/microwakeword-keywords/main/models/hey_gabbie/hey_gabbie.json` |
| Koo Pah | `models/koo_pah/koo_pah.json` | `- model: https://raw.githubusercontent.com/Loic760/microwakeword-keywords/main/models/koo_pah/koo_pah.json` |

## ESPHome Usage

If your ESPHome YAML already has a `micro_wake_word:` block, add one or more of these lines under `models:`:

```yaml
    - model: https://raw.githubusercontent.com/Loic760/microwakeword-keywords/main/models/hey_gabbie/hey_gabbie.json
    - model: https://raw.githubusercontent.com/Loic760/microwakeword-keywords/main/models/koo_pah/koo_pah.json
```

Full minimal block:

```yaml
micro_wake_word:
  models:
    - model: https://raw.githubusercontent.com/Loic760/microwakeword-keywords/main/models/hey_gabbie/hey_gabbie.json
    - model: https://raw.githubusercontent.com/Loic760/microwakeword-keywords/main/models/koo_pah/koo_pah.json
```

Do not use a normal GitHub `blob` page URL. ESPHome supports the `github://` shorthand above and full raw URLs.

The full raw URLs are:

```text
https://raw.githubusercontent.com/Loic760/microwakeword-keywords/main/models/koo_pah/koo_pah.json
https://raw.githubusercontent.com/Loic760/microwakeword-keywords/main/models/hey_gabbie/hey_gabbie.json
```

The equivalent GitHub shorthands are:

```yaml
    - model: github://Loic760/microwakeword-keywords/models/hey_gabbie/hey_gabbie.json@main
    - model: github://Loic760/microwakeword-keywords/models/koo_pah/koo_pah.json@main
```

## Collection Layout

Each wake word lives in its own folder:

```text
models/
  hey_gabbie/
    hey_gabbie.json
    hey_gabbie.tflite
  koo_pah/
    koo_pah.json
    koo_pah.tflite
```

Keep each JSON manifest next to its `.tflite` file. The manifest's `model` field is a relative path, so moving one without the other will break ESPHome downloads.

When adding another wake word:

1. Create `models/<keyword_slug>/`.
2. Put `<keyword_slug>.json` and the matching `.tflite` model in that folder.
3. Set the JSON `model` field to the local TFLite filename, for example `"my_keyword.tflite"`.
4. Add the new model line to the table above.
