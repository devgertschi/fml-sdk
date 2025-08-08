# FML: Freeform Markup Language v0.1

## Overview
Freeform Markup Language (FML) is a lightweight, expressive markup language designed to write prompts for large language models (LLMs) using structured XML-style tags and Mustache-style variables. It’s designed for developers who want readable, reusable, and modular prompts without the chaos of raw strings.

## Features

- 🧩 Mustache-style variable interpolation: `{{ name }}`
- 🔁 `<include>` tag for nesting other `.fml` files
- 🧪 Simple, testable, and transformable prompt formats

## 📦 Installation

```bash
npm install @devgertschi/fml-sdk
```

## Syntax

### Tags
FML uses angle-bracketed XML-style tags:

| Tag | Purpose |
| -- | -- |
| `<include src="..."/>` | Imports other `.fml` files |

```xml
<system>
  You are a helpful assistant.
</system>

<user>
  Hello, what can you do?
</user>

<assistant>
  I can help with a variety of tasks including answering questions and writing code.
</assistant>
```

### Variables
Use `{{ variable_name }}` syntax for dynamic substitution:

```
Tell me a story about {{ animal }} who learns to {{ skill }}.
```

###  File Composition
Modularize prompts using `<include>`:

```xml
<include src="common/system-prompt.fml" />
Hello there!
```

### BBCode Tag Style

You can configure the parser to use BBCode-style tags (e.g., [include src="..." ]) instead of XML-style tags by passing the `tagStyle` option:

```ts
import { parseFML } from '@devgertschi/fml-sdk';

const message = await parseFML('bbcode-include.fml', undefined, { tagStyle: 'bbcode' });
```

Example BBCode-style FML:

```
[include src="common/system-prompt.fml"]
Hello there!
```

## Example

```ts
import { parseFML } from 'fml-sdk'

const message = await parseFML('onboarding-prompt.fml', {
  variables: { name: 'David' }
})
```

## File Format

- Extension: `.fml`
- UTF-8 encoding

---

Built with ❤️ by [David Pichsenmeister](https://pichsenmeister.com) to make prompting a bit more human.

Heard about in a talk @viennajs, tried, forked and probably improved by [devgertschi](https://gertschi.dev).
