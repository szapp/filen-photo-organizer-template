# Filen Photo Organizer

Automatically organize photo and camera uploads on your [Filen.io](https://filen.io) drive.

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

- `ROOT_PATH`: Enter the desired path to the photo directory in your filen.io drive
- `DIR_PATTERN`: Enter a date-time pattern for the directory names to sort the photos into. [Format][date-format-link]. If empty, no directories will be created. If omitted, defaults to `YYYY-MM`, which places photos taken in the March 2024 into the sub-directory `2024-03`
- `FILE_PATTERN`: Enter a date-time pattern for renaming the files based on date-taken. If empty, files will not be renamed. If omitted, defaults to `YYYY-MM-DD_HH.mm.ss`, which renames a JPG photo taken on March 4th, 2024 at 21:15:12 to `2024-03-4_21.15.12.jpg`

### 4. Enjoy

Once the variables and secrets are properly configured, the photo directory will be organized periodically at intervals of 10 minutes between 6:00 and 22:00 UTC. You can adjust the schedule in the file `.github/workflows/organize.yml`.

You can inspect the organization operations in the Actions tab in your repository in the section `Workflows` -> `Organize photos`.

## GitHub Action

For more information, visit the repository of the GitHub Action [szapp/filen-photo-organizer](https://github.com/szapp/filen-photo-organizer).
