## Artifactory
- Hosted at https://binaries.avivagroup.com/ui/packages
- Contains a mirror of brew, pypi, npm etc
- Log in with just the A number (don't need the domain)

## WSS 
To turn off
`launchctl unload -w /Library/LaunchAgents/com.symantec.wssa.uix.plist`
Then go to VPN in settings and disable

`launchctl load -w /Library/LaunchAgents/com.symantec.wssa.uix.plist` to turn back on 
## Brew Bypass
Come off WSS, unset the proxies, go off network.
## Brew Actual
for brew with artifactory:
1. get an auth token via curl  -X POST -u AVIVAGROUPUSERNAMEHEREWITHOUTQUOTESANDNODOMAIN [https://binaries.avivagroup.com/artifactory/api/security/apiKey](https://binaries.avivagroup.com/artifactory/api/security/apiKey "https://binaries.avivagroup.com/artifactory/api/security/apikey")
2. add the following to .zshrc:
    1. `export HOMEBREW_DOCKER_REGISTRY_TOKEN=<the auth token from previous step>`
    2. `export PYTHONWARNINGS="ignore:Unverified HTTPS request"`
    3. `export HOMEBREW_ARTIFACT_DOMAIN=https://binaries.avivagroup.com/artifactory/<whateveryourremoteiscalled>`
