# alc-dog-training

[![content validation](https://github.com/astrapi69/alc-dog-training/actions/workflows/validate-content.yml/badge.svg)](https://github.com/astrapi69/alc-dog-training/actions/workflows/validate-content.yml)
[![engine on npm](https://img.shields.io/npm/v/learn-content-engine?label=engine%20on%20npm)](https://www.npmjs.com/package/learn-content-engine)

The [Adaptive Learner](https://github.com/astrapi69/adaptive-learner)
content repository for **Hundetraining** (dog training): a Git repository of
plain lesson files that the app loads directly and no vendor can lock away.

It ships six German-language knowledge sets (domain `knowledge`,
`domain_label` Hundetraining) that form one continuous series on
gewaltfreies Training mit positiver Verstärkung — nonviolent training with
positive reinforcement — from the very first weeks with a puppy (Teil 0) up
to advanced behaviour work (Teil 4). This repository was created from
[adaptive-learner-content-template](https://github.com/astrapi69/adaptive-learner-content-template),
which provides the schema mirror, validator, CI and authoring tooling
described below.

> **Herkunft:** Diese Sets lagen zuvor im Test-/Starter-Repo
> [`adaptive-learner-content-test`](https://github.com/astrapi69/adaptive-learner-content-test)
> (vormals `content-test#54` / `#65`) und wurden in dieses eigenständige
> Content-Repo verschoben.

## The series

Six sets, 23 lessons, source and target language German, content license
CC-BY-SA-4.0. Recommended order:

### Teil 0 — `sets/de/welpen-grundkurs` (A1, 4 Lektionen)

| # | Lesson | Titel |
|---|--------|-------|
| 01 | `01-stubenreinheit.json` | Stubenreinheit |
| 02 | `02-beisshemmung.json` | Beißhemmung und Zähnchen |
| 03 | `03-erste-naechte-ruhe.json` | Erste Nächte, Ruhe und Schlaf |
| 04 | `04-name-bindung-sozialisierung.json` | Name, Bindung und erste Sozialisierung |

### Teil 0+ — `sets/de/welpen-spezial` (A1, 4 Lektionen)

| # | Lesson | Titel |
|---|--------|-------|
| 01 | `01-geraeusche-habituation.json` | Geräusche und Umweltreize |
| 02 | `02-ausruestung-angewoehnen.json` | Halsband, Geschirr und Leine angewöhnen |
| 03 | `03-angstphasen.json` | Angstphasen ruhig begleiten |
| 04 | `04-autofahren-ausfluege.json` | Autofahren und erste Ausflüge |

### Teil 1 — `sets/de/hundetraining-anfaenger` (A1, 3 Lektionen)

| # | Lesson | Titel |
|---|--------|-------|
| 01 | `01-grundlagen-hundeerziehung.json` | Grundlagen der Hundeerziehung |
| 02 | `02-grundkommandos-sitz-platz.json` | Erste Grundkommandos: Sitz und Platz |
| 03 | `03-rueckruf-leinenfuehrigkeit.json` | Rückruf und Leinenführigkeit |

### Teil 2 — `sets/de/hundetraining-aufbau` (A2, 4 Lektionen)

| # | Lesson | Titel |
|---|--------|-------|
| 01 | `01-impulskontrolle-bleib-aus.json` | Impulskontrolle: Bleib und Aus |
| 02 | `02-alleinbleiben.json` | Entspannt allein bleiben |
| 03 | `03-begegnungen-sozialisierung.json` | Begegnungen und Sozialisierung |
| 04 | `04-tricks-beschaeftigung.json` | Tricks und Beschäftigung |

### Teil 3 — `sets/de/hundetraining-alltag` (B1, 4 Lektionen)

| # | Lesson | Titel |
|---|--------|-------|
| 01 | `01-antijagdtraining.json` | Antijagdtraining |
| 02 | `02-maulkorbtraining.json` | Maulkorbtraining |
| 03 | `03-medical-training-tierarzt.json` | Kooperatives Medical Training |
| 04 | `04-notrueckruf-ablenkung.json` | Notrückruf unter Ablenkung |

### Teil 4 — `sets/de/hundetraining-verhalten` (B2, 4 Lektionen)

| # | Lesson | Titel |
|---|--------|-------|
| 01 | `01-leinenreaktivitaet.json` | Leinenreaktivität (Pöbeln an der Leine) |
| 02 | `02-ressourcenverteidigung.json` | Ressourcenverteidigung |
| 03 | `03-frust-uebererregung.json` | Frust und Übererregung |
| 04 | `04-unsicherheit-selbstvertrauen.json` | Unsicherheit und Selbstvertrauen aufbauen |

Each lesson combines theory steps with mixed exercise types (matching,
cloze, free_text, word_tiles, multiselect; Teil 0+ and Teil 4 also use
native `multiple_choice`). Weiterführende Literatur je Reihenteil steht in
[`books.yaml`](books.yaml) (domain `dog-training`).

## What's inside

- `manifest.yaml` — the root manifest listing the six sets above.
- `sets/de/<set>/` — per set: its set manifest plus the lesson JSONs.
- `books.yaml` — recommended reading for the series (domain `dog-training`);
  not a content set, not processed by the validator.
- `schema/` — the pinned [`learn-content-engine`](https://github.com/astrapi69/learn-content-engine)
  schema mirror; [`engine-version.txt`](schema/engine-version.txt) holds the
  pinned engine version (currently `0.12.2`) and is the source of truth. This
  is what the content is validated against — independent of the app.
- `templates/` — starting-point lessons per domain (language / programming /
  knowledge), kept from the template for authoring new lessons.
- `scripts/validate_content.py` — the local validator.
- `scripts/generate_exercises.py` — an optional BYOK AI exercise generator.
- `generated/` — staging area for AI drafts (never shipped directly).
- `.github/workflows/` — CI that validates every push/PR against the pinned engine.
- `docs/` — [GETTING-STARTED.md](docs/GETTING-STARTED.md) and a local
  [LESSON-FORMAT.md](docs/LESSON-FORMAT.md). The **canonical, test-validated**
  format reference is the engine's
  [`docs/lesson-format.md`](https://github.com/astrapi69/learn-content-engine/blob/main/docs/lesson-format.md).

## Quick start

```bash
git clone https://github.com/astrapi69/alc-dog-training.git
cd alc-dog-training

# Validate all sets (needs only Python 3 + these two deps)
pip install pyyaml jsonschema
python3 scripts/validate_content.py        # exit 0 == all sets pass
```

Before you push, `make lint` runs the same semantic engine gate as CI
(`Engine conformance`): it installs the engine release pinned in
`schema/engine-version.txt` into `node_modules/` (gitignored; needs Node.js
and npm) and checks every lesson and manifest with the engine's rule ids
(`E-CARD-REF` & co.). `make lint-warnings` additionally prints the engine
CLI's warnings (`W-*`).

Full authoring walkthrough: [docs/GETTING-STARTED.md](docs/GETTING-STARTED.md).

## Export a set for AI review

`scripts/export_set.py` writes all lessons of ONE set into a single
YAML (or JSON) file so an AI assistant or a human can review the whole
set in one pass (syntax, correctness, consistency across lessons):

```bash
python3 scripts/export_set.py welpen-grundkurs
# -> exports/welpen-grundkurs-de-<timestamp>.yaml
python3 scripts/export_set.py hundetraining-anfaenger --format json --out /tmp/review.json
```

The slug is the set id from the root `manifest.yaml` or the folder name of
the set path; when the same folder name exists under several source-language
directories, `--lang` (default `de`) picks the `sets/<lang>/` directory.
Umlauts stay real UTF-8. An unknown slug aborts with a list of the available
sets. The `exports/` folder is gitignored (read-only snapshot, not a
re-import format).

Full usage guide: [`docs/export-set-usage.md`](docs/export-set-usage.md)
(English) / [`docs/export-set-usage.de.md`](docs/export-set-usage.de.md)
(Deutsch).

## Generate exercises with AI (optional)

`scripts/generate_exercises.py` turns a topic into a lesson with a BYOK
model (Anthropic / OpenAI / Gemini) and gates every draft through
`validate_content.py` before writing it into `generated/`:

```bash
export ANTHROPIC_API_KEY="sk-..."          # or OPENAI_API_KEY / GEMINI_API_KEY
python3 scripts/generate_exercises.py \
  --topic "Rückruf unter Ablenkung aufbauen" \
  --target-lang de --source-lang de --set-id hundetraining-alltag
```

A draft is a draft until you review it — no validator catches a claim that
is factually wrong about dog behaviour or training method.

## How it stays current

The content is validated against the **pinned** engine version in
`schema/engine-version.txt` on every push and pull request (structural +
semantic + drift gates in `.github/workflows/`). A green CI means the
content is valid for every consumer of that engine release. When the
engine is bumped, it reaches this repository the same way it reaches the
rest of the chain: a deliberate pin-bump PR that the drift gate guards.

The tooling is licensed MIT (see [LICENSE](LICENSE)); the lesson content
carries its own license, CC-BY-SA-4.0, declared in each set manifest's
`metadata.license`.
