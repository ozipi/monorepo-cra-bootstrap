# monorepo-cra-bootstrap
monorepo with cra bootstrap example

Create the app in another location
===
# go to some temporary location
cd /tmp
# make the app
create-react-app web
# get rid of node modules and yarn.lock
rm -rf web/node_modules yarn.lock
# move it to the workspaces
mv web ./apps
cd ./apps/web
===

install the yarn packages
===
yarn add --dev react-app-rewired react-app-rewire-yarn-workspaces
===

Swap the start, build, and test scripts in package.json for these:
===
"start": "react-app-rewired start",
"build": "react-app-rewired build",
"test": "react-app-rewired test --env=jsdom",
===

copy config.overrides.js from exampleApp to the new app location

create a test code using the core/test from the new app
===
import test from 'core/test'
console.log("exampleApp::test", test())
===

last step
===
cd monorepo-cra-bootstrap
rm -rf node_modules core/node_modules views/node_modules native/node_modules web/node_modules
yarn
===

