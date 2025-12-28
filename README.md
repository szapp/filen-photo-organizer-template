# Filen Photo Organizer

Automatically organize photo and camera uploads on your [Filen.io](https://filen.io) drive.

Source template: [szapp/filen-photo-organizer-template](https://github.com/szapp/filen-photo-organizer-template)  
Based on Github Action: [szapp/filen-photo-organizer](https://github.com/szapp/filen-photo-organizer)

## Create your own

[![Use me](https://img.shields.io/badge/template-use%20me-green?style=for-the-badge&logo=github)](https://repo.new/?template_name=filen-photo-organizer-template&template_owner=szapp&name=filen-photo-organizer&description=Automatically%20organizes%20my%20filen.io%20photos)

Click the link above to set up the photo organizer for your own filen.io drive with minimal effort.

## Setup

### 1. Create a repository from this template by using the link above

### 2. Setup the login credentials as repository secrets

Head to the repository settings and navigate to the secrets and variables configuration, found in the section `Security` in `Secrets and variables` -> `Actions`

Create three repository secrets in the `Secrets` tab.

- `FILEN_EMAIL`: Enter your filen.io account login email
- `FILEN_PASSWORD`: Enter your filen.io account login password
- `FILEN_TFA`: Enter your filen.io account two-factor authentication secret, not the generated OTP. This is secret is only needed if you have TFA set up

ℹ️ **Note** Before submitting, make sure you are creating a secret (obscured) and not variable (plain text)!

### 3. Setup the configuration as repository variables

Switch to the `Variables` tab and create three repository variables.

- `ROOT_PATH`: Enter the desired path to the photo directory in your filen.io drive.
- `RECURSIVE`: Enter `true` or `false` to include or exclude files in sub-directories.
- `CONVERT_HEIC`: Enter `true` or `false` to convert HEIC/HEIF files or retain the format.
- `KEEP_ORIGINALS`: Enter `true` or `false` to copy/keep or delete/move the source files.
- `DESTINATION_PATH`: Enter a destination path relative to `ROOT_PATH` (specify an absolute path with a leading `/`), e.g. specify an empty value to create directories inside `ROOT_PATH`. If `RECURSIVE` is `true`, the destination has to be outside of `ROOT_PATH`, i.e. either start with `../` or with `/`.
- `DIR_PATTERN`: Enter a date-time pattern for the directory names to sort the photos into. If empty, no separte directories will be created within `DESTINATION_PATH`, and `FILE_PATTERN` must not be empty. [Format][date-format-link], e.g. `yyyy-MM` places photos taken in the March 2024 into the sub-directory `2024-03`.
- `FILE_PATTERN`: Enter a date-time pattern for renaming the files based on date-taken. If empty, files will not be renamed and `DIR_PATTERN` must not be empty. E.g. `yyyy-MM-dd_HH.mm.ss` renames a JPG photo taken on March 4th, 2024 at 21:15:12 to `2024-03-4_21.15.12.jpg`.
- `FALLBACK_TIME_ZONE`: Enter your local time zone as [TZ/IANA identifier][timezones-link], e.g. `Europe/Berlin`. This time zone will be used when no GPS metadata is found, to determine the local time a photo was taken. If omitted, defaults to `Europe/Berlin`.

The destination path of the organized photos and videos will be the composition of `DESTINATION_PATH / DIR_PATTERN / FILE_PATTERN.jpg`, e.g. `../../organized/2024-03/2024-03-4_21.15.12.jpg`.

### 4. Enjoy

Once the variables and secrets are properly configured, the photo directory will be organized periodically.

The Github workflow runs in intervals of every second hour between 5:00 and 22:00 UTC daily. This time range coincides well with day time in Central and Western European countries. If you live outside of Europe, you might want to update these values. You can adjust the schedule in the file `.github/workflows/organize.yml`.

The most frequent a scheduled GitHub workflow can run is every 5 minutes. However, with the monthly 2.000 computing minutes quota for free GitHub accounts
and an estimated average run time of this workflow of 5 minutes at generous photographing, the proposed schedule here of every second hour during day time or less is highly recommended.

You can inspect the organization operations in the `Actions` tab in your repository in the section `Workflows` -> `Organize photos`.

## Note for changing from V1 to V2

With the introduction of time-zone-aware time stamps, there are breaking changes in V2. Please update the time formats in `DIR_PATTERN` and `FILE_PATTERN` (if used) based on different [date formatting][date-format-link]. Additionally, a new GitHub variable was added to specify the user default time zone, see above.

## Note for changing from V2 to V3

When updating from V2 to V3, update `twoFactorCode` into `twoFactorSecret` in the workflow file.

## Note for changing from V3 to V4

When updating from V3 to V4, no changes have to be made to retain the old behavior. But the additional options `RECURSIVE`, `CONVERT_HEIC`, `KEEP_ORIGINALS`, and `DESTINATION_PATH` are available.

## GitHub Action

For more information, visit the repository of the GitHub Action [szapp/filen-photo-organizer](https://github.com/szapp/filen-photo-organizer).

[date-format-link]: https://moment.github.io/luxon/#/formatting?id=table-of-tokens
[timezones-link]: https://en.wikipedia.org/wiki/List_of_tz_database_time_zones
