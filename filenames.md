---
title: Filenames for audio files
---

This guide contains recommendations for naming audio files containing
ecoacoustic recordings.

One format makes it easier for everyone to write software once
that works for everyone. It encourages collaboration and interoperability.
This is important for researchers, platforms, and tools alike.

## Recommended Format

Our recommended format is:

```txt
{Date}[_{SiteName}][_{...other}].{Extension}
```

Valid examples of this format include:

```txt
20210901T120000Z_SiteName_123456.flac
20170625T102105+1000_Oxley-creek_-12.345+127.789.wav
20170625T102105.123456+0930.wav
```

We'll explain each part of the format below.

> [!Note]
> Most tools and platforms don't output filenames in this format yet.
> However, Ecosounds and EMU are two tools that do.

The choices made in this document are designed, in priority order, to:

1. be safe for use in most operating systems and shells
2. follow existing standards where possible
3. be easy to read by humans
4. be easy to parse by computers
5. be compact
6. be naturally sortable

## Special characters

Filenames **MUST NOT** contain special characters, including those that are
commonly interpreted by shells (like Bash, PowerShell, or CMD).

Filenames:

- **MUST NOT** contain any of the following characters:
  - Any non printable characters (e.g. null, backspace, tab, newline, etc)
  - `*` (asterisk)
  - `?` (question mark)
  - `[` (left square bracket)
  - `]` (right square bracket)
  - `{` (left curly brace)
  - `}` (right curly brace)
  - `\` (backslash)
  - `/` (forward slash)
  - `|` (pipe)
- **SHOULD NOT** contain:
  - Any leading or trailing whitespace
  - Single (`'`) or double (`"`) quotes
  - Spaces
- **MAY** contain:
  - Alphanumeric characters (A-Z, a-z, 0-9)
  - Hyphens (`-`)
  - Underscores (`_`)
  - Periods (`.`)

Spaces **MAY** be used, but are **NOT RECOMMENDED**. If a filename needs to be
converted to remove spaces, then spaces **SHOULD**
be replaced with hyphens (`-`).

For example:

```diff
- 20170625T102105_Oxley creek.wav
+ 20170625T102105_Oxley-creek.wav
```

## Extensions

A filename **MUST** end with a valid audio file extension, such as:

- `.flac`
- `.wav`
- `.mp3`

## Components

You **MUST** separate components of the filename with an underscore (`_`).

For example:

```diff
- 20170625T102105Oxley creek.wav
+ 20170625T102105_Oxley-creek.wav
```

## Dates

