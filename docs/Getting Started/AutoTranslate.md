---
sidebar_position: 2
---

# Auto translate using Lingo

[Lingo.dev](https://lingo.dev/) is an AI-powered localization and internationalization platform aimed at developers and engineering teams who want to make their web/mobile apps multilingual.

## Creating a Lingo.dev account & API Key

Visit [Lingo login page](https://lingo.dev/en/auth) to authenticate.<br/>
After authenticating <br />

1. Click on `Projects`.
2. Create a new project if you don’t already have one.
3. Select your project.
4. Open the `Settings` tab.
5. Copy your `API Key`.

## Put your API key in the `.env` file before running the Lingo CLI.

```js
LINGODOTDEV_API_KEY=<API_KEY>
```

## Running Lingo cli

```txt
 npx lingo.dev@latest init
```

1. Choose your default language.
2. Your target languages want to translate, seprated by commas.
3. File format for you translation files like json, yaml etc.
4. Default path for i18n/[locale].json

This action will create an `/i18n/en.json` file. This file contains `key:value` pairs that define which keys should be translated and their corresponding text.

```json
{
  "greeting": "This text of your component will be translated by Lingo.dev" //you will see something different
}
```

It will also create an i18n.json file, which contains all the configuration for your translations, such as the source language, target languages, and other settings.

```json
{
  "version": "1.10",
  "locale": {
    "source": "en",
    "targets": ["hi", "de", "zh", "ja", "ko", "es"] //add targets as per your wish
  },
  "buckets": {
    "json": {
      "include": ["i18n/[locale].json"]
    }
  },
  "$schema": "https://lingo.dev/schema/i18n.json"
}
```

## Running the translation job (generate target JSONs)
```json
npx lingo.dev@latest run
```

This command will create target files with their respective translations. For example, `i18n/hi.json` will contain the Hindi translation, like this:
```json
{
  "greeting": "आपके कंपोनेंट का यह टेक्स्ट Lingo.dev द्वारा अनुवादित किया जाएगा"
}
```

In Next Chapter, will will learn how to translate our rangoli component with lingo.dev