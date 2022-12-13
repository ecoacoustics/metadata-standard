---
title: Metadata standard
---

# metadata-standard

A set of pseudo-standards for metadata for ecoacoustics projects.

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.5778058.svg)](https://doi.org/10.5281/zenodo.5778058)

## Why

Common standards of data allow work to be reused across different projects.
There are formal standards for metadata and they're important.
You can find out more about the standards that relevant for Ecoacoustics at

- The Biodiversity Information Standards (TDWG) <https://www.tdwg.org/>
- Audobon Core <https://ac.tdwg.org/>
- The Annotations Interest Group <https://github.com/tdwg/annotations>

**However**, we don't think standards like these are appropriate for every day
use. They are great for transferring data between databases but, they're
exacting and finnicky to use.

Our goal with this repository is to describe a set of best practices that will
push your everyday ecologist into choosing names, values, and data structures
that will be easy to convert to formal standards, but which will not require
them to know about these standards.

## Goals

- Simplify the exchange of ecoacoustics data through common formats
- Ensure adequate data is collected to make the science of ecoacoustics reproducible
- Push users into the pit of success with gentle suggestions
- Make it easy to convert from these common formats to formal standards

## Status

This standard is currently a draft proposal. We encourage collaboration and
comments through the
[issue tracker](https://www.github.com/ecoacoustics/metadata-standard/issues) and our
[discussions tab](https://www.github.com/ecoacoustics/metadata-standard/discussions).

## Parts

Our standard is divided into parts to make it easy to read. Each part is in a folder
or file next to this README.

- [Naming & Terminology](./naming.md)
- [Units](./units.md)
- [Field Data](./field_data.md)
- [Sensors](./sensors.md)
- [Storage](./storage.md)
- [Annotations](./annotations.md)
- [Analysis Effort](./analysis_effort.md)
- [Command Line Interface](./cli.md) for batch analysis

## Terminology

Formal standards define what certain terms mean. We'll do that here to, albeit
with less of a focus on consistency. These terms are taken from
[RFC 2119](https://www.rfc-editor.org/rfc/rfc2119.html).

- **MUST**: means that the term is required to be present in the metadata.
- **MUST NOT**: means that the term is not required to **NOT** be present in the metadata.
- **SHOULD**: means that the term is recommended to be present in the metadata.
- **SHOULD NOT**: means that the term is not recommended to **NOT** be present in the metadata.
- **MAY**: means that the term is optional (optionally present) in the metadata.

## Support

This project is supported by the [Open Ecoacoustics](https://openecoacoustics.org) project.

![The Open Ecoacoustics Logo](./media/OpenEcoAcoustics_horizontal_rgb.jpg)
