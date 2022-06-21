---
status: draft
version: 0.1
---

# Command Line Interfaces


A _command line interface_ is the arguments accepted by a non-graphical program.
It's really important for using non-interactive (and non-graphical) programs.

Many analyses are extremely useful because they're interactive:

- you can plot graphs
- run different sections of your program when you want
- interact with graphics (like RShiny or Jupiter Notebooks)

However, once you've finished building your analyses, 
there tends to be a requirement to run the analysis again, but this time at scale, over a _whole_ lot of data.
Systems that do these analyses, like your University _High Performance Computer_, are unique:

- their job systems are not[^1] interactive
- their job systems are not graphical 
   - you can't _show_ images (but you can _save_ them for later)
   - you can't run your analyses step by step
- they tend to be highly parallelizable 
- they tend to be file based - they have a shared network storage system that all jobs can access

So what are we to do?

A little bit of software architecture will help! Any analyses should have three main sections:

- Your scratch area (or note book, or experimentation entry)
- A CLI interface (for use with HPC and other non-interactive systems)
- The core part of your analysis that is common to both.

In another article !!!TODO!!! we'll help you structure your programs to adhere to this guidance.
This article focuses on a standard implementation for the CLI interface.
    
## Common Analysis CLI

### Purpose

To analyze a short block of audio with pre-defined (and configurable analysis)
with the restriction that the analysis must be non-interactive, and non-graphical.

Typical usages would be to run an event recognizer or a classifier over a segment of audio.

### Syntax

An abstract example of the syntax follows:

```
<path to executable> --output <path to output directory> --configuration <path to configuration> <path input file>
```

Here are several conforming examples.

A Windows example running a PowerShell script:

```
C:\Users\Anthony\Documents\GitHub\bower-bird\run.ps1 --output F:\temp --configuration C:\Users\Anthony\Documents\GitHub\bower-bird\config.yml minute1.wav
```

A Linux example running a Bash script:

```
/work/analysis.sh --output /scratch --configuration /work/configuration.txt minute2.wav
```


### Details

- `<path to executable>` is the absolute file system path the script that will run the analyses
    - it should be executable (i.e. have the `+x` permission on Linux/Mac, or have the `.exe` or `.ps1` extension on Windows) 
- `--output` is a required option that specifies the directory where output from your analysis **MUST** be places
    - the supplied path **MUST** be absolute
- `--configuration` is an _optional_ option that **MAY** be provided to customize the analysis
    - the supplied path **MUST** be absolute
- `<path to input file>`
    - the supplied path **MUST** be absolute
- The script **MUST NOT** fail if additional options are provided
- The script **MUST** return an exit code
    - `0` means the script ran without problem
    - Any value from `1` though to `255` (inclusive) means an error occurred
    - Any other value **MUST NOT** be returned

### Audio details

- the supplied file **MUST** be a WAVE file
- the supplied file **MUST** have an `.wav` extension
- the supplied file is referred to a segment
- the suplied file **SHOULD** be `60 seconds` in duration
- there **SHOULD** be negligble overlap between each segment
- the spec **DOES NOT** define any of the following properties:
    -   sample rate
    -   channels
    -   bit depth
    -   file name format

### Recommended implementation 

Real world practicalities mean CLIs are not as simple as this spec defines. Thus we recommend using a wrapper script which hides the complexity.

#### A cross-platform PowerShell example

The following PowerShell example adapts [AP.exe](https://github.com/QutEcoacoustics/audio-analysis) to conform to this specification

```pwsh
#!/usr/bin/env pwsh -l


$output = $args[1]
$configuration = $args[3]
$segment = $args[4]


if ($IsWindows) {
    AP.exe audio2csv $segment $configuration $output -n
}
else {
    AP audio2csv $segment $configuration $output -n
}

return $LASTEXITCODE
```

## Open questions

### Configurable segment semantics?

Should the block size, format, or overlap be configurable?

Does a user want 120-second blocks, consistent sample rate, or an overlap of 50%?

### Providing of metadata

It would be nice if we could pass a metadata blob to the analysis. Something like a `--metadata` flag which points to a JSON file which contains:

```json
{
  "original": { /* metadata on the original file */ },
  "segment": { /* metadata for the current segment */ }
}
```

### Other standards for other tasks

This standard is designed specifically for analyses where no learning/training occurs. 

Does the opportunity exist to define a standard for training tasks?

Analysis tends to be embarrassingly parallel; a need to run on HPC (or in batch systems) drives this standard. Does that need also exist for training?

---

[^1]: PBS does have an interactive mode, where you are allocated the resources you requested and you can type commands in. However, it is still not well suited 
