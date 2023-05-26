# Quick Setup

## Angular
```powershell
npm install -g @angular/cli
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

## Library Monorepo
```powershell
ng new library-workspace --no-create-application
cd .\library-workspace\
```

## ESLint
```powershell
ng add @angular-eslint/schematics
ng config cli.schematicCollections '["@angular-eslint/schematics"]'
```

## Conventional Commit Lint
```powershell
npm install -g @commitlint/cli @commitlint/config-conventional
ConvertFrom-Json @"
{ 
    "extends": ["@commitlint/config-conventional"]
}
"@ | ConvertTo-Json | Set-Content ".commitlintrc.json"
npm i -D husky
npx husky install
npx husky add .husky/commit-msg 'npx commitlint --edit $1'
```

## Prettier

### Install
```powershell
npm install prettier --save-dev
ConvertFrom-Json @"
{                      
  "tabWidth": 2,
  "useTabs": false,
  "singleQuote": true,
  "semi": true,
  "bracketSpacing": true,
  "arrowParens": "avoid",
  "trailingComma": "es5",
  "bracketSameLine": true,
  "printWidth": 80
}
"@ | ConvertTo-Json | Set-Content ".prettierrc.json"
Get-Content -Path .gitignore | Set-Content ".prettierignore"
```

### Configure with ESLint
```powershell
npm install prettier-eslint eslint-config-prettier eslint-plugin-prettier --save-dev

```

## Stylelint
```powershell
npm install --save-dev stylelint stylelint-config-standard-scss
ConvertFrom-Json @"
{
  "extends": [
    "stylelint-prettier/recommended",
    "stylelint-config-standard-scss"
  ]
}
"@ | ConvertTo-Json | Set-Content ".stylelintrc.json"
```

## Jest
```powershell
npm install jest --save-dev
```

Then update the `angular.json` file
```json
// angular.json
{
  "projects": {
    "my-app": { // <- The name of your app
      "architect": {
        "test": {
          "builder": "@angular-devkit/build-angular:jest",
          "options": {
            "tsConfig": "tsconfig.spec.json",
            "polyfills": ["zone.js", "zone.js/testing"]
          }
        }
      }
    }
  }
}
```