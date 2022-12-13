---
title: Metadata collected by sensors
---

# Metadata collected by sensors

Most acoustic sensors (or _passive acoustic monitors_) collect some metadata
along with audio recordings.

Each vendor typically collects metadata in their own format.

The goal of this document is to provide a common standard for sensor-produced
metadata.

However, it is currently unrealistic to expect every vendor to collect metadata in
the same format. Even if mass adoption occurs, there are still an uncountable
number historically recorded audio recordings for which the metadata could
prove valuable.

We expect that the most common pattern will be
<abbr title="Babel fish, a fictional species of fish invented by Douglas Adams in 1978; see The Hitchhiker's Guide to the Galaxy">babel fish</abbr>
pattern - that is, there will be one or more tools that can extract metadata from
a recording and convert it to the common format defined in this document.

The [Emu](https://github.com/QutEcoacoustics/emu) tool is one such tool.
It currently is in development along with this standard.

## Metadata locations

There are multiple places where metadata for a recording can be found:

- In the filename of the recording
  - This is the most commonly seen and used metadata
- In the audio file itself, typically in a text, comments, or custom header
- In a _sidecar_ file - that is:
  - a separate file stored in the same folder/directory as the audio file
  - in a different format and extension
  - but with the same base name
  - stores data for only the file that it shares its basename with
- In a _shared sidecar_ file - that is:
  - a file that is not the audio file itself
  - usually stored in a common location, like the root of a memory card
  - in a different format and extension
  - stores data for all files in its directory and below it
- In any _other files_, typically unrelated to a recording - that is:
  - a file that is stored in a common location, like the root of a memory card
  - it stores values associated with the sensors deployment, but not explicitly
    associated with a recording

All known sensors store some metadata in the filename of the recording.

_Frontier Labs_ and _Wildlife Acoustics_ (and others?) store metadata in
the audio file itself.

As far as we are aware, no sensor stores metadata in a sidecar files. However,
some software (like Raven, and AvianNZ) do store
[annotations](./annotations.md) in sidecar files.

Some sensors, like the _Frontier Labs BARs_ used shared _sidecar_ files.
Each recording has an entry in a CSV file that includes the metadata in an easy
to use format.

> TODO: add example of shared sidecar file

Some sensors, like _Wildlife Acoustics SM2s_ store a log of regularly sampled
temperature readings in an unrelated file.
This is a good example of a metadata file that is not related to any
of the recordings.

> TODO: add example of shared sidecar file

### Recommendations

The principle here is to make it always easy to move audio files and allow
the metadata to be moved along with them, with the least chance of error or
erasure.

#### 1. Priority

Vendors **SHOULD** store metadata in the formats described above, but, with
an emphasis of prioritizing the formats in this order:

1. In audio files
1. In filenames
1. In shared sidecar file
1. In sidecar files
1. Other files

#### 2. Redundancy

Any information stored in the filename of a recording, or in a side car file,
**SHOULD** also be stored inside the audio file itself.

A vendor **SHOULD NOT** implement on only one metadata format.

## The metadata standard

### Data stored in the filename

1. Filenames **MUST** consist of only safe characters.
    - Unsafe characters include the following and **MUST NOT** be used:
      - Characters that can be used as wildcards in a shell command (
    such as `*`, `?`, `[`, `]`, `{`, `}`).
      - Characters that are used in path constructs (such as `/`, `\`, `:`, and `;`)
      - Non-printable characters (`\x00` to `\x1F`)
2. Filenames **SHOULD** prefer basic ASCII characters
    - UTF-8 characters **MAY** be used but there a strong preference for simpler characters
3. Filenames **MUST** avoid encoded information
    - Filenames should be readable by humans
4. Filenames **MUST** be unique for each recording.
5. Filenames **MUST** contain a date stamp
6. Filenames **SHOULD** begin with a date stamp
7. Filenames date stamps **MUST** adhere to the [ISO8601 format](https://en.wikipedia.org/wiki/ISO_8601) modified for filenames.
    - The date stamp **SHOULD** be in the format `YYYYMMDDThhmmss.ssssss`
    - The date stamp **MAY** use the separator `-` or ` ` (space)
      instead of `T` but it is not recommended.
      (This is allowed in the RFC3339 format, but not in the ISO8601 format).
    - The date stamp **SHOULD** omit the fractional seconds component `.ssssss`, unless
      the sensors has a an accurate high-resolution clock
    - If a fractional seconds component is included, the sensor **MAY** emit
      only as many fractional digits as are needed to represent the resolution of
      the sensor's clock
8. A filename **SHOULD** contain a UTC offset when this information is available.
    - Valid formats include:
        - `YYYYMMDDThhmmss[.ssssss][+|-]hhmm`
        - `YYYYMMDDThhmmss[.ssssss]Z`
9. Filenames **SHOULD** consist of a series underscore (`_`) delimited fields,
    suffixed with a file format extension (including a `.` period).

    ```
    <prefix>_<date_stamp>_<suffix>.<extension>
    ```

10. Filenames **SHOULD NOT**
    - use delimiter other than `_` to separate fields
    - omit delimiters between fields
    - have leading or trailing delimiters (`_a.wav` and `a_.wav` are invalid)
11. Within a field in a filename, words can be separated by `-` (a hyphen)
    - a ` ` (space) may be used to separate words but it is not recommended
12. A filename **MAY** contain either or both of a prefix or suffix around the date stamp
13. The prefix and suffix **MAY** contain multiple fields (delimited by `_`)
14. A filename **MAY** contain the GPS location of the file
    - The location **MUST** be formatted as per the
      [ISO6709 string format (Annex H)](https://en.wikipedia.org/wiki/ISO_6709#String_expression_(Annex_H))
      but modified for filenames. Effectively this format is:

      ```
      [+|-]<latitude in decimal degrees>[+|-]<longitude in decimal degrees>[+|-]<altitude in meters>
      ```

      - The altitude is optional.
      - The leading `+` or `-` is not optional.
      - The trailing `/` solidus is not acceptable in a filename and is omitted.
      - The coordinates **MUST** be in the WGS 84 datum.
15. The filename's extension **MUST** match it's format

### Data stored in the audio file

1. Metadata stored in headers of audio files **MAY** use one of the following formats:
    - A custom RIFF chunk in a WAVE file
    - A standard mechanism for storing comments in a FLAC, WAVE, or MP3 file

This standard may define it's own format for storing metadata in audio files,
however, we're seeking comments from vendors before designing such a format.

2. Within the metadata section fields are arranged as key-value pairs.
  Each pair is delimited either by the format's standard delimiter, or
  a null character (`\0`)
3. Within the key-value pairs, the key is delimited by the format's key-value
  delimiter or an `=` (equals) sign
4. The key for each key-value pair **MUST** consist only of the characters `a-z`, `A-Z`,
  `0-9`, and `_`.
5. The value for each key-value pair **MAY** by and valid UTF-8 string (format permitting)
6. The keys present **MAY** include any of the terms defined later in this document
    - If an analogous field is recorded, the key **SHOULD** be named the same as is defined
      in this document.

      i.e. Do NOT include `RECORDING_DATE` in the key-value pairs when this document
      defines `recording_start`

7. Fields not included in this document **MAY** be included.
8. Arrays of values can use a suffixed index to indicate the position of the value
    - These indexes **MUST**
        - be integers
        - be positive
        - start from 0 
    - For example, `microphone_type_0` indicates the first microphone type and
        `microphone_type_1` indicates the second microphone type.

#### Well known fields

This is a list of the fields that could be defined in the metadata of an audio file:

- `dateTime` in ISO8601 format
- `sensorUTCOffset` - not required if included in dateTime
- `fileName` - ideally, containing dateTime and UTC information
- `recordingStart`
- `recordingEnd`
- `sensorID` - identification of the sensor for deployment purposes
- `deviceSerial` - number identifying the sensor to the vendor
- `sensorFirmwareVersion`
- `microphoneType_<index>`
- `microphoneID_<index>`
- `microphoneBildDate_<index>`
- `channelGain_<index>`
- `sampleRate`
- `fileSize`
- `duration`
- `fileFormat`
- `bitsPerSample`
- `channelCount` - 1 or 2 channels, i.e.: mono or stereo
- `bitSize`
- `mediaType`
- `memoryCardSerial`
- `memoryCardID`
- `cardSlotNumber`
- `memoryCardCapacity`
- `memoryCardFreeSpace`
- `memoryCardSpeed`
- `memoryCardFormatType`
- `memoryCardManufacturerID`
- `memoryCardOemID`
- `memoryCardProductRevision`
- `memoryCardWriteCurrentVmin`
- `memoryCardWriteCurrentVmax`
- `memoryCardWriteB1Size`
- `memoryCardEraseB1Size`
- `batteryVoltage`
- `batteryPercentage`
- `powerType` - solar or internal battery
- `location`
- `latitude`
- `longitude`
- `lastTimeSync`
- `scheduleName`


// more to come
