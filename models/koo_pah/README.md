# Koo Pah microWakeWord Model
Downloaded from https://microwakeword.com

## What's in this Folder
  koo_pah.tflite    — TFLite model (the trained wake word)
  koo_pah.json      — ESPHome manifest (points at the .tflite)

Keep both files together. The manifest references the .tflite
by relative path (koo_pah.tflite); renaming or separating them
will break the model.

## How to use it with ESPHome
1. Add this snippet to your existing device YAML:

       micro_wake_word:
         models:
           - model: https://raw.githubusercontent.com/Loic760/microwakeword-keywords/main/models/koo_pah/koo_pah.json

2. Recompile and flash: esphome run your_device.yaml

Requires ESPHome 2024.7.0 or newer. Your microphone must be
configured at 16 kHz (the default for voice_assistant and most
ESP32 mic setups).

## Tuning
The model manifest includes default values in the "micro" section. You
can also override these in ESPHome YAML:

      micro_wake_word:
        models:
          - model: https://raw.githubusercontent.com/Loic760/microwakeword-keywords/main/models/koo_pah/koo_pah.json
            probability_cutoff: 90%
            sliding_window_size: 5

For local testing, copy koo_pah.json and koo_pah.tflite into the same
folder as your ESPHome device YAML, then use:

      micro_wake_word:
        models:
          - model: koo_pah.json

Open koo_pah.json and edit the "micro" section only if you want to
change the defaults in the repository. In JSON these values are floats;
in ESPHome YAML overrides, use percentages such as `90%`.

  probability_cutoff           Lower = more sensitive (more false
                               accepts). Higher = stricter (may miss
                               real triggers). Current: 0.5.
                               Try values in the 0.90–0.99 range.

  sliding_window_size          Frames averaged before deciding.
                               Bigger = smoother but slower to react.
                               Current: 5.

Leave feature_step_size and tensor_arena_size as delivered — they
match how this model was trained; changing them will break it.

## Help
  ESPHome docs: https://esphome.io/components/micro_wake_word/
  This service: https://microwakeword.com
