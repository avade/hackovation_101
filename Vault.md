Getting started with HashiCorp Vault
===================================
Placeholder short vault description

# Installation steps:
## download and install the vault client binaries for your OS from URL:
https://www.vaultproject.io/downloads.html </br>
test the installation with `vault -h`
## export the Environment variable, depends on your OS, in *UNIX OS like this:
`export VAULT_ADDR=https://cicd-vault.tools.msi.audi.com`
## authenticate yourself with the given token like:
replace the given token with your team given token
`vault auth <given-token>`
## Retrieving your Hackathon credentials
replace the team placeholder with your team number
`vault read HACKOVATION/<team-1>`

