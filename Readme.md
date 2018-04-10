# IoT Package Manager

## Recommended Workflows


### Create an IPM Package via Developer Console

1. Go to Home Page
2. Select `Export Icon`
3. Log into your GitHub
4. Select assets to export
5. Choose a name, set tags, license
6. Provide image url (recommend imgur.com)
6. A repo will be created on your behalf with your system


### Update an IPM Package via CLI

Prerequisites

Required

git  
cb-cli > 4.0  
[cb-cli releases](https://github.com/clearblade/cb-cli/releases)

Optional  
jsdoc2md  

```
npm i -g jsdoc2md
```

1. git clone <YOUR_REPO> && cd <YOUR_REPO>
2. cb-cli init
3. cb-cli export/pull
4. Make changes
5. Document jsdoc: `jsdoc2md ./code/*/*/*.js > jsdoc.md && cat jsdoc >> Readme.md`
5. 	git add, commit, push