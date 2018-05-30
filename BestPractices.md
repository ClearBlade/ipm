# Developing IPM Packages - Best Practices
v1.0

## Terminology
`Asset` - any single, indivisible component of an IoT System (example a Device, User, or a Portal)


## Package-wide conventions

### 1. Casing Conventions


|  Asset |  Casing | Example  |
|---|---|---|
| System Name  |  train-case | gcloud-bigquery  |
|  Collection Name |  snake_case |  dropbox_resources |
|  Collection Column Name | snake_case  | user_id  |
|  Code Service Name | PascalCase  |  FetchMyPosition |
|  Code Library Name |  PascalCase |  GPSLibrary |
| Edge,Trigger,Timer,Device,Portal,Else  |  PascalCase |  GPSDevice|
|  Code Service Params |  snake_case or camelCase | user_id, userID
|  Code Service variables | camelCase  |  userID |

### 2. Naming Conventions

| Type | Rule | Example |
|---|---|---|
|Example|\<PACKAGE_NAME\>Example|GCloudExample|
|Reusable Library|\<PACKAGE_NAME\>Lib|GCloudLib|
|Constants|\<PACKAGE_NAME\>Constants|GCloudConstants|

## Documenting your Code

### Javascript Code

##### 1. JSDoc your code using standardize syntax here:

All Code Service and Library code must be fully documented with [JSDoc](usejsdoc.org)

Example

```
/**
 * @typedef DBConnector
 * @param {string} uri URI to connect to DB
 * @returns {boolean} connectionStatus
 * 
 * DBConnector for connecting to special databases
 */
function DBConnector(uri){
	...
	return true
}
```
##### 2. Generate markdown and append to Readme.md

We use a tool called `jsdoc2md`. It ingests all the system's code services and libraries, and outputs markdown documentation

```
npm install -g jsdoc-to-markdown
jsdoc2md code/*/*/*.js >> Readme.md
```

## Revision History
| Version | Date | Notes | Author |
|---|---|---|---|
|1.0| 2018-05-29 | Draft | Robert Reinold |

