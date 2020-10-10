# ServiceNow CI/CD GitHub Action for Rollback Plugin

Rollback a desired plugin on ServiceNow instance.

# Usage
## Step 1: Collect the data from ServiceNow
Collect all required data from the ServiceNow - username, password, instance
## Step 2: Configure Secrets in your GitHub repository
On GitHub, go in your repository settings, click on the secret _Secrets_ and create a new secret.

Create secrets called 
- `SNOW_USERNAME`
- `SNOW_PASSWORD`
- `SNOW_INSTALL_INSTANCE` **domain** only required from the url like https://**domain**.service-now.com

## Step 3: Configure the GitHub action
```yaml
- name: Rollback Plugin 
  if: ${{ failure() && steps.activate_plugin.outputs.failed }} # Runs if Activate Plugin step is failed
  uses: ServiceNow/sncicd_plugin_rollback@1.0 # like username/repo-name
  with:
    pluginID: 
  env:
    snowUsername: ${{ secrets.SNOW_USERNAME }}
    snowPassword: ${{ secrets.SNOW_PASSWORD }}
    snowInstallInstance: ${{ secrets.SNOW_INSTALL_INSTANCE }}
```
Inputs:
- **pluginID** - Plugin ID for rollback (like com.servicenow_now_calendar)

Environment variable should be set up in the Step 1
- snowUsername - Username to ServiceNow instance
- snowPassword - Password to ServiceNow instance
- snowInstallInstance - ServiceNow instance where plugin will be rolled back

## Tests

Tests should be ran via npm commands:

#### Unit tests
```shell script
npm run test
```   

#### Integration test
```shell script
npm run integration
```   

## Build

```shell script
npm run buid
```

## Formatting and Linting
```shell script
npm run format
npm run lint
```
