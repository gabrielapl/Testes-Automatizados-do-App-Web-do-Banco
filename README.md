# Testes Automatizados do App Web do Banco

## Objetivo

Este projeto tem como objetivo automatizar testes end-to-end da aplicação web do banco utilizando Cypress com JavaScript. A automação cobre cenários importantes de negócio, como login e transferência bancária, garantindo maior confiabilidade e agilidade na validação das regras da interface.

A ideia principal é simular a interação real do usuário com a aplicação, validar mensagens exibidas na tela e verificar que os fluxos principais funcionam corretamente.

---

## Componentes do projeto

### 1. Cypress
O projeto utiliza Cypress como ferramenta principal de automação de testes de interface.

### 2. Custom Commands
Os comandos customizados foram organizados em arquivos separados para facilitar reutilização e manutenção. Eles centralizam ações repetitivas da aplicação, como:

- login com credenciais válidas e inválidas
- seleção de opções em combobox
- validação de mensagens exibidas no toast
- execução de transferência bancária

Arquivos de comandos:

- `cypress/support/commands.js`
- `cypress/support/commands/common.js`
- `cypress/support/commands/login.js`
- `cypress/support/commands/transferencia.js`

### 3. Testes end-to-end
Os cenários automatizados ficam em:

- `cypress/e2e/login.cy.js`
- `cypress/e2e/transferencia.cy.js`

Esses testes cobrem:

- login com usuário válido
- login com credenciais inválidas
- transferência com dados válidos
- tentativa de transferência acima do limite sem autenticação

### 4. Fixtures
Os dados de teste são armazenados em:

- `cypress/fixtures/credenciais.json`

Esse arquivo organiza credenciais válidas e inválidas para que os testes possam consumir informações de forma organizada.

### 5. Relatórios
O projeto utiliza o plugin `cypress-mochawesome-reporter` para gerar relatórios em HTML após a execução dos testes.

Os relatórios ficam em:

- `cypress/reports/html`

### 6. Configuração do Cypress
A configuração do projeto está em:

- `cypress.config.js`

Ela define a URL base da aplicação e registra o plugin do relatórios.

---

## Pré-requisitos

Antes de executar os testes, é necessário que os seguintes projetos estejam em funcionamento:

1. API do banco: https://github.com/juliodelimas/banco-api
2. Aplicação web do banco: https://github.com/juliodelimas/banco-web

Esses serviços precisam estar rodando localmente para que o Cypress consiga acessar a aplicação e realizar os testes.

Também é necessário ter instalado:

- Node.js
- npm

---

## Instalação

1. Clone este repositório:

```bash
git clone <url-do-repositorio>
cd Testes-Automatizados-do-App-Web-do-Banco
```

2. Instale as dependências do projeto:

```bash
npm install
```

3. Inicie a API e a aplicação web do banco conforme as instruções dos repositórios mencionados acima.

4. Verifique se a aplicação está acessível na URL configurada no projeto:

```javascript
baseUrl: 'http://localhost:4000'
```

---

## Execução dos testes

### Executar em modo headless (linha de comando)

```bash
npm test
```

### Executar com navegador visível

```bash
npm run cy:headed
```

### Abrir a interface do Cypress

```bash
npm run cy:open
```

---

## Documentação dos testes

### Login
Arquivo: `cypress/e2e/login.cy.js`

Cenários:

- Login com dados válidos deve permitir entrada no sistema
- Login com dados inválidos deve apresentar mensagem de erro

Esses testes validam a experiência do usuário ao tentar acessar o sistema e confirmam que mensagens de erro e sucesso são exibidas corretamente.

### Transferência
Arquivo: `cypress/e2e/transferencia.cy.js`

Cenários:

- Deve transferir quando informo dados e valor válidos
- Deve apresentar erro quando tentar transferir mais que R$ 5.000,00 sem o token

Esses testes garantem que a regra de negócio da transferência foi implementada corretamente e que a aplicação responde ao usuário com a mensagem esperada.

---

## Documentação dos Custom Commands

### `verificarMensagemNoToast`
Valida uma mensagem exibida em um toast na interface.

```javascript
cy.verificarMensagemNoToast('Transferência realizada!')
```

### `selecionarOpcaoNaComboBox`
Seleciona uma opção em um campo do tipo combobox a partir do label do campo e do valor desejado.

```javascript
cy.selecionarOpcaoNaComboBox('conta-origem', 'Ana Pereira')
```

### `fazerLoginComCredenciaisValidas`
Preenche os campos de usuário e senha com dados válidos e realiza o login.

```javascript
cy.fazerLoginComCredenciaisValidas()
```

### `fazerLoginComCredenciaisInvalidas`
Preenche os campos com credenciais inválidas e tenta autenticar.

```javascript
cy.fazerLoginComCredenciaisInvalidas()
```

### `realizarTransferencia`
Executa o fluxo completo de transferência informando conta de origem, conta de destino e valor.

```javascript
cy.realizarTransferencia('Ana Pereira', 'Fernanda', '11')
```

---

## Estrutura do projeto

```text
.
├── cypress/
│   ├── e2e/
│   │   ├── login.cy.js
│   │   └── transferencia.cy.js
│   ├── fixtures/
│   │   └── credenciais.json
│   ├── reports/
│   │   └── html/
│   ├── screenshots/
│   ├── support/
│   │   ├── commands.js
│   │   └── commands/
│   │       ├── common.js
│   │       ├── login.js
│   │       └── transferencia.js
│   └── videos/
├── cypress.config.js
├── package.json
├── README.md
└── ...
```

---

## Observações finais

Este projeto foi estruturado para facilitar a manutenção dos testes e a reutilização de ações comuns da aplicação. O uso de Custom Commands reduz duplicação de código e deixa os cenários de teste mais limpos e legíveis.

Além disso, a geração de relatórios em HTML ajuda na análise dos resultados e facilita a revisão do status dos testes após cada execução.
