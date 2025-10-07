---
title: Filenames for audio files
status: draft
---

# Filenames for audio files

## Recommended

To maintain consistency across contributors and easy ingestion of data, it is
recommended that you use the "short" ISO8601 format.

2017-06-25T10:21:05.flac

### Technical Details

`yyyy-MM-ddThh:mm:SS.file_extension`

| Code           | Meaning                                        |
| -------------- | ---------------------------------------------- |
| yyyy           | A 4 digit year                                 |
| MM             | A 2 digit month, with leading zeros            |
| dd             | A 2 digit day, with leading zeros              |
| T              | Separator between date & time information      |
| hh             | Hours, with leading zeros                      |
| :              | Separator between hours and minutes            |
| mm             | Minutes, with leading zeros                    |
| :              | Separator between minutes and seconds          |
| SS             | Seconds, with leading zeros                    |
| .              | Separator between time & file extension        |
| file_extension | Audio file type (e.g. `.flac`, `.wav`, `.mp3`) |

## Alternative Formats

<https://github.com/QutEcoacoustics/emu/blob/master/test/Fixtures/FileNameParsingFixtures.csv>

If it is not possible to convert audio file names into the
[recommended](#recommended) format, the below formats are recognised by most
ecoacoustic tooling.

| "Filename"                                                                         | "ExpectedDateTime"           | "Timezone Offset" | "TokenizedName"                                                |
| ---------------------------------------------------------------------------------- | ---------------------------- | ------------------ | -------------------------------------------------------------- |
| "THOMPSON_20170625_102105.wav"                                                     | "2017-06-25T10:21:05"        |                    | "THOMPSON\_{LocalStartDate}{Extension}"                        |
| "20170704*104849*.wav"                                                             | "2017-07-04T10:48:49"        |                    | "{LocalStartDate}\_{Extension}"                                |
| "20150703_050000_MusimunatDay2.wav"                                                | "2015-07-03T05:00:00"        |                    | "{LocalStartDate}\_MusimunatDay2{Extension}"                   |
| "MISTLETOE_20170406_075002.wav"                                                    | "2017-04-06T07:50:02"        |                    | "MISTLETOE\_{LocalStartDate}{Extension}"                       |
| "20180226*040000_Bar29 \_27.2819 90.1361*.wav"                                     | "2018-02-26T04:00:00"        |                    | "{LocalStartDate}\_Bar29 {Location}{Extension}"                |
| "20180226_040000_Bar29 [27.2819 90.1361].wav"                                      | "2018-02-26T04:00:00"        |                    | "{LocalStartDate}\_Bar29 {Location}{Extension}"                |
| "NW3-010793_20140331_053200.wav"                                                   | "2014-03-31T05:32:00"        |                    | "NW3-010793\_{LocalStartDate}{Extension}"                      |
| "SM301297_0+1_20170912_220000.wav"                                                 | "2017-09-12T22:00:00"        |                    | "SM301297*0+1*{LocalStartDate}{Extension}"                     |
| "STURT1_20150130_000954.wav"                                                       | "2015-01-30T00:09:54"        |                    | "STURT1\_{LocalStartDate}{Extension}"                          |
| "20160823*063006_Dawn *-1.4763 178.8986\_.wav"                                     | "2016-08-23T06:30:06"        |                    | "{LocalStartDate}\_Dawn {Location}{Extension}"                 |
| "MISTLETOE_20151126_182616.wav"                                                    | "2015-11-26T18:26:16"        |                    | "MISTLETOE\_{LocalStartDate}{Extension}"                       |
| "THOMPSON_20171025_102103.wav"                                                     | "2017-10-25T10:21:03"        |                    | "THOMPSON\_{LocalStartDate}{Extension}"                        |
| "NW3-010793_20131024_051500.wav"                                                   | "2013-10-24T05:15:00"        |                    | "NW3-010793\_{LocalStartDate}{Extension}"                      |
| "20180210*123000_Bar26 \_23.8916 95.9669*.wav"                                     | "2018-02-10T12:30:00"        |                    | "{LocalStartDate}\_Bar26 {Location}{Extension}"                |
| "PILLIGA_20121204_234600.wav"                                                      | "2012-12-04T23:46:00"        |                    | "PILLIGA\_{LocalStartDate}{Extension}"                         |
| "20110921_110000.wav"                                                              | "2011-09-21T11:00:00"        |                    | "{LocalStartDate}{Extension}"                                  |
| "WOO_20170611_100000+1000.wav"                                                     | "2017-06-11T10:00:00"        | "+10:00"           | "WOO\_{StartDate}{Extension}"                                  |
| "20161108_075126_SunriseToSunset [-39.5336 -131.2711].wav"                         | "2016-11-08T07:51:26"        |                    | "{LocalStartDate}\_SunriseToSunset {Location}{Extension}"      |
| "acoustic_study_00m.mp3"                                                           |                              |                    | "acoustic_study_00m{Extension}"                                |
| "NW6-0009582_20131224_130100.wav"                                                  | "2013-12-24T13:01:00"        |                    | "NW6-0009582\_{LocalStartDate}{Extension}"                     |
| "20091219T070006+1000_00600.wav"                                                   | "2009-12-19T07:00:06"        | "+10:00"           | "{StartDate}\_00600{Extension}"                                |
| "5B07C752.WAV"                                                                     | "2018-05-25T08:20:34"        | "+00:00"           | "{StartDate}{Extension}"                                       |
| "5B07DEA0.WAV"                                                                     | "2018-05-25T10:00:00"        | "+00:00"           | "{StartDate}{Extension}"                                       |
| "5B07FAC0.WAV"                                                                     | "2018-05-25T12:00:00"        | "+00:00"           | "{StartDate}{Extension}"                                       |
| "5B0816E0.WAV"                                                                     | "2018-05-25T14:00:00"        | "+00:00"           | "{StartDate}{Extension}"                                       |
| "00000000.WAV"                                                                     | "1970-01-01T00:00:00"        | "+00:00"           | "{StartDate}{Extension}"                                       |
| "0_20120108_010000_000.wav"                                                        | "2012-01-08T01:00:00"        |                    | "0\_{LocalStartDate}{Extension}"                               |
| "0000514b-9329-404c-bdb3-a50827457b15_20100503-080000Z.mp3"                        | "2010-05-03T08:00:00"        | "+00:00"           | "0000514b-9329-404c-bdb3-a50827457b15\_{StartDate}{Extension}" |
| "DM420082_20111021_000000.MP3"                                                     | "2011-10-21T00:00:00"        |                    | "DM420082\_{LocalStartDate}{Extension}"                        |
| "EMER_20040521_201651.wav"                                                         | "2004-05-21T20:16:51"        |                    | "EMER\_{LocalStartDate}{Extension}"                            |
| "EMER_20000102_133112.wav"                                                         | "2000-01-02T13:31:12"        |                    | "EMER\_{LocalStartDate}{Extension}"                            |
| "20070415051314.wav.trimmed.wav"                                                   | "2007-04-15T05:13:14"        |                    | "{LocalStartDate}.wav.trimmed{Extension}"                      |
| "20070513081940.trimmed_manually.wav"                                              | "2007-05-13T08:19:40"        |                    | "{LocalStartDate}.trimmed_manually{Extension}"                 |
| "EMER_20000101_000553.wav"                                                         | "2000-01-01T00:05:53"        |                    | "EMER\_{LocalStartDate}{Extension}"                            |
| "OLONG-CH1_0+1_20171121$143444.wav"                                                | "2017-11-21T14:34:44"        |                    | "OLONG-CH1*0+1*{LocalStartDate}{Extension}"                    |
| "weird20180801_240000.aac"                                                         | "2018-08-01T24:00:00"        |                    | "weird{LocalStartDate}{Extension}"                             |
| "weird20180801_240000-1030.aac"                                                    | "2018-08-01T24:00:00"        | "-10:30"           | "weird{StartDate}{Extension}"                                  |
| "short_time_180801_1630_test.wav"                                                  | "2018-08-01T16:30:00"        |                    | "short*time*{LocalStartDate}\_test{Extension}"                 |
| "20180517_010348.5AFCD4F4.WAV"                                                     | "2018-05-17T01:03:48"        |                    | "{LocalStartDate}.5AFCD4F4{Extension}"                         |
| "OLONG-SOLAR_0+1_20180221T031609+1000.wav"                                         | "2018-02-21T03:16:09"        | "+10:00"           | "OLONG-SOLAR*0+1*{StartDate}{Extension}"                       |
| "OLONG-SOLAR_0+1_20180221$031609.wav"                                              | "2018-02-21T03:16:09"        |                    | "OLONG-SOLAR*0+1*{LocalStartDate}{Extension}"                  |
| "20151212_123456Z.mp3"                                                             | "2015-12-12T12:34:56"        | "+00:00"           | "{StartDate}{Extension}"                                       |
| "123_20131012_123456-9_456.mpg"                                                    |                              |                    | "123_20131012_123456-9_456{Extension}"                         |
| "123_20131012_123456-09_456.mpg"                                                   | "2013-10-12T12:34:56"        | "-09:00"           | "123\_{StartDate}\_456{Extension}"                             |
| "86f5923d-ef1d-4159-b120-a8dec3f6334e.wav"                                         |                              |                    | "86f5923d-ef1d-4159-b120-a8dec3f6334e{Extension}"              |
| "5AFCD4F45AFCD4F4.WAV"                                                             |                              |                    | "5AFCD4F45AFCD4F4{Extension}"                                  |
| "prefix5AFCD4F4prefix.WAV"                                                         |                              |                    | "prefix5AFCD4F4prefix{Extension}"                              |
| "20161108T075126.123456-0430_SunriseToSunset [-39.5336 -131.2711].wav"             | "2016-11-08T07:51:26.123456" | "-04:30"           | "{StartDate}\_SunriseToSunset {Location}{Extension}"           |
| "20091219T070006.789123+1130_00600.wav"                                            | "2009-12-19T07:00:06.789123" | "+11:30"           | "{StartDate}\_00600{Extension}"                                |
| "20091219T070006.789+1130_00600.wav"                                               | "2009-12-19T07:00:06.789"    | "+11:30"           | "{StartDate}\_00600{Extension}"                                |
| "a_2359-01012015_blah.dnsb48364JSFDSD"                                             | "2015-01-01T23:59:00"        |                    | "a\_{LocalStartDate}\_blah{Extension}"                         |
| "20180226*040000Z*+40.1213-075.0015+2.79CRSWGS_84.flac"                            | "2018-02-26T04:00:00"        | "+00:00"           | "{StartDate}\_{Location}{Extension}"                           |
| "671629352.181204100002.wav"                                                       | "2018-12-04T10:00:02"        |                    | "671629352.{LocalStartDate}{Extension}"                        |
| "20210617T080000+0000*Rec2*-18.2656+144.5564.flac"                                 | "2021-06-17T08:00:00"        | "+00:00"           | "{StartDate}_Rec2_{Location}{Extension}"                       |
| "PILLIGA*20121204_234600*+13-090.wav"                                              | "2012-12-04T23:46:00"        |                    | "PILLIGA*{LocalStartDate}*{Location}{Extension}"               |
| "FNQ-RBS_20190102_044802_010.wav"                                                  | "2019-01-02T04:48:02.010"    |                    | "FNQ-RBS\_{LocalStartDate}{Extension}"                         |
| "S20240815T091156.982648+1000*E20240815T091251.967555+1000*-12.34567+78.98102.wav" | "2024-08-15T09:11:56.982648" | "+10:00"           | "S{StartDate}_E{EndDate}_{Location}{Extension}"                |
| S20210205T035946676+1000*E20210205T040446501+1000*-08.0000+000.0000.wav            | 2021-02-05T03:59:46.676      | +10:00             | S{StartDate}_E{EndDate}_{Location}{Extension}                  |
| 2025-09-30T03:32:35.594002Z.wav                                                    | 2025-09-30T03:32:35.594002   | +00:00             | {StartDate}{Extension}                                         |
| 2025-09-30T03:32:35.594002.wav                                                     | 2025-09-30T03:32:35.594002   |                    | {LocalStartDate}{Extension}                                    |
