# IoT Package Manager

 
## Brief intro to ClearBlade Platform

When a developer ready to begin using the ClearBlade Platform the first element that must be created is a System.

This System represents a backend for the mobile app(s), web dashboard, fat clients or IoT networks that need a common system of record. The System contains

* an API for clients to consume
* data saved in well defined structures
* custom business logic
* messages being published
* a role based authority model for users and devices
* a bunch of assets which user can work with. Ex: Code Services, Code Libraries, Adapters, Portals etc. 

Within the Code section of a System you can device two types of Code that ultimately make up the application layer of your System

Services are available externally and called by clients via HTTP or MQTT
Libraries are lines of javascript that can be included into services to provide reusable logic
    
   __Note__: _The code in javascript for code services and libraries needs to be in es5 strictly. So it's a good idea to test it on ClearBlade platform's code-service by importing it._ 

## What is IPM?
IPM is IoT Package manager, which allows developers to share their complete IoT solutions or templates. All the assets can be shared. The assets which have the potential to be highly re-usable are services, libraries, adapters & portals. But again all the assets can be shared. 

## The need for IPM

As in the world of IoT, there is a lot of scope reusability of the code you write. ClearBlade provides a way to the user to share his/her system with all it's assets and use somebody else's system in their system, by importing it. 
And these shared systems are opensource, because __Sharing is Caring !__


## Creating/Updating IPM package
### --> Recommended Workflow:
#### 1. Create an IPM Package via ClearBlade [Developer Console](https://platform.clearblade.com)

##### Please register on the above link and create a account on ClearBlade platform if not done already.

##### Once the account is created, follow these steps:

* Create a new system
* Create code libraries
* Test them by importing them into code services.
* Once it looks like the system is ready (more features can be added refer [Update an IPM Package](#Update-an-IPM-Package-via-CLI) )  
* Go to Home Page
* Select `Export Icon` on the system
* Log into your GitHub
* Select assets to export
* Choose a name, set tags, license
* Provide image url (recommend imgur.com)
* A repo will be created on your behalf with your system
* Click Publish to head to [ipm.clearblade.com](https://ipm.clearblade.com)
* Log in / register
* Publish package with a relevant name and the github url.

### 2. Update an IPM Package via CLI

#### Prerequisites

##### Required

>git   
>cb-cli > 4.0    [cb-cli releases](https://github.com/clearblade/cb-cli/releases)

##### Optional 
Helper tool for documenting library using jsdoc.
>jsdoc2md  

```
npm i --save-dev jsdoc2md
```
#### Steps

* git clone <YOUR_REPO> && cd <YOUR_REPO>
* cb-cli init
* cb-cli export/pull
* Make changes
* Document jsdoc: `jsdoc2md ./code/*/*/*.js > jsdoc.md && cat jsdoc.md >> Readme.md`
* git add, commit, push
* Imports by other users is made from the master branch. So make sure the _master branch_ has the latest edits.



### --> Alternative Workflow

#### Create an IPM Package via CLI

* On Github, create a new repo.
* `cb-cli export` your system to your filesystem
* Whenever working with ClearBlade System, and using the CLI make sure you're in the root system folder. (`ls` in that directory should show `system.json`)
* Follow this [Sample-Package.json](https://raw.githubusercontent.com/ClearBlade/ipm/master/Sample-Package.json) or use the curl: `curl https://raw.githubusercontent.com/ClearBlade/ipm/master/Sample-Package.json -o package.json`
* edit package.json with name, version, owner, tags, image url and other relevant fields, the sample package.json is pre-filled with, ensure changing them before publishing.
* (Another option would be to download an [Empty-Package.json](https://raw.githubusercontent.com/ClearBlade/ipm/master/Sample-Package.json) or use the Curl: `curl https://raw.githubusercontent.com/ClearBlade/ipm/master/Sample-Package.json -o package.json`) 
* (optional) `jsdoc2md ./code/*/*/*.js > jsdoc.md && cat jsdoc >> Readme.md`
* List of required files: 

>1. system.json
>2. package.json
>3. .gitignore 
		
* git init
* Add ".cbmeta" & "jsdoc.md to `.gitignore`
* **Note**: `.cbmeta has credentials like authtoken, so it's advisible to put them in .gitignore, and not upload to github`
* git remote add origin \<GITHUB_URL\>
* git add . && git commit -am "initial" && git push origin master -u 
* Go to [ipm.clearblade.com](https://ipm.clearblade.com) to publish package
