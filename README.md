# monorepo-cra-bootstrap
This is a walktrough to create monorepos with cra using [raact-app-rewired](https://github.com/timarney/react-app-rewired) and [yarn-workspaces-cra-crna](https://github.com/viewstools/yarn-workspaces-cra-crna)

## Summary
you sometimes need share code about our React components between multiple apps, including WEB, Mobile with React Native
A solution very easy and fast is using Yarn Workspaces, this allow us have shared components in many apps.

## Overview
Our repository will have the follow structure
```sh
.
+-- core
    +-- mycomponent
    +-- ...
    +-- package.json
+-- apps
    |
    +-- webapp(use Create React App)
        +-- config-override.js
        +-- package.json
    +-- webadmin(use Create React App)
        +-- config-override.js
        +-- package.json
    +-- morewebapps...
+-- package.json
```

core folder will hold all react components
apps folder are our diferents aplications written in React, we must add a config-override file for each.

## Getting started

### Step 1: Create the apps in other location
we need create our apps with React using create-react-app.

In every package.json rename the scripts to:
```json
...
"scripts": {
    "start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react-app-rewired test --env=jsdom",
    "eject": "react-app-rewired eject"
  },
...
```
and the config-override.js in the root of every project, see [structure](##overview)
```js
const rewireYarnWorkspaces = require('react-app-rewire-yarn-workspaces');
module.exports = function override(config, env) {
	return rewireYarnWorkspaces(config, env);
};
```
now install
```bash
$> yarn add --dev react-app-rewired react-app-rewire-yarn-workspaces
```
and get rid of node_module folders and yarn.lock file
```
rm -rf node_module yarn.lock
```

## Step 2: Core folder
those are our shared components.
for this example will add the package.json and a test file

package.json:
```json
{
	"name": "core",
	"version": "0.0.1"
}
```

### Step 3: Create our main folder
Here is where applications will live, for example MyWorkspaceCompany, and move in the apps we created early,
```
mv .../myapp1 ./MyWorkspaceCompany/apps
mv .../myapp2 ./MyWorkspaceCompany/apps
...
```
after adding a package.json file inside MyWorkspaceCompany with:
```json
{
  "private": true,
  "workspaces": [
    "apps/react-app1",
    "apps/react-app2",
    "core"
    ...
  ]
}
```

### Step 4 install dependencies
move to the MyWorkspaceCompany folder and run:
```
yarn install
```

that is it!
