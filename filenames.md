---
title: Filenames for audio files
---

# Filenames for audio files

This document is aims to standardise audio file names so for easy ingestion by
platforms and tools such as [Ecosounds](https://www.ecosounds.org/) and
[emu](https://github.com/QutEcoacoustics/emu).

Having a consistent file format for audio files encourages the collaboration,
interoperability, and re-use of audio data.

## Common Rules

These rules should be applied to all audio files

1. All audio files **should** have a file extension notating the file format
2. All audio files **should** contain information about when it was recorded in the file name

## Recommended

To maintain consistency across contributors and easy ingestion of data, it is
recommended that you use the "short"
[ISO8601](https://en.wikipedia.org/wiki/ISO_8601) format.

This is the same as the "full" ISO8601 format, but does not include the optional
fractional seconds (ISO 8601 section 4.2.2.4).

An example of the recommended format can be seen below:

```txt
2017-06-25T10:21:05.flac`
```

### Technical Details

`YYYY-MM-DDThh:mm:ss`

| Code | Meaning                             |
| ---- | ----------------------------------- |
| YYYY | A 4 digit year                      |
| MM   | A 2 digit month, with leading zeros |
| DD   | A 2 digit day, with leading zeros   |
| hh   | Hours, with leading zeros           |
| mm   | Minutes, with leading zeros         |
| ss   | Seconds, with leading zeros         |

## Secondary Recommended Formats

Secondary recommended formats are formats which are recommended for very
specific use cases which may require additional information.

### Fractional seconds

If your audio requires fractional second accuracy, you can include fractional
seconds that conform to the ISO 8601 standard.

`YYYY-MM-DDThh:mm:ss.SSSS`

| Code        | Meaning                                        |
| ----------- | ---------------------------------------------- |
| YYYY        | A 4 digit year                                 |
| MM          | A 2 digit month, with leading zeros            |
| DD          | A 2 digit day, with leading zeros              |
| hh          | Hours, with leading zeros                      |
| mm          | Minutes, with leading zeros                    |
| ss          | Seconds, with leading zeros                    |
| SS          | fractional seconds                             |
| {Extension} | Audio file type (e.g. `.flac`, `.wav`, `.mp3`) |

## Alternative Date & Time Formats

<https://github.com/QutEcoacoustics/emu/blob/master/test/Fixtures/FileNameParsingFixtures.csv>

If it is not possible to convert audio file names into the
[recommended](#recommended) format, the below formats are recognised by most
ecoacoustic tooling.

Most "alternative" formats are variations of the `YYYYMMDD` format, with
differing prefixes/suffixes, separators, and location information.

| Format                       | Example                          | Commonly Produced By                                                  | Comments                                                 |
| ---------------------------- | -------------------------------- | --------------------------------------------------------------------- | -------------------------------------------------------- |
| `YYYY-MM-DDThh:mm:ss.SSSSSS` | `2025-09-30T03:32:35.594002.wav` |                                                                       |                                                          |
| `YYYYMMDD_hhmmss`            | `20170625_102105.wav`            | Wildlife Acoustics (sm2, sm3, sm4, song meter mini, song meter micro) |                                                          |
| `YYYYMMDD_hhmmss_SSS`        | `20170625_102105_010.wav`        |                                                                       |                                                          |
| `YYYYMMDD-hhmmss`            | `20100503-080000.wav`            |                                                                       |                                                          |
| `YYYYMMDD$hhmmss`            | `20180221$031609.wav`            |                                                                       |                                                          |
| `YYYYMMSS*hhmmss*`           | `20170704*104849*.wav`           |                                                                       |                                                          |
| `YYYYMMDDhhmmss`             | `20070415051314.wav`             |                                                                       |                                                          |
| `YYYYMMDDThhmmss`            | `20091219T070006+1000.wav`       |                                                                       |                                                          |
| `YYYYMMDDThhmmss.SSSSSS`     | `20161108T075126.123456.wav`     |                                                                       |                                                          |
| `YYYYMMDD`                   | `20131012.wav`                   |                                                                       |                                                          |
| `YYYYMMDD_hhmmss`            | `20131012_123456.wav`            |                                                                       |                                                          |
| `yyMMDD_hhmm`                | `180801_1630.wav`                |                                                                       | This uses a short year format. E.g. 18 means 2018        |
| `DDMMYYYY`                   | `01012015.wav`                   |                                                                       | Do not use because it breaks the year -> day conventions |
| `{HEX_ENCODED_UNIX_EPOCH}`   | `5B07C752.wav`                   | Audio moth                                                            |                                                          |

## End Date times

| Format                                                                  | Example                                               | Commonly Produced By                              |
| ----------------------------------------------------------------------- | ----------------------------------------------------- | ------------------------------------------------- |
| `S{StartDate YYYYMMDDThhmmss.SSSSSS}_E{EndDate YYYYMMDDThhmmss.SSSSSS}` | `S20240815T091156.982648_E20240815T091251.967555.wav` | Obsolete Frontier Labs high precision date format |
| `S{StartDate YYYYMMDDThhmmss.SSSSSS}*E{EndDate YYYYMMDDThhmmss.SSSSSS}` | `S20240815T091156.982648*E20240815T091251.967555.wav` | Obsolete Frontier Labs high precision date format |

## UTC offsets

### Recommended UTC Offset Formats

It is recommended that you include the UTC offset using a plus (+) sign directly
after the date/time section of a file name.

E.g. A UTC offset of "UTC+10:00" will be encoded in the file name as such:

```txt
2017-06-25T10:21:05+1000.flac
```

### Alternative UTC Offset Formats

| Suffix Format | Example                         | Comments            |
| ------------- | ------------------------------- | ------------------- |
| `-hhmm`       | `2017-06-25T10:21:05-1000.flac` |                     |
| `_hhmm`       | `2017-06-25T10:21:05_1000.flac` |                     |
| `*hhmm`       | `2017-06-25T10:21:05*1000.flac` |                     |
| `Z`           | `2017-06-25T10:21:05Z.flac`     | Shortcode for UTC+0 |

### Invalid Date & Time Formats

| Format                             | Example                        | Comments                                                                                                             |
| ---------------------------------- | ------------------------------ | -------------------------------------------------------------------------------------------------------------------- |
| `YYYYMMDD_hhmmss.{HEX UNIX EPOCH}` | `20180517_010348.5AFCD4F4.wav` | Mixing the `YYYYMMDD_hhmmss` with the audio moth unix epoch hex is invalid. The first date/time found should be used |

## Location

It is **recommended** to encode location information inside of the audio files
metadata.

However, if you have a specific use case requiring the location to be present in
the audio files name, you can use the following formats.

### Recommended Location Format

[ISO6709:H without trailing solidus](<https://en.wikipedia.org/wiki/ISO_6709#String_expression_(Annex_H)>)

E.g. An audio file with the latitude -39.5336, and longitude of -131.2711

```txt
2017-06-25T10:21:05-39.5336-131.2711.flac`
```

If a UTC offset is also required in the file name, the UTC offset should come
directly after the date/time portion of the file name.

E.g. For a UTC offset of `+1000`

```txt
2017-06-25T10:21:05+1000-39.5336-131.2711.flac`
```

### Alternative Location Formats

| Code | Meaning |
| ---- | ------- |
| D    | Degrees |
| M    | Minutes |
| S    | Seconds |

| Format        | Example                           |
| ------------- | --------------------------------- |
| `[DD.D DD.D]` | `20180226 [27.2819 90.1361].wav`  |
| `*DD.D DD.D*` | `20160823 *-1.4763 178.8986*.wav` |
| `_DD.D DD.D*` | `20180226 _27.2819 90.1361*.wav`  |
