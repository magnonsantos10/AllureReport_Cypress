# AllureReport_Cypress
Configuração do Allure Report com Cypress

## Instalação

* instalando mocha-allure-reporter

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
Após seguir os passos acima, executar o seguinte comando no terminal:

```
npm test
```

O comando acima fará com que os testes dentro de integration com a estenção `.spec.js` sejam executados, após a execução as pastas do allure report + allure results serão apresentadas no Visual Studio ou na IDE que você estiver utilizando no momento.

![image](https://user-images.githubusercontent.com/91263334/146851249-fd16584d-612d-4c75-8bfc-b6569b5ce6ac.png)

Feito isso podemos executar o seguinte comando abaixo: 

```
allure serve
```

Com isso o servidor do allure será iniciado e podemos acompanhar o allure-report através do navegador padrão.

![image](https://user-images.githubusercontent.com/91263334/146851504-5e56632a-bf83-4829-b195-ecf41c2f88ae.png)

Acessando `Suites` podemos ver de modo detalhado oque foi executado durante os testes, inclusive um vídeo de verificação com o passo a passo da execução.

![image](https://user-images.githubusercontent.com/91263334/146851728-07059434-316e-4a5b-8269-338e60db11b3.png)

Fim!!!

