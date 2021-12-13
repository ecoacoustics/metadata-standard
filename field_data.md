# Data collection and metadata

This part is aimed to inform best practice for providing information
when sharing/publishing acoustic data, but also additional metadata that could
be collected and would help to increase re use and sharing data for different purposes.

## Effort

Amount of data collected during the whole deployment

Unit: Gigabytes (GB)

## Data collection protocol

How was the data collected? Inform about recording protocol (i.e.: how the recorder
was programmed) and sampling design (how many days, month, year, and sampling points).

If the data collection protocol was inspired/same as published research, provide citation. It is also important to provide justification of choices based on ecology/biology nature of research questions to be answered.

Examples:

    - 10 Recorders were programmed to record 1 minute every 5 minutes and stayed in
    the field for 10 days in October/2019. Sampling points can be found in figure x (provide map with experimental design).
    - 2 recorders were deployed at -27.38, 152.87; -27.38, 152.88. The equipment were
    programmed to record continuously and were left at each location from October 1st,
    2019 until October 5th, 2019.
    - 24 recordings were deployed in 12 different landscapes. The sound data was collected
    from 15/08/2016 until 12/11/2016 with recorders rotating between landscapes. Complete
    description of sampling dates at each landscape, including information on coordinates,
    can be found in table xx (provide table with geographic coordinates and dates for each
    landscape sampled).

## Additional metadata

Additional data is very beneficial when analyzing ecological data. For acoustics,
some metadata is required as they would determine ecological patterns, species
identification etc, while others might be beneficial although not mandatory.

### Associated with every recording

- [**MUST**] [Date](./units.md#dates)

- [**MUST**] [Time](./units.md#dates)

- [**MAY**][Temperature](./units.md#temperature)

- [**MAY**]Relative Humidity

### Associated with every deployment

- [**MUST**] [Location](./units.md#gps+coordinates)

- [**MUST**] Sampling rate

- [**MAY**] Microphone gain

- [**MAY**] Additional ecological information:
  - Vegetation around the recorder (Canopy cover, shrub cover, dominant
   vegetation species, among others)

  - Aspect

  - Slope

  - Site photos (North, South, East, West)

## The date and time to use

- The date and time should be set to the local time of the deployment area and
provide information on UTC offset at the moment of deployment. Additionally,
this information **MUST** be recorded in metadata spreadsheet associated with
each sensor so if [this](./naming.md#Wrong+date+or+time+set) happens, the correct
date and time can be fixed.
  - e.g. If deploying in QLD, the timezone is AEST, the offset is +10  
  - e.g. If deploying in NSW, the timezone is either AEST or AEDT
  (daylight savings). Set the time correctly to **local time**
  (including daylight savings) **for when the sensors are first scheduled to record**.
  - If the first recording is scheduled for October 4th 2015 06:00,
    set the time to +11 (one hour forward), the same as what your smartphone/watch/clock
    would indicate on that day.
  - If the first recordings is schedules for April 3rd 2016 06:00,
    set the time to +10 (normal time)

## Pre-Deployment

Before the sensor is setup in the field.

Before deployment, ensure the following:

- Check to make sure you have the latest version of the firmware.
- Fresh batteries are installed

- Fresh batteries installed for clock (if required)

- Configuration information is set

- Date and time are set correctly.

___



## Checklist

A purportedly handy summary of the above

- [ ] Pre-deployment
  - [ ] Plan study
  - [ ] Pack equipment
    - [ ] Check firmware
    - [ ] Install RTC batteries
    - [ ] Set Time
    - [ ] Set configuration/schedule
    - [ ] Microphones
    - [ ] Microphone windsocks
    - [ ] Power supplies
      - [ ] Battries
      - [ ] Solar Panels
        - [ ] Solar panels
        - [ ] Solar panel electronics
        - [ ] Battery reserve (?Dry-cell?, deep-cycle)
    - [ ] Tools
      - [ ] ...
    - [ ] Mounting equipment
      - [ ] ...
- [ ] Deployment
  - [ ] Attach microphones
  - [ ] Open Cover
  - [ ] Test Audio
  - [ ] Inspect for damage
  - [ ] Check batteries installed
  - [ ] Check firmware
  - [ ] Check Time/Date
  - [ ] Check desiccant
  - [ ] Install SD cards
  - [ ] Check scheduled wake up time
  - [ ] Mounting
    - [ ] Check in shade for hot areas
    - [ ] ...  
  - [ ] Wake up, record date, time, and site
  - [ ] Make sure indicator light is flashing
  - [ ] Record meta-data
    - [ ] GPS coordinates (latitude, longitude, altitude, coordinate system)
    - [ ] Site name
    - [ ] Photos
    - [ ] Date/Time information
      - [ ] Local time (as per your watch)
      - [ ] Sensor time (what the sensor says is the time)
      - [ ] The timezone you are in at the moment of deployment
    - [ ] Relevant ecology / geography details
