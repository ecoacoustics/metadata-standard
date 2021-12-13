# Annotations guides

An _annotation_ is any descriptive mark applied to some data.

For Ecoacoustics, we can constrain the definition to:

> An annotation is one or more labels applied to a bounded segment of audio

The terms _acoustic events_, _tags_, or _labels_ are often used, however,
for consistency implementors **SHOULD** use the term _annotation_.

This document proposes the fields required for standard annotations so they
could be easily shared among researchers and used in different
softwares/purposes/contexts.

All units **MUST** be SI units.
If you're not sure what does this means, check our page on [units](./units.md)

## Fields

- [**MUST**] **Start:** of the annotation in the recording in
[seconds](./units.md#offsets), i.e.: offset from the initial time of the
recording

- [**MUST**] **Species Scientific Name/Common name/Sound id:** Scientific name
is preferred to decrease ambiguity

- [**MUST**] **Type of tag:** Indication if the tag is scientific name, common
name or other type of tags; E.g.: if the tag corresponds to species scientific
name, type of tag should be `scientific_name`;

- [**MUST**] **Event date:** [date](./units.md#dates) of the annotation
(same date as recording)

- [**MUST**] **Unique ID:** Unique id of that annotation

- [**MUST**] **Verification status:** if the annotation was verified by someone
else, this should be stated. The suggested vocabulary here is the
[iNaturalist](https://www.inaturalist.org/posts/26549-what-is-a-verifiable-observation-and-how-does-it-reach-research-grade)

- [**SHOULD**] **End:** end of annotation in the recording in
[seconds](./units.md#offsets), i.e.: offset from the initial time of the
recording

- [**SHOULD**] **Latitude:** [latitude](./units.md#gps+coordinates) of the
recording where the annotation was identified

- [**SHOULD**] **Longitude:** [longitude](./units.md#gps+coordinates) of the
recording where the annotation was identified

- [**MAY**] **High Frequency:** Higher point in [frequency](./units#frequency)
of the annotation

- [**MAY**] **Low Frequency:** Lower point in [frequency](./units#frequency)
of the annotation

- [**MAY**] **Identified by:** ORCID or name of the person who annotated
