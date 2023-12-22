# Custom sentences for Home Assistant

This repository is a collection of community custom sentences and intents for the Home Assistant voice assistant Assist.

## How to use

If you've set your eyes on an intent or custom sentence that you want to use, do the following:

- copy the `custom_sentences/<xx>/<intent_handler>.yaml` file to your `/config` folder, under the same folder structure
- if it's not a built-in intent, copy the `custom_intents/intent_handler.yaml` file in your `/config` folder, under the same folder structure
- if you have already defined some custom intents, follow the [instructions below](#MigratingYourCustomIntents)
- update your `configuration.yaml` file to contain

```yaml
# /config/configuration.yaml
conversation:
intent_script: !include_dir_merge_named custom_intents
```

- restart Home Assistant core

Now your new sentences/intents should work when using them inside your voice assistant

### Migrating your custom intents

If you've already defined some custom intents and want to add others from this repo, you must move the intents from `configuration.yaml` to a dedicated file. Let's say this is in your `configuration/yaml` file

```yaml
# /config/configuration.yaml
intent_script:
  MyIntent:
    action:
      service: my.service
    speech:
      text: "I've called my service"
```

Create a file called `/config/custom_intents/default.yaml` and move everything that's under `intent_script:` in `configuration.yaml`, but unindent the resulting dictionary so that it's on the first level in the file.

```yaml
# /config/custom_intents/default.yaml
MyIntent:
  action:
    service: my.service
  speech:
    text: "I've called my service"
```

Next, edit `configuration.yaml` and alter the `intent_script:` key

```yaml
# /config/configuration.yaml
intent_script: !include_dir_merge_named custom_intents
```

At the end, reload the `Intent script` configuration from the [Developer tools](https://my.home-assistant.io/redirect/server_controls/). You're done!

## How to contribute

### Custom intents

To add custom intents, add a filed called `custom_intents/intent_handler.yaml`, where `intent_handler` is the [snake_case](https://en.wikipedia.org/wiki/Snake_case) notation of the intent name (e.g. `ExampleIntent` -> `example_intent`)

The file structure is that described in the Home Assistant docs for [intent script](https://www.home-assistant.io/integrations/intent_script/)

```yaml
# Make a short description of what the intent does
IntentHandler: # Change this to your own intent name
  speech:
    text: "This is a custom response"
```

### Custom sentences for existing intents

If you want to add sentences for either a built-in Home Assistant intent or for a custom one, you should add/edit the `custom_sentences/<xx>/<intent_handler>.yaml` file, where:

- `xx` is the language code (e.g. `en` for English)
- `intent_handler` is the [snake_case](https://en.wikipedia.org/wiki/Snake_case) notation of the intent name (e.g. `ExampleIntent` -> `example_intent`)

The file structure is that described in the Home Assistant docs for [custom sentences](https://www.home-assistant.io/integrations/conversation/#adding-custom-sentences)

```yaml
language: "xx" # Replace this with an actual language code
intent_script:
  IntentHandler: # Change this to an actual intent key
    data:
      - sentences:
          - "a sentence that triggers the intent"
          - "with [optional] placeholders (and|or) {lists}" # as per the syntax described here https://developers.home-assistant.io/docs/voice/intent-recognition/template-sentence-syntax
lists:
  list_name:
    values:
      - value1
      - in: "(second value|value2)"
        out: value2
```

You will need to add as many files as you have translations for your sentences.

### Translations

If you see an intent that you'd like to use, but it's not translated in your language, please consider doing so for everybody. Let's say you like the English sentences in `custom_sentences/en/<intent_handler>.yaml` and you'd like to translated them to French. Just create a file called `custom_sentences/fr/<intent_handler>.yaml` and copy the structure from `en`, making the following modifications:

```yaml
language: "fr" # Replace this with the language code for your actual language, if it's not French
intent_script:
  IntentHandler:
    data:
      - sentences:
          - "french translation of the sentence" # Translate here
lists:
  list_name:
    values:
      - value1 # this should NOT be translated, but you could do this
      #     - in: "value 1 in french"
      #       out: value1
      - in: "(second value|value2)" # this should be translated
        out: value2 # but NOT this
```
