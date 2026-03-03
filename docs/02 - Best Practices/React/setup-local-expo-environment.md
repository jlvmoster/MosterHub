# How to Setup Your Local Environment for Expo React Native Projects

> At the time of writing, `Expo v53` is the current major version...

## Install ESlint and Prettier for Expo

Following this [documentation](https://docs.expo.dev/guides/using-eslint/), run the command below:

```bash
npx expo lint
```

```bash
npx expo install prettier eslint-config-prettier eslint-plugin-prettier --dev
```

## Modify ESLint config file called `eslint.config.js` in the project root

```javascript
// https://docs.expo.dev/guides/using-eslint/
const { defineConfig } = require("eslint/config");
const expoConfig = require("eslint-config-expo/flat");
const eslintPluginPrettierRecommended = require("eslint-plugin-prettier/recommended");

module.exports = defineConfig([
  expoConfig,
  eslintPluginPrettierRecommended,
  {
    ignores: [".expo/*", "dist/*", "node_modules/*"],
  },
]);
```

## Install and Configure `prettier`, `husky`, and `lint-staged`

To setup automatic style formatting on a pre-commit hook, first install the required packages as `devDependencies`:

```bash
npm i -D husky lint-staged
```

### Prettier

Then create a `.prettierrc.json` file with your preferred styling rules. Here's mine:

```json
{
  "arrowParens": "always",
  "bracketSameLine": false,
  "bracketSpacing": true,
  "embeddedLanguageFormatting": "auto",
  "endOfLine": "lf",
  "jsxSingleQuote": true,
  "printWidth": 100,
  "quoteProps": "as-needed",
  "semi": false,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "useTabs": false
}
```

Create a `.prettierignore` to exclude unneeded files (if necessary):

```
.expo
.idea
node_modules
package-lock.json
```

### Husky and Lint-Staged

To setup pre-commit on staged files, first setup a lint-staged script in `package.json` to run prettier on all specified files:

```
{
  ...
  "lint-staged": {
    "*.{js,ts,jsx,tsx}": [
      "eslint --fix",
      "prettier --write"
    ],
    "*.{html,css,json,yml,yaml,md,mdx}": [
      "prettier --write"
    ]
  }
  ...
}
```

Next, setup husky to install a pre-commit hook on `npm install` by adding an `npm prepare` script:

```bash
npx husky init
```

Set pre-commit hook

```bash
echo "lint-staged" > .husky/pre-commit
```
