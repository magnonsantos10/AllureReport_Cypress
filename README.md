# AllureReport_Cypress
Configuração do Allure Report com Cypress

## Instalação

* instalando mocha-aalure-reporter

```
npm i --save-dev mocha-allure-reporter
```

* Instalando allure-commandline

```
npm install -g allure-commandline --save-dev
```

* instalando @shelex plugin

```
npm i --save-dev cypress @shelex/cypress-allure-plugin 
```

## Configuração de Plugin

* Configurar em cypress/plugin/index.js

```
/// <reference types="cypress" />
/// <reference types="@shelex/cypress-allure-plugin" />

const allureWriter = require("@shelex/cypress-allure-plugin/writer")

module.exports = (on, config) => {
  allureWriter(on, config);
  return config;
}
```

## Configuração de import

* Configurar em cypress/support/index.js

```
import '@shelex/cypress-allure-plugin'
```
## Script

* Configurar em package.json

```
"scripts": {
    "gui": "npx cypress open",
    "cy:run:folder": "cypress run --spec \"cypress/integration/**/*.spec.js\" --env allure=true -- reporter mocha-allure-reporter",
    "posttest": "allure generate allure results --clean -o allure-report || true",
    "test": "npm run cy:run:folder"
  },
```

## Cypress.json

* Configurar em cypress.json

```
{
    "env": { 
        "allureResultsPath": "allure-results"
      }
}
```