The most important part of a filename is the date and time the recording started.
We recommend using an [ISO8601](https://en.wikipedia.org/wiki/ISO_8601)
format for all date and time information (everywhere,
not just in filenames). ISO8601 is an international standard for the representation
of dates and times.

For filenames though, you **MUST** use the _basic_ format of ISO8601, which
does not include any separators (e.g. hyphens or colons). This produces a
more compact datestamp and avoids any issues with special characters (mainly `:`)
in filenames.

Filenames **SHOULD** contain a UTC offset (see below) to avoid ambiguity about the
time the recording started. Filenames **MAY** use `Z` to indicate UTC+0.

Examples of the recommended format follow:

```txt
20170625T102105Z.flac
20250990T033235.123456+0930.wav
20250990T033235-0430.wav
```

Variations of this format **MAY** omit the UTC offset, e.g. `20170625T102105.flac`
but this is **NOT RECOMMENDED** because the datestamp becomes ambiguous.

### Precise format

The precise format for the date and time is: `YYYYMMDDThhmmss[.SSSSSS][Z|(+|-)hhmm]`.
Where:

| Code       | Meaning                                                             |
| ---------- | ------------------------------------------------------------------- |
| YYYY       | A 4 digit year                                                      |
| MM         | A 2 digit month, with leading zeros                                 |
| DD         | A 2 digit day, with leading zeros                                   |
| T          | A separator between the data and time components                    |
| hh         | Hours, 0-24, with leading zeros                                     |
| mm         | Minutes, with leading zeros                                         |
| ss         | Seconds, with leading zeros                                         |
| SSSSSS     | [Optional] Fractional seconds (up to 6 digits)                      |
| Z          | [Optional] UTC+0 designator                                         |
| (+\|-)hhmm | [Optional] UTC offset in hours and minutes, positive if east of UTC |

## Locations

It is **recommended** to encode location information inside the metadata of
audio files rather than in filenames.

However, if you do need to encode location, then filenames **MUST** use
[ISO6709:H](<https://en.wikipedia.org/wiki/ISO_6709#String_expression_(Annex_H)>)
without a trailing solidus to represent locations in filenames.
We omit the trailing solidus (`/`) to avoid special characters in filenames.

The precise format is: `(+|-)<Latitude>(+|-)<Longitude>[[+|-]<Altitude>][<CRS>]`
, where:

| Code      | Meaning                                                   |
| --------- | --------------------------------------------------------- |
| Latitude  | Latitude in decimal degrees, DD.DDDDDD                    |
| Longitude | Longitude in decimal degrees, DDD.DDDDDD                  |
| Altitude  | Altitude in meters above sea level (optional)             |
| CRS       | Coordinate Reference System (optional, default is WGS84). |

- Implementers **MUST** use only decimal degrees.
  - **DO NOT** use degrees, minutes, seconds.
- Implementers **MUST** use a leading sign (`+` or `-`) for both latitude and longitude.
- Consumers **MUST** assume the WGS84 datum, unless otherwise specified in
  the metadata.
- Altitude **MAY** be included, but is not required.
  - If included, altitude **MUST** be in meters above sea level, with a
    leading sign (`+` or `-`).
- Latitude **MUST** be formatted with a leading sign (`+` or `-`).
- Latitude **MUST** be formatted with 2 digits before the decimal point, including a leading zero if necessary.
- Longitude **MUST** be formatted with a leading sign (`+` or `-`).
- Longitude **MUST** be formatted with 3 digits before the decimal point, including a leading zeros if necessary.
- Altitude **MUST** be formatted with a leading sign (`+` or `-`) when included.
- The CRS **SHOULD** be presented as a EPSG code, prefixed with `CRS`
  - e.g. `CRSWGS_84` for WGS84

For example, an audio file with the latitude `-39.5336`, and longitude of `+131.2711`
would be encoded in the filename as:

```txt
-39.533600+131.271100
```

Valid examples in filenames include:

```txt
20170625T102105+1000_-12.345000+127.456000.wav
20170625T102105+1000_+02-009.wav
20170625T102105+1000_-12.345-127.456+30.wav
20170625T102105+1000_-12.345000+127.456000+30CRSWGS_84.wav
20170625T102105+1000_+0+0.flac
```

## Alternative Date & Time Formats

Open Ecoacoustics maintains a tool, EMU, that can parse a variety of date and
time formats from filenames. The full list of supported formats can be found
in EMU's test fixtures: <https://github.com/QutEcoacoustics/emu/blob/master/test/Fixtures/FileNameParsingFixtures.csv>

Alternative formats **SHOULD NOT** be used, but we recognise that many formats
are already in use. EMU supports the following alternative formats and can convert[^1]
them to the recommended format.

| Format                       | Example                          | Commonly Produced By | Comments                                                 |
| ---------------------------- | -------------------------------- | -------------------- | -------------------------------------------------------- |
| `YYYYMMDD_hhmmss`            | `20170625_102105.wav`            | Wildlife Acoustics   |                                                          |
| `YYYYMMDD_hhmmss_SSS`        | `20170625_102105_010.wav`        | Wildlife Acoustics   |                                                          |
| `{HEX_ENCODED_UNIX_EPOCH}`   | `5B07C752.wav`                   | Audio moth           |                                                          |
| `YYYYMMDD-hhmmss`            | `20100503-080000.wav`            |                      |                                                          |
| `YYYYMMDD$hhmmss`            | `20180221$031609.wav`            | Wildlife Acoustics   |                                                          |
| `YYYYMMSS*hhmmss*`           | `20170704*104849*.wav`           |                      |                                                          |
| `YYYYMMDDhhmmss`             | `20070415051314.wav`             |                      |                                                          |
| `YYYYMMDDThhmmss`            | `20091219T070006+1000.wav`       | Frontier Labs        |                                                          |
| `YYYYMMDDThhmmss.SSSSSS`     | `20161108T075126.123456.wav`     | Frontier Labs        |                                                          |
| `YYYYMMDD`                   | `20131012.wav`                   |                      | While understood, this format is too ambiguous           |
| `yyMMDD_hhmm`                | `180801_1630.wav`                |                      | This uses a short year format. E.g. 18 means 2018        |
| `DDMMYYYY`                   | `01012015.wav`                   |                      | Do not use because it breaks the year -> day conventions |
| `YYYY-MM-DDThh:mm:ss.SSSSSS` | `2025-09-30T03:32:35.594002.wav` | NoiseNet             | Avoid due to special characters in a filename            |

### End Date times

So far only one manufacturer (Frontier Labs) encodes both a start and end date
in their filenames. They do this so their localisation software can determine
what direction from a recorder a sound was made.

We **DO NOT RECOMMEND** this format, but we recognise it is in use.
Instead we **RECOMMEND** embedding the end date in the audio file's metadata.

If you need to parse it, then EMU can parse both the start and end datestamps.

The format prefixes the start date with `S` and the end date with `E`.

| Format                                                  | Example                                                         | Commonly Produced By                              |
| ------------------------------------------------------- | --------------------------------------------------------------- | ------------------------------------------------- |
| `S{YYYYMMDDThhmmss.SSSSSSZ}_E{YYYYMMDDThhmmss.SSSSSSZ}` | `S20240815T091156.982648+1130_E20240815T091251.967555+1130.wav` | Frontier Labs high precision date format          |
| `S{YYYYMMDDThhmmssSSSZ}_E{YYYYMMDDThhmmssSSSZ}`         | `S20240815T091156.982648*E20240815T091251.967555.wav`           | Obsolete Frontier Labs high precision date format |

The datestamps produced in this format are otherwise well formatted with respect to
the recommended format.

---

[^1]: EMU can not parse all components of every format. It does however do a
      good job of presenting datestamps in the recommended format.