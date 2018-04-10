# IoT Package Manager

## Recommended Workflows


### Create an IPM Package via Developer Console

#### Steps

1. Go to Home Page
2. Select `Export Icon`
3. Log into your GitHub
4. Select assets to export
5. Choose a name, set tags, license
6. Provide image url (recommend imgur.com)
7. A repo will be created on your behalf with your system
8. Click Publish to head to ipm.clearblade.com
9. Log in / register
10. Publish package with the github url


### Update an IPM Package via CLI

Prerequisites

####Required

git   
cb-cli > 4.0    [cb-cli releases](https://github.com/clearblade/cb-cli/releases)

#### Optional  
jsdoc2md  

```
npm i -g jsdoc2md
```
#### Steps

1. git clone <YOUR_REPO> && cd <YOUR_REPO>
2. cb-cli init
3. cb-cli export/pull
4. Make changes
5. Document jsdoc: `jsdoc2md ./code/*/*/*.js > jsdoc.md && cat jsdoc >> Readme.md`
5. 	git add, commit, push

## Alternative Workflows

### Create an IPM Package via CLI

1. On Github, create a new repo
2. `cb-cli export` your system to your filesystem
3. curl https://docs.clearblade.com/v/3/static/ipm/package.json
4. edit package.json with name, version, owner, tags, image url
5. (optional) jsdoc2md ./code/*/*/*.js > jsdoc.md && cat jsdoc >> Readme.md
4. git init
5. git remote add origin <GITHUB_URL>
6. git add * && git commit -am "initial" && git push origin master -u 
7. Go to ipm.clearblade.com to publish package