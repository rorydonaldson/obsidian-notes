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
Come off WSS, unset the proxies and curl ca bundle, go off network.
## Brew Actual
for brew with artifactory:
1. `get an auth token via curl  -X POST -u AVIVAGROUPUSERNAMEHEREWITHOUTQUOTESANDNODOMAIN https://binaries.avivagroup.com/artifactory/api/security/apikey
2. add the following to .zshrc:
    1. `export HOMEBREW_DOCKER_REGISTRY_TOKEN=<the auth token from previous step>`
    2. `export PYTHONWARNINGS="ignore:Unverified HTTPS request"`
    3. `export HOMEBREW_ARTIFACT_DOMAIN=https://binaries.avivagroup.com/artifactory/<whateveryourremoteiscalled>`

## npm
1. Generate an auth token at https://binaries.avivagroup.com/ui/repos/tree/General/npm-virtual
	1. Remember to regenerate anytime your password is changed
2. Add a file at `~/.npmrc` as below

```
registry=https://binaries.avivagroup.com/artifactory/api/npm/npm-virtual/  
email=<firstname.lastname>@aviva.com  
always-auth=true  
noproxy[]=binaries.avivagroup.com  
//binaries.avivagroup.com/artifactory/api/npm/npm-virtual/:_auth="<owntoken>"
```

## PyPI

Run the below:
```
pip config --user set global.trusted-host "binaries.avivagroup.com"
pip config --user set global.index-url https://binaries.avivagroup.com/artifactory/api/pypi/pypi-virtual/simple
```
Add the following to `~/.zshrc`:
```
export http_proxy="http://ep.threatpulse.net:80"
export https_proxy="http://ep.threatpulse.net:80"
export CURL_CA_BUNDLE="$HOME/.certs/ca-bundle.crt"
export no_proxy="binaries.avivagroup.com,localhost,127.0.0.1,host.docker.internal,10.0.0.0/16,192.168.59.0/24,192.168.49.0/24,192.168.39.0/24,192.168.49.2,.avivacloud.com
```
If you don't have the cert bundle, can get from here https://github.com/aviva-verde/data-engineering-tools/tree/main/onboarding/certs

> Note: You will need to be on the VPN or office network for this to work 

## Go Proxy
Add the following to `~/.zshrc`:
`export GOPROXY="https://binaries.avivagroup.com/artifactory/api/go/go-github-virtual"`

## Pyenv 
Need CA certs set, then can pyenv install

## Slack
- Some features don't work

## Copilot
- Need to speak to James Cryer for co-pilot licence
- Need you added to an AD group for proxy unblock https://itselfservice.avivagroup.com/index.aspx?sf=a7c2c7a8-ee81-41f1-a18a-f84e867942dd


## OpenAI/ChatGPT
- Access can be granted by going to https://itselfservice.avivagroup.com/ --> system access request, and then searching for Generative AI

## AWS 
- Run `aws-vault exec aviva-data-testing` to set the profile
- Needs the proxies turned off 
- Can do like `aws-vault exec aviva-data-testing aws s3 ls`
- 