# Textfilters

Composable TypeScript text filtering primitives for moderation pipelines.

Textfilters is a small set of composable TypeScript text filtering primitives for moderation pipelines. This repository is documentation-only and provides the ecosystem overview for the current package set.

## Packages

| Package | Repository | Status | Purpose |
| --- | --- | --- | --- |
| `@textfilters/core` | `textfilters/core` | `0.1.0` on GitHub Packages | Shared contracts and pipeline utilities. |
| `@textfilters/url` | `textfilters/url` | `0.1.0` on GitHub Packages | URL and obfuscated-link filtering. |
| `@textfilters/phone` | `textfilters/phone` | `0.1.0` on GitHub Packages | Phone-like sequence filtering. |
| `@textfilters/profanity` | `textfilters/profanity` | `0.1.0` on GitHub Packages | Profanity filtering primitives. |
| `@textfilters/spam` | `textfilters/spam` | `0.1.0` on GitHub Packages | Lightweight in-memory spam guard primitives. |

All current packages are published to GitHub Packages as `0.1.0`.

## Installation

Packages are published to GitHub Packages, not the public npm registry.

```ini
@textfilters:registry=https://npm.pkg.github.com
```

GitHub Packages requires npm authentication for installs, including public packages.

```sh
npm install @textfilters/core @textfilters/url @textfilters/phone @textfilters/profanity @textfilters/spam
```

## Usage

```ts
import { createTextPipeline } from "@textfilters/core";
import { filter as urlFilter } from "@textfilters/url";
import { filter as phoneFilter } from "@textfilters/phone";
import { filter as profanityFilter } from "@textfilters/profanity";

const pipeline = createTextPipeline()
  .use(urlFilter)
  .use(phoneFilter)
  .use(profanityFilter);

const safeText = pipeline.censor("message with https://example.com and +7 999 123-45-67");
```

```ts
import { createSpamFilter } from "@textfilters/spam";

const spam = createSpamFilter({
  minIntervalMs: 700,
  duplicateWindowMs: 12_000,
  burstWindowMs: 10_000,
  burstMaxMessages: 6,
});

const decision = spam.check({
  actorKey: "user:123",
  text: "hello",
});
```

## Release Model

Packages use semantic versioning. Packages are published to GitHub Packages first, with GitHub Releases and immutable release tags using `vX.Y.Z`. npmjs.org publication may be added later.

## Support

Open package-specific bugs in the relevant package repository. Open ecosystem documentation issues in this repository. For security reports, see the organization security policy in `textfilters/.github`.

## Roadmap

Planned future packages:

* `@textfilters/email` - email address and obfuscated-email filtering.

## License

MIT
