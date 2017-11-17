Getting started with Vault
===================================

We provide all cerdentials via token from Vault. You will get a team-token from TECH-TEAM before the hack begins. Please follow this introduction:

1. Download Vault client package and install:
```
https://www.vaultproject.io/downloads.html
```

2. To verify your installation, open a terminal window and type:
```
vault -h
```

3. Export Vault environment variable: 
```
export VAULT_ADDR=https://cicd-vault.tools.msi.audi.com
```

4. Authenticate with the given token:
```
vault auth <GIVEN-TOCKEN>
```

5. Get all credentials for hackathon:
```
vault read HACKOVATION/team-0
```
Replace the team placeholder with your team-number