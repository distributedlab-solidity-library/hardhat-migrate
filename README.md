[//]: # ([![npm]&#40;https://img.shields.io/npm/v/@dlsl/hardhat-deploy.svg&#41;]&#40;https://www.npmjs.com/package/@dlsl/hardhat-deploy&#41; [![hardhat]&#40;https://hardhat.org/buidler-plugin-badge.svg?1&#41;]&#40;https://hardhat.org&#41;)

# Hardhat migrate

[Hardhat](https://hardhat.org) plugin to simplify the deployment and verification of contracts 
to [Etherscan](https://etherscan.io).

## What

This plugin helps you deploy verify the source code for your Solidity contracts on [Etherscan](https://etherscan.io).

This is a fairly simple and rather straightforward Hardhat plugin:

- For deployment, it uses [@truffle/deployer](https://www.npmjs.com/package/@truffle/deployer) and 
[@truffle/reporters](https://www.npmjs.com/package/@truffle/reporters) to report on the deployment process.

- For verification, it uses [@nomiclabs/hardhat-etherscan](https://www.npmjs.com/package/@nomiclabs/hardhat-etherscan)

## Installation

```bash
npm install --save-dev @dlsl/hardhat-migrate
```

And add the following statement to your `hardhat.config.js`:

```js
require("@dlsl/hardhat-migrate");
```

Or, if you are using TypeScript, add this to your `hardhat.config.ts`:

```ts
import "@dlsl/hardhat-migrate";
```

## Naming convention

It is also **mandatory** to observe the naming convention for migrations such as this one:
> X_migration_name.migration.js

* Where **X** is the serial number in which your migrations will be applied.
* migration_name is simply the name of the migration.

## Tasks

This plugin provides the `deploy` task, which allows you to deploy and verify contracts.

Under the hood, for verification process, it uses [@nomiclabs/hardhat-etherscan](https://www.npmjs.com/package/@nomiclabs/hardhat-etherscan) 
plugin.  

> :warning: **Hardhat Config**: Make sure they are follow the docs from @nomiclabs/hardhat-etherscan. 

Do not import @dlsl/hardhat-migrate and @nomiclabs/hardhat-etherscan together, under the hood in @dlsl/hardhat-migrate.
@nomiclabs/hardhat-etherscan is already imported.

> :x: **Wrong way**
```js
require("@nomiclabs/hardhat-etherscan");
require("@dlsl/hardhat-migrate");
```

> :heavy_check_mark: **Right way**
```js
require("@dlsl/hardhat-migrate");
```


To view the available options, run the command (help command):
```bash
npx hardhat help deploy
```

## Environment extensions

This plugin does not extend the environment.

## Usage

You need to add the following Deploy config to your `hardhat.config.js` file:

```js
module.exports = {
  migrate: {
    verify: true,
    confirmations: 5,
    pathToMigrations: "./deploy/"
  }
};
```

[//]: # (## How it works)

## Known limitations

- Adding, removing, moving or renaming new contracts to the hardhat project or reorganizing the directory structure of contracts after deployment may alter the resulting bytecode in some solc versions. See this [Solidity issue](https://github.com/ethereum/solidity/issues/9573) for further information.
