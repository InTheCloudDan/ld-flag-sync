# LaunchDarkly Flag Sync

Get an Access Token: https://app.launchdarkly.com/settings/authorization

Additional Documentation: https://docs.launchdarkly.com/home/account-security/api-access-tokens

Write out a file: `main.yaml` in current directory.

## Format
`project_key`: Project being targeted.
`environment_source`: Environment settings are copied from.
`environment_targets`: List of Environments settings are copied to.

You can omit both, or have either `flag_filter` or `flags` but not both.

`flag_filter`: Optional - map that accepts a key `tag` to filter flags for.
`flags`: Optional - List of Flags to have their settings copied.  If omitted, all flags will be copied.

`included_actions`/`excluded_actions`: Optional - Define the parts of the flag configuration that will be copied (or not copied for excluded_actions). By default, the entire flag configuration will be copied.

You can have either `included_actions` or `excluded_actions` but not both.

Valid `included_actions` and `excluded_actions` include:
```
updateOn
updatePrerequisites
updateTargets
updateRules
updateFallthrough
updateOffVariation
```

## Sample Configuration files:
### List of Flags:
```
project_key: demo-project
environment_source: test
environment_targets:
    - production
flags:
    - chatbox
    - show-widgets
    - dark-theme
```
### Filtered:
```
project_key: demo-project
environment_source: test
environment_targets:
    - production
flag_filter:
    tag: release-1-0
```
### All:
```
project_key: demo-project
environment_source: test
environment_targets:
    - production
```
## Running
This will mount your current directory which should contain a `main.yaml` file into the container and sync the flags.
```docker run -v "${PWD}":/ansible/playbooks/vars -e LAUNCHDARKLY_ACCESS_TOKEN="<REPLACE-API-TOKEN>" intheclouddan/flag-sync:latest```

A number of tasks will be skipped each run. This is expected and settings will still be copied.
