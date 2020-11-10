# Modern Angular Starter

This project includes:

- ESLint
- Prettier
- Jest
- Cypress

## Steps

Clone this project or do the belows step by yourself

```bash
ng new modern-angular-starter --skipInstall --strict --style=scss
cd modern-angular-starter
yarn install
```

1. Replace TSLint and Codelyzer with ESLint and @angular-eslint
2. Install Prettier
3. Replace Karma and Jasmine with Jest
4. Replace Protractor with Cypress

### 1. Replace TSLint and Codelyzer with ESLint and @angular-eslint

```bash
# Remove tslint config
rm tslint.json

# Uninstall tslint and codelyzer
yarn remove \
  tslint \
  codelyzer

# Install @angular-eslint and eslint and @typescript-eslint
ng add @angular-eslint/schematics

# Add .eslintrc.json to project
ng g @angular-eslint/schematics:add-config-to-project modern-angular-starter

# Add .eslintignore
echo "node_modules" >> .eslintignore
echo "dist" >> .eslintignore
echo "yarn.lock" >> .eslintignore
```

#### Update angular.json

Remove `architect.lint` then rename `architect.eslint` to `architect.lint`

```json
{
  "projects": {
    "modern-angular-starter": {
      "architect": {
        "lint": {
          "builder": "@angular-eslint/builder:lint",
          "options": {
            "lintFilePatterns": ["src/**/*.ts", "src/**/*.component.html"]
          }
        }
      }
    }
  }
}
```

#### Update package.json

Update `package.json`, add these 2 command into scripts

```json
{
  "scripts": {
    "eslint": "eslint --ext .ts,.component.html src/",
    "eslint:fix": "eslint --fix --ext .ts,.component.html src/"
  }
}
```

#### Install Airbnb ESLint config

```bash
yarn add -D \
  eslint-plugin-import \
  eslint-config-airbnb-typescript
```

Then update `.eslintrc.json` after `"plugin:@angular-eslint/recommended"` add `"airbnb-typescript/base"`

```json
{
  "files": ["*.ts"],
  "parserOptions": {
    "project": ["tsconfig.*?.json", "e2e/tsconfig.json"]
  },
  "extends": ["plugin:@angular-eslint/recommended", "airbnb-typescript/base"]
}
```

### 2. Install Prettier

```bash
yarn add -D \
  prettier \
  eslint-config-prettier \
  eslint-plugin-prettier
```

Create `.prettierrc.json` with rules

```json
{
  "singleQuote": true,
  "jsxBracketSameLine": true
}
```

Create `.prettierignore`

```ignore
node_modules
dist
yarn.lock
.log
```

Update `package.json`, add command into scripts

```json
{
  "scripts": {
    "prettier": "prettier --write ."
  }
}
```

Update `.eslintrc.json`, add `"prettier/@typescript-eslint"` and `"plugin:prettier/recommended"` at the bottom of extends

```jsonc
{
  "extends": [
    "plugin:@angular-eslint/recommended",
    "airbnb-typescript/base",
    // Prettier need to at the bottom of extends, it willprevent conflict rules with pitter formatter
    "prettier/@typescript-eslint",
    "plugin:prettier/recommended"
  ]
}
```

Config `.vscode/settings.json` for auto fix lint & format

```json
{
  "editor.formatOnSave": true,
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[jsonc]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[markdown]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "eslint.validate": ["javascript", "typescript", "html"],
  "eslint.options": {
    "extensions": [".js", ".ts", ".html"]
  }
}
```

<!-- TODO -->

### 3. Replace Karma and Jasmine with Jest

<!-- TODO -->

### 4. Replace Protractor with Cypress

<!-- TODO -->

## References

ESLint

- https://dev.to/dreiv/using-eslint-and-prettier-with-vscode-in-an-angular-project-42ib
- https://dev.to/bzvyagintsev/migrate-angular-app-to-eslint-with-prettier-airbnb-styleguide-husky-and-lint-staged-862
- https://eslint.org/docs/user-guide/command-line-interface
- https://github.com/angular-eslint/angular-eslint
- https://github.com/typescript-eslint/typescript-eslint
- https://github.com/benmosher/eslint-plugin-import
- https://github.com/iamturns/eslint-config-airbnb-typescript
