Modern Angular Starter
---

This project includes:

- ESLint
- Prettier
- Jest
- Cypress

[toc]

## How to

Clone this project or do the belows step by yourself

```bash
ng new modern-angular-starter --skipInstall --strict --style=scss
cd modern-angular-starter
yarn install
```

### Replace TSLint and Codelyzer with ESLint and @angular-eslint

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
            "lintFilePatterns": [
              "src/**/*.ts",
              "src/**/*.component.html"
            ]
          }
        }
      }
    }
  }
}
```

#### Update package.json

Add these 2 command into package.json

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
    "project": [
      "tsconfig.*?.json",
      "e2e/tsconfig.json"
    ]
  },
  "extends": ["plugin:@angular-eslint/recommended", "airbnb-typescript/base"]
}
```

### Introduce Prettier

<!-- TODO -->

### Replace Karma and Jasmine with Jest

<!-- TODO -->

### Replace Protractor with Cypress

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

