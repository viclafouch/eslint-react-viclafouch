# Eslint / Prettier Setup of @viclafouch 📦

These are the ESLint and Prettier settings for a Next.js project ⚡️


# Table of Contents

- [Eslint / Prettier Setup of @viclafouch 📦](#eslint--prettier-setup-of-viclafouch-)
- [Table of Contents](#table-of-contents)
  - [What it does](#what-it-does)
  - [Local / Per Project Install](#local--per-project-install)
  - [If you use JavaScript](#if-you-use-javascript)
    - [Scripts](#scripts)
  - [If you use TypeScript](#if-you-use-typescript)
    - [Extend your tsconfig](#extend-your-tsconfig)
    - [Better typing](#better-typing)
    - [Scripts](#scripts-1)
  - [If you use Next.js](#if-you-use-nextjs)
  - [If you use React.js](#if-you-use-reactjs)
  - [If you want to use Prettier](#if-you-want-to-use-prettier)
  - [If you use VS Code](#if-you-use-vs-code)

## What it does

* Lints JavaScript / TypeScript based on the latest standards
* Multiple configs `react` `hooks` `next`..
* Shared `tsconfig.json`
* Fixes issues and formatting errors with Prettier
* Check for accessibility rules on JSX elements.

## Local / Per Project Install

1. If you don't already have a `package.json` file, create one with `npm init`.

2. Then we need to install everything needed by the config:

```
npx install-peerdeps --dev @viclafouch/eslint-config-viclafouch
```

3. You can see in your package.json there are now a big list of devDependencies.

4. Create a `.eslintrc` file in the root of your project's directory (it should live where package.json does). Your `.eslintrc` file should look like this:

5. Extends your config with the minimal base of Frichti config :

```json
{
  "extends": [
    "@viclafouch/eslint-config-viclafouch"
  ]
}
```

## If you use JavaScript

You can remove these unnecessary packages (you don't need the TypeScript support)

```diff
{
  "devDependencies": {
- "@typescript-eslint/eslint-plugin": "xxx",
- "@typescript-eslint/parser": "xxx",
- "typescript": "xxx"
  }
}
```

### Scripts

You can add two scripts to your package.json to lint and/or fix your code:

```json
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "npm run lint -- --fix",
  }
}
```
## If you use TypeScript

### Extend your tsconfig

First, extend your current config file `tsconfig.json` with this following snippet:

```json
{
  "extends": "@viclafouch/eslint-config-viclafouch/tsconfig.json",
  ...
}
```

Then, add the TypeScript Eslint rules to your `.eslintrc` file:

```js
{
  extends: [
    '@viclafouch/eslint-config-viclafouch',
    '@viclafouch/eslint-config-viclafouch/typescript'
  ],
  parserOptions: {
    project: true,
    tsconfigRootDir: __dirname
  },
  root: true
}
```

Then, you can remove these following unnecessary packages (you don't the Babel parser, we use `@typescript-eslint/parser`) instead.


```diff
{
  "devDependencies": {
- "@babel/core": "xxx",
- "@babel/eslint-parser": "xxx"
  ...
  }
}
```

### Better typing

TypeScript's built-in typings are not perfect. frichti-reset makes them better.

1. Create a `reset.d.ts` file in your project with these contents:

```ts
// Do not add any other lines of code to this file!
import '@viclafouch/eslint-config-viclafouch/reset.d'
```

2. Enjoy improved typings across your entire project.

### Scripts

You can add two scripts to your package.json to lint and/or fix your code:

```json
{
  "scripts": {
    "lint": "tsc --noEmit && eslint . --ext .js,.jsx,.ts,.tsx",
    "lint:fix": "npm run lint -- --fix",
  },
}
```

## If you use Next.js

You can also add additional rules for Next.js. It includes the following configurations : `@viclafouch/eslint-config-viclafouch/react`, `@viclafouch/eslint-config-viclafouch/hooks` and Next.js specific rules.

```js
{
  extends: [
    '@viclafouch/eslint-config-viclafouch',
    '@viclafouch/eslint-config-viclafouch/next'
  ],
}
```

## If you use React.js

You can also add additional rules for only React.js ecosystem (without Next.js).

```js
{
  extends: [
    '@viclafouch/eslint-config-viclafouch',
    '@viclafouch/eslint-config-viclafouch/react',
    '@viclafouch/eslint-config-viclafouch/hooks'
  ],
}
```


## If you want to use Prettier

Be sure to add the prettier config at the end of your `extends` array.

```js
{
  extends: [
    '@viclafouch/eslint-config-viclafouch',
    '@viclafouch/eslint-config-viclafouch/react',
    '@viclafouch/eslint-config-viclafouch/hooks',
    '@viclafouch/eslint-config-viclafouch/prettier' // be sure to be the last
  ],
}
```

## If you use VS Code

Once you have done. You probably want your editor to lint and fix for you.

1. Install the [ESLint package](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
2. Now we need to setup some VS Code settings. Create a `.vscode` folder at your root project, and create a `settings.json` file in this folder. Then, add this little config:

```js
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```