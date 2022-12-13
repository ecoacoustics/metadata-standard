---
title: Units
---

# Units

Simply put, all units for all values **MUST** be
non-prefixed _International System of Units_ (_SI_ / _Metric_) units.

This may not always be the easiest choice but this rule will vastly simplify
interoperation and conversion of data between different databases.

## Rules

### 1. Implicit units **MUST** be assumed to be **SI** units

Any field that does explicitly mention a unit **MUST** be assumed to be in SI units.

### 2. Explicitly mentioned units **SHOULD** be **SI** units

A field may include the name of the unit in it's _name_ if it helps clarify
the meaning of the value.

The unit name **SHOULD NOT** be abbreviated.

CSV distance measurement in meters:

```csv
distance_meters
12030
```

### 3.Values that violated the above rules **MUST** name the unit explicitly

A field **SHOULD NOT** store any non-SI unit.

It **MAY** store a non-SI unit if the unit it is explicitly stated in the field's name.

The unit name **SHOULD NOT** be abbreviated.

Examples:

CSV distance measurement in kilometers:

```csv
distance_kilometers
12.03
```

JSON distance measurement in miles:

```JSON
{
    "distance_miles": 7.4750954
}
```

## Further definitions

### Dates

Dates must be stored in the [ISO8601 format](https://en.wikipedia.org/wiki/ISO_8601).

The ISO8601 format is a standard format for representing dates and times.
It is flexible in some of its forms. For example:

- The most common form is `YYYY-MM-DDThh:mm:ss`
  - this is a _local date_, that is, a date that is ambiguous in the exact time it
    occurs because it has no UTC offset information.
- You can add fractional seconds `YYYY-MM-DDThh:mm:ss.sss`
- Or you can use an alternate separator: `YYYY-MM-DD hh:mm:ss.sss`
  - using a ` ` (space) separator is recommended for dates that need to be parsed by Excel
  - using the `T` separator is the recommended default
- 24-hour times **MUST** be used.
- AM and PM times **MUST NOT** be used.
- You can add UTC offsets: `YYYY-MM-DDThh:mm:ss+HH:MM`
- Or include dates in UTC: `YYYY-MM-DDThh:mm:ssZ`

### Durations

Durations **SHOULD** always be stored in seconds.

A duration **MAY** be stored in the [ISO8601 duration format](https://en.wikipedia.org/wiki/ISO_8601#Durations), but it is not recommended.

### Offsets

Offsets **MUST** be stored in seconds.

Offsets **MUST NOT** be negative.

### GPS Coordinates

GPS coordinates **MUST** adhere to the following rules:

- latitude and longitude **MUST** be stored in decimal degrees
- where a geodetic datum is not specified it should be assumed to be WGS84
- you **SHOULD** avoid storing coordinates in other datums
  - if you do you **MUST** include the datum in another field
- coordinates **MAY** be stored in the following formats:
  - two fields, typically named `latitude` and `longitude`, in the WGS84 datum

    ```csv
    latitude,longitude
    -27.3812533,152.7130153
    ```

  - three fields, typically named `latitude`, `longitude` and `geodetic_datum`

    ```csv
    latitude,longitude,geodetic_datum
    -27.3812533,152.7130153,WGS_84
    ```

  - one field, using the [ISO 6709](https://en.wikipedia.org/wiki/ISO_6709#String_expression_(Annex_H))
    standard _String (Annex H)_ format, typically named `location`.

    ```csv
    location
    -27.3812533+152.7130153/
    ```

    With altitude:

    ```csv
    location
    -27.3812533+152.7130153+28.4CRSWGS_84/
    ```

### Frequency

Frequency values **MUST** be stored in hertz (Hz).

### Temperature

Technically, the SI unit for temperature is kelvins (K). However, we recognize
that outside of physics and chemistry, using kelvins is impractical.

As degrees Celsius (℃) is a derived SI unit, has the same magnitude as kelvins,
and is trivial to convert to and from, we recommend that temperature values be
stored in degrees Celsius.

## Advice for working with user-facing units

Units should be converted to an appropriate format when shown in a user interface,
or when otherwise presented to a user.

For example: a field survey form should accept units in the most relevant format.
This might mean miles or kilometers for a distance measurement.

When the data is saved, it **MUST** be converted to non-prefixed SI units.

### Example: making an app

If you're making an app, you can convert units in your view-model or in the
binding expression of the UI component.

### Example: using a spreadsheet

If you're recording data in a spreadsheet, you can accept user input in one
cell, and have another hidden cell that converts the user input to SI units.
