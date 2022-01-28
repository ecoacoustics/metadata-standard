# Standard structure for storing audio files

It is advisable to keep original files as those have the log file associate
that contains important metadata. Also, it is advised to keep files in original
size and split into smaller files by demand and to not keep the smaller files
as those take up too much memory.

## General folder structure

`{project}/{deployment}/{site}/[{memory_card}/]`

## Syntax

- `/` represents a folder separator (either on Windows (`\`) or Linux (`/`))
- The tokens between the square braces (`[` and `]`) represent optional folders
- The tokens between the squigly braces (`{` and `}`) represent folder names

## Token guide

- `{project}`: A short name for the project the audio is being collected for.
  - e.g. `Y:\Groote`, or `Y:\Cooloola`
- `{deployment}`: A human readable date that roughly represents when the data
was collected. Optionally it may include the deployment dates as a range.
  - e.g.  `Y:\Groote\201506`, or `Y:\Cooloola\20150715`
  - e.g.  `Y:\Groote\2015 June`, or `Y:\Cooloola\2015 July, Week 1`
  - e.g.  `Y:\Groote\20150101-20150301`, or `Y:\Cooloola\20150706-20150710`
- `{site}`: A short name that describes the site (the location on the ground)
where the sensor was deployed.
  - e.g. `Y:\Groote\201506\Emerald River`, or `Y:\Cooloola\20150715\GympieNP`
- `{memory_card}`: An optional folder. If the sensor used more than one memory
card, audio should be kept in the same folders that represent the memory card it
was recorded on.
  - e.g. `Y:\Groote\201506\Emerald River\Card 1`, and `Y:\Groote\201506\Emerald River\Card 2`

### Why did we choose `/{deployment}/{site}/` instead of `/{site}/{deployment}/`?

We typically add data in batches as they are collected from sensors. We also
typically get data back from one project at a time.

If we store the data in batches (the same way it was collected) it makes it
easier to analyse and upload those same batches of data.

If we didn't store data in the deployment folders, all old and new data would
be mixed... making it even harder to efficiently harvest/analyze audio data.

### Storage of other data

We generally encourage users to **copy** in any relevant data. In particular,
leaving notes that describe the data (e.g. "left mic failed", or "RTC failed,
dates invalid"), or copies of their records. Any metadata is appreciated.

Most data should be put in the site folders as usually most important
information is related to a sensor. More information about additional metadata can be found [here](./field_data.md#additional-metadata).

### Wrong date or time set

If the wrong date or time was set on a sensor, then all files will have an
incorrect offset.

This error is repairable provided the
_exact original recording start date and time_ is known. For that reason, [this](./field_data.md#The+date+and+time+to+use) is important.

### RTC batteries flat/faulty

If for some reason the RTC (real time clock) batteries are flat then all the
datestamps will look like similar to this: `prefix_20000101_002404.wav`.

In particular, note the `200001...` section of the datestamp indicates the
recording started in January of the year 2000... which is almost certainly wrong.

#### For battery deployments

Provided the sensor was deployed using only a battery pack, then this error is
repairable IFF the _exact original recording start date and time_ is known. For
that reason, [this again](./field_data.md#The+date+and+time+to+use) is important.

### For solar panel deployments

If the sensor was deployed using a solar panel, **it is likely all audio data
from that sensor will be marked as corrupt**.

Because solar panel deployments (which are often backed by a large main-power
battery) can turn on and off based on the availability of power, the result can
include non-contiguous sections of audio data. When the RTC batteries are
working correctly and when the sensor powers up again, there is no problem - the
new section of audio data will be dated correctly (the powered off period will
not affect the datestamps).

However, if the RTC batteries are not working and the sensor powers up again,
the sensor will revert to the factory date (Jan 1st 2000). If this power cycle
happens multiple times, each new group of audio files recorded in batches
starting again from the factory date. The result is essentially **randomly dated**
 audio files.
