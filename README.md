# LaunchDarkly Flag Sync

Get an Access Token: https://app.launchdarkly.com/settings/authorization

Additional Documentation: https://docs.launchdarkly.com/home/account-security/api-access-tokens

Write out a file: `main.yaml` in current directory.

## Format
`project_key`: Project being targeted.
`environment_source`: Environment settings are copied from.
`environment_targets`: List of Environments settings are copied to.
`flags`: List of Flags to have their settings copied.

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

### Running
This will mount your current directory which should contain a `main.yaml` file into the container and sync the flags.
```docker run -v "${PWD}":/ansible/playbooks/vars -e LAUNCHDARKLY_ACCESS_TOKEN="<REPLACE-API-TOKEN>" intheclouddan/flag-sync:latest```
