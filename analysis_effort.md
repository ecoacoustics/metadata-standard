# Analysis Effort

This section describes which metrics and procedures should be reported when performing
data analysis. It also aims to propose a standardised way to do that so it is
easier to compare and share data among different projects.

The idea is to have sections/descriptions that should be in the methods section
of a paper, ensuring research can be reproduced, compared and improved.
Moreover, it is also important to try and justify the choices as much as possible,
either with citations from similar work or ecological reasons for making such decisions

## Effort

How much data was analysed

Unit: Bytes

## How was the data analysed?

Description of how the data was analysed

Example:

- Data was manually `annotated`
- `Acoustic indices` were calculated
- Species `presence/absence` data was collected
- Minutes were `clustered`, etc.

_Note:_ for more information on annotations see [this link](./annotations.md)

## Tool

Which software, version, package, was used to analyse the data. Provide all the
required information to make sure the research is reproducible.

Example:

- `Raven` was used for annotations;
- `AnalysisPrograms.exe` was used for generating indices;
- `Audacity` was used for detecting species presence/absence;
- `Kaleidoscope` was used for clustering and `Raven` was used for species'
identification
    in each cluster.

## How much effort was put into it?

How much time did it take to analyse the informed amount of data, in a way,
using that tool.

Ideally, this information should be the most precise as possible. However, we
understand this might not always be possible or accurate. Therefore, even if it
is a rough estimate, or only the computational effort, this will help to provide
comparison between methods and inform the development of better tools.

Example:
- `X` bytes of data were manually annotated in `Y` hour of effort.
- `U` bytes of data were analysed using `AnalysisPrograms.exe` to calculate acoustic indices. In a computer with `ABC` specifications, the analysis took `D` hours to run.
- `F` hours were necessary to go through `E` bytes of files and collecting bird species presence/absence information.
- Clustering of `Q` bytes took `P` minutes with `N` clusters being generated. Identification of those clusters took `O` hours. 

## What was the analysis protocol?

Was there protocol used to analyse the data in a systematic way? In this section
is important to provide justification for every choice, being that the
ecological/biological reason for such choice and/or relevant citation that used
similar method for answering related questions.

Example:

- Species were identified in the `first minute of every hour`
- Indices were calculated for `every minute` of recording;
- Species presence were collected by analysing `5 minutes every 10 minutes`;
- `60 initial clusters` were generated and `5 first minutes of each one` were identified.

## Who performed the analysis

Provide information on the person who performed the analysis (ideally ORCID).

## Data repository

If the data or any step of the analysis is available in a repository, provide
link/DOI for access.

____

Any additional information that was no covered in this document
is valuable as it could improve usability of the data in different contexts. Information on techniques that were tested and did not work is also extremely valuable along with the information/hypothesis of how/why it failed. A lot of time could be saved if we shared not only the success stories but also the "fiascos".

If you would like to contribute, check [this link](./README.md#status)

## Checklist

- [ ] Analysis effort
- [ ] Data analysis description
- [ ] Information software/method used
- [ ] How much effort was put into analysis
- [ ] Analysis protocol
  - [ ] Description
  - [ ] Ecological/biological justification
  - [ ] Important references/citations
- [ ] Information on who performed the analysis
- [ ] Data repository information
