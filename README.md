# Port

## Pre-requisites

- Node = 16.15.0

## How to use this monorepo

This Monorepo uses [Yarn 3 (Berry)](https://yarnpkg.com/), in order to install Yarn, follow the guide [here](https://yarnpkg.com/getting-started/install)

### For quick installation reference:

```
npm i -g corepack
corepack enable
yarn set version 3.2.3
```

### Install packages:

```
yarn install
```

### Add a package to a specific workspace

```
yarn workspace <workspace_name> add <package_name>
```

or add a development package:

```
yarn workspace <workspace_name> add -D <package_name>
```

### Run a script from a specific workspace

```
yarn run workspace <workspace_name> run <command_name>
```

## Monorepo Structure

The monorepo root directory includes general config files, the yarn configuration and a general `package.json` file specifying the workspace paths

All microservices and packages are under the `apps` folder

Shared packages should go under the `packages` folder

### Typescript builds of shared packages

Note that shared packages use the `"composite": true` flag, this means they are what Typescript calls - Incremental Builds. In case you want to completely regenerate the compiled output of such a shared package, you need to delete both the `dist` folder and the `tsconfig.tsbuildinfo` file in the directory of the specific shared package, after that running a build command will rebuild the `dist` directory

### Using scripts from packages

If you want to run the `start` script from package `cool-service`, you can do one of the following:

1. Run the command `yarn workspace cool-service run start`
2. Add the line `"cool:start": "yarn workspace cool-service run start"` to the root `package.json` scripts block, and then run `yarn run cool:start`

## Yarn vs NPM cheatsheet

Add a package

```
# NPM
npm install <package>

# Yarn
yarn add <package>
```

Add a development package

```
# NPM
npm install --save-dev <package>

# Yarn
yarn add -D <package>
```

Install packages

```
# NPM
npm install

# Yarn
yarn install
```

Execute package binaries (NPX)

```
# NPM
npx create-react-app my-website

# Yarn - doesn't have an official replacement for npx but using yarn create or yarn dlx usually does the trick
```

Perform outdated package upgrading

```
# NPM
npm outdated
npm update

# Yarn
yarn plugin import interactive-tools
# To view an interactive CLI interface to update packages run:
yarn interactive-upgrade
# To just update packages everywhere run
yarn up -R '**'
```

## TODO

1. Create a general docker-compose file for all services
2. create general config files and store them in the root directory, and add proper overriding config files in the microservice subdirectories
