# Contributing

:wave: Hello there! :tada: Thanks for taking the time to contribute!

Seen something outdated or plain wrong? Spotted a typo somewhere? Think something could be better translated, or want to translate the whole deck into a new language? Awesome! :100: Let us now right away by [opening a new issue](https://github.com/axelboc/anki-ultimate-geography/issues).

#### Table of contents

[Contributor's guide](#contributors-guide)

- [Set-up](#set-up)
- [Build and import](#build-and-import)
- [Indexing](#indexing)
- [Quotes normalisation](#quotes-normalisation)

[Content guidelines](#content-guidelines)
  - [_Country_ field](#country-field)
  - [_Flag similarity_ field](#flag-similarity-field)
  - [Translation sources](#translation-sources)

[Maintainer's guide](#maintainers-guide)

- [Versioning](#versioning)
- [Release process](#release-process)


## Contributor's guide

Ready to start working on an issue? Here is what you need to know.

- If you're new to contributing on GitHub, [read this guide](https://guides.github.com/activities/contributing-to-open-source/) first.
- The deck is managed with [Anki Deck Manager](https://github.com/OnkelTem/anki-dm). The project's documentation explains the file structure in details, but the most important file is `data.csv`. It contains the actual content of the deck, including translations. In most cases, this is the only file you'll need to work on.
- If you add a new row to `data.csv`, make changes to other files, or would like to review the changes you made to the deck in Anki, you'll need to set up and use Anki Deck Manager.

### Set-up

1. Install the [CrowdAnki add-on](https://github.com/Stvad/CrowdAnki) in Anki.
1. Fork and clone this repository on your machine.
1. With the help of your favourite command-line package manager (e.g. `brew`, `chocolatey`, `apt-get`), install [PHP 7](http://php.net/) and [Composer](https://getcomposer.org/download/).
1. From the root of the project, run `composer install` to install Anki Deck Manager.

### Build and import

From here, building the deck is as simple as running `composer build`. Anki Deck Manager builds the deck into the `build` folder, in a format that CrowdAnki understands, which you can then import into Anki.

### Indexing

Anki requires each note to have a unique identifier. When you add a note to the deck, that is, when you add a row to `data.csv`, make sure to leave the first column empty. Then, tell Anki Deck Manager to re-index the deck by running `composer index`. The note you added will receive an identifier.

### Quotes normalisation

Anki Deck Manager has a very specific way of wrapping fields with double quotes in `data.csv` to escape special characters (cf. [#129](https://github.com/axelboc/anki-ultimate-geography/issues/129)). Whether you edit the file by hand or through an editor, chances are you won't end up with double quotes in the same places. If you commit the file as is, the diff will be cluttered with changes that have nothing to do with your edits. To avoid this, run `composer index` before committing your changes. This command has the side effect of normalising the escaping of fields in the entire file.

### Content guidelines

#### _Country_ field

The correct name to use for a given country or territory in each language is not always clear. This usually occurs in two cases:

- when the official name is changed but the old name remains more frequently used (in the media and in everyday conversation) - e.g. _Ivory Coast_ vs. _Côte d'Ivoire_;
- when the official name is simply shortened in everyday use - e.g. _China_ vs. _People's Republic of China_.

Unless otherwise stated in [`TRANSLATION_SOURCES.md`](https://github.com/axelboc/anki-ultimate-geography/blob/master/TRANSLATION_SOURCES.md), we take **the title of the Wikipedia article** for the country, in the language of the given deck. Alternative names may be mentioned in the _Country info_ field, when relevant.

If the title of the Wikipedia article contains a parenthetical portion for disambiguation purposes, it must be removed, except in the very unlikely case that two countries share the same name in a given language — e.g. _Saint-Martin (Antilles françaises)_ and _Saint-Martin (royaume des Pays-Bas)_ in the French deck.

Country names must not be preceded by articles, particularly in gendered languages (French, German, etc.) unless Wikipedia indicates otherwise - e.g. _United Kingdom_, _The Gambia_. This rule also applies to the _Flag similarity_ field, but not to other fields in which country names are used in sentences.

> To understand the reasoning behind these decisions, see [#181 (Wikipedia as source)](https://github.com/axelboc/anki-ultimate-geography/issues/181), [#212 (disambiguating country names)], and [https://github.com/axelboc/anki-ultimate-geography/pull/157#issuecomment-549143860 (no gender articles)].

#### _Country info_ field

To help with memorisation and provide context while learning, this field may contain:

- governance information - e.g. _Overseas territory of the United Kingdom_ (Cayman Islands)
- statehood information - e.g. _Independent state claimed by Moldova_ (Transnistria)
- alternative and former country names - e.g. _Also known as Timor-Leste_ (East Timor)
- in rare cases only, general knowledge information - see Melanesia for an example

The content of this field should be concise and consistent across notes. It may differ between languages, notably when dealing with alternative names.

#### _Capital_ field

Unless otherwise stated in [`TRANSLATION_SOURCES.md`](https://github.com/axelboc/anki-ultimate-geography/blob/master/TRANSLATION_SOURCES.md), we use the capital given in the [infobox](https://en.wikipedia.org/wiki/Template:Infobox_country#Examples) of the Wikipedia article for the country, in the language of the given deck.

If the title of the Wikipedia article contains a parenthetical portion for disambiguation purposes, it must be removed. The _Capital hint_ field is used instead for disambiguation.

If a capital has alternative names, we take **the title of the Wikipedia article** for the capital, in the language of the given deck. This corresponds typically to the name used in the infobox of the country's Wikipedia article. Alternative names may be mentioned in the _Capital info_ field, when relevant.

If multiple capitals are listed in a country's infobox, the following guidelines apply:

- If the first capital is followed by a qualifier such as "official", "constitutional", "de jure", "claimed", or "political", it must be used alone in the _Capital_ field. The _Capital info_ field must then be used to detail the status and/or role of every capital - e.g. _While Dodoma is the official capital, Dar es Salaam is the de facto seat of government._
- If government branches such as "executive" or "legislative" are the only qualifiers used, then the capitals must all be listed in the _Capital_ field, separated by commas - e.g. _Pretoria, Cape Town, Bloemfontein_ (South Africa). The _Capital info_ field must again be used to detail the role of every capital.
- If no qualifiers are provided at all, then the capitals must all be listed in the _Capital_ field, separated by commas - e.g. _Santa Cruz de Tenerife, Las Palmas_ (Canary Islands). A concise explanation should then be provided in the _Capital info_ field.

#### _Capital info_ field

As explained in the previous section, this field is typically used for countries with multiple capitals, to clarify the role and/or status of each capital, or to explain succinctly why the country has multiple capitals.

#### _Capital hint_ field

This field is used in notes that share:

- the same exact capital - e.g. _London_ (United Kingdom and England);
- capitals with very similar names - e.g. _Georgetown_ and _George Town_.

The hints appear on _Capital - Country_ cards to avoid confusion or random guesses. They should
convey as little information as possible to not give away the answers.

#### _Flag_ field

This field must contain a single HTML image element pointing to the SVG or PNG image of a flag - e.g. `<img src="ug-flag-seychelles.svg" />`. The image must be placed in the ` media` folder and named `ug-flag-<country_name>.<svg|png>`. SVG is the preferred format.

SVG flags are sourced from [Wikimedia](https://commons.wikimedia.org/). We use the flag that is presented in the [infobox](https://en.wikipedia.org/wiki/Template:Infobox_country#Examples) of the English Wikipedia article for the country. The flag's source URL and licence must be documented in `sources.csv`.

The following guidelines apply to flag images:

- The `viewBox`, `width` and `height` attributes are required.
- The height must be set to 250 px (`height="250"`) and the width adjusted proportionally.
- Each flag must be optimised with [SVGO](https://jakearchibald.github.io/svgomg/).
- SVG flags larger than 50 kB must be exported to PNG (still with a height of 250 px) and optimised with a tool like [PNGGauntlet](https://pnggauntlet.com/).

If the name of a country appears clearly on a flag, a second version of that flag may also be provided, with the name of the country blurred out. The name should be blurred using [Inkscape](https://inkscape.org/)'s Gaussian blur effect as explained in #247. The blurred flag must be named `ug-flag-<country_name>-blur.<svg|png>` and placed in the `media` folder. A second HTML element must then be added to the _Flag_ field _before_ the existing HTML element. This allows the blurred flag to appear on the front of the country's _Flag - Country_ card.

#### _Flag similarity_ field

This field is used in the _Flag - Country_ template.

In Anki, when you keep on confusing two flags, you can't put them side by side to learn their visual differences. The _Flag similarity_ field works around this limitation by providing a concise description of the differences a flag has with another. It allows users to more easily learn to distinguish pairs of similar flags and perhaps come up with mnemonics to remember their respective countries.

A note's _Flag similarity_ field contains a list of countries, each followed by a list of differences. For instance, the flag similarities for Iceland are written as follows: _Norway (red background, blue cross), Faroe Islands (white background, red and blue cross)_. The list of differences must be **precise**, **clear**, and **concise**. Advanced [vexillological](https://en.wikipedia.org/wiki/Vexillology) terms should be avoided.

Flag similarities are always **mutual**: if flag A is similar to flag B, then flag B is similar to flag A. To determine whether two flags are similar enough to warrant mutual _Flag similarity_ information, their differences must first be **identified** and **classified**. The following classification applies:

- **Critical differences (C)**
  - presence/absence of decoration - e.g. symbol, coat of arms
- **Major differences (M)**
  - same colours in different positions (e.g. two swapped, three rotated)
  - decorations of different types in same position (e.g. symbol vs. coat of arms)
  - decorations of same type in different positions (e.g. star(s) above/below band for Curaçao/Nauru)
- **Minor differences (m)**
  - slightly different colours (e.g. shade of blue, red vs. maroon, darker green)
  - slightly different geometry (e.g. width, number of serrated edges for Qatar/Bahrain, size of canton)
  - different decoration of same type in same position (e.g. different symbol, different coat of arms)
  - decorations of same type in different amounts (e.g. fewer stars)
  - decorations of same type with different colours (e.g. white vs. red stars for Australia/New Zealand)
- **Negligible differences (n)**
  - subtly different colours - i.e. [ΔE](https://github.com/axelboc/anki-ultimate-geography/issues/50#issuecomment-525902404) < 30
  - subtly different geometry

Two flags are then eligible for _Flag similarity_ information when they respect the two rules below:

- Their differences all fit in the above classification. For instance, France and Italy are not eligible because their left bands are respectively blue and green, and "different colours in same position" does not appear in the classification.
- Their classified differences form one the following combinations:
  - `1C 0M 0m {0+}n` = one critical difference and any number of negligible differences
  - `0C 1M {0–2}m {0+}n` = one major difference, up to two minor differences, and any number of negligible differences
  - `0C 0M {0–3}m {0+}n` = up to three minor differences and any number of negligible differences

Critical, major, and minor differences should be listed in the _Flag similarity_ field. Negligible differences should be listed only when relevant, notably when two flags share nothing but negligible differences.

#### _Map_ field

This field must contain a single HTML image element pointing to the PNG image of a map - e.g. `<img src="ug-map-seychelles.png" />`. The image must be placed in the ` media` folder and named `ug-map-<country_name>.png`. PNG is the preferred format.

The source SVG maps come, or are inspired, from the [SVG locator maps](https://commons.wikimedia.org/wiki/Category:SVG_locator_maps_of_countries_(16:9_regional_location_map_scheme)) project on Wikimedia. The maps' source URLs and licences must be documented in `sources.csv`.

The following guidelines apply to map images:

- The maps must be sourced or created as SVG, exported to PNG, and then optimised with a tool like [PNGGauntlet](https://pnggauntlet.com/).
- They should have a width of 500 px and a height of approximately 281 px.
- The style (colours, strokes, etc.) should match that of existing maps in the deck (note that water bodies use a different style than countries).
- For small islands or archipelagos, the map should include a zoom box to facilitate identification.

### Translation sources

If you are contributing a new language, please add any sources to [`TRANSLATION_SOURCES.md`](https://github.com/axelboc/anki-ultimate-geography/blob/master/TRANSLATION_SOURCES.md), also explaining any stylistic choices.

If you are changing the style or content of an existing translation significantly, please update the sources and explanations.

## Maintainer's guide

### Versioning

The releases follow a versioning scheme of the form `x.y`, where:

- `x` increases in the case of a **major, breaking release** (e.g. v3.0),
- `y` increases in the case of a **minor, non-breaking release** (e.g. v2.6).

Content changes, such as adding or removing a note, replacing an image, or translating the deck into a new language, all constitute minor changes. A change is considered major when users are likely to **lose a significant part of their progress** when upgrading the deck with CrowdAnki (cf. [_Upgrading_](README.md#upgrading) section of README).

### Release process

1. Bump the version in `desc.html` and commit the change.
1. Run `composer index && composer build`.
1. Add each folder in the `build` directory to a separate ZIP archive named as follows:
  - `Ultimate Geography` ==> `Ultimate_Geography_v[x.y]_EN.zip`.
  - `Ultimate Geography [Extended]` ==> `Ultimate_Geography_v[x.y]_EN_EXTENDED.zip`.
  - `Ultimate Geography_de` ==> `Ultimate_Geography_v[x.y]_DE.zip`.
  - `Ultimate Geography [Extended]_de` ==> `Ultimate_Geography_v[x.y]_DE_EXTENDED.zip`.
1. In Anki, synchronise all your devices then import the folder of the standard English deck with CrowdAnki (i.e. `Ultimate Geography`). For major versions, make sure to perform a [clean import](README.md#major-version). Synchronise all your devices again once the import is complete.
1. Export the deck as an APKG package named `Ultimate_Geography_v[x.y]_EN.apkg`, making sure to exclude scheduling information but include all media.
1. Write the release notes on GitHub.
1. Attach the APKG file as well as all the ZIP files to the release and publish it.
1. Go to [AnkiWeb](https://ankiweb.net/decks/).
1. Find the _Ultimate Geography_ deck and select _Actions_ > _Share_
1. Update the version number in the title and the description if needed.
1. Enter the full legal name and click _Share_.
1. Close the milestone in GitHub and create a new one for the next version.
