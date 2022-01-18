![CAPA LINKEDIN_PERFIL PESSOAL03](https://user-images.githubusercontent.com/52717632/123512102-9546b200-d653-11eb-8b6c-f6c1dd19143e.png)
# Projeto Stranger Things - Back-End :zombie:

Esta é a primeira parte do projeto Stranger Things, para ver o Front-End, basta acessar [aqui](https://github.com/AndersonSilva94/project-stranger-things-frontend).

## Objetivos a serem alcançados no decorrer da construção do projeto:

Nesse projeto, você será capaz de:
  - Publicar aplicações através do `Heroku`;
  - Visualizar logs das suas aplicações publicadas;
  - Monitorar suas aplicações publicadas;
  - Utilizar variáveis de ambiente dentro do `Heroku`;
  - Instalar, utilizar e aproveitar os principais recursos do `PM2`;
  - Fazer deploy no `Heroku` aproveitando recursos de um process manager.

---

## Instruções para clonar o projeto

1. Clone o repositório
  ```bash
  $ git clone https://github.com/AndersonSilva94/project-stranger-things-backend.git`.
  ```

2. Entre na pasta do repositório que você acabou de clonar:
    ```bash
    $ cd project-stranger-things-backend
    ```

3. Instale as dependências
  ```bash
  $ npm install
  ```

4. Rode a aplicação
  ```bash
  $ npm start
  ```

---

## O que deverá ser desenvolvido

Você vai adaptar e configurar os projetos descritos nesse README para que seja feito o deploy deles. Você vai colocar os projetos frontend e backend no ar com o `Heroku`, utilizando o `PM2` para gerenciar e monitorar os processos. Além disso, você vai alterar alguns comportamentos aplicando os conceitos vistos no conteúdo.

---

## Testes

### Backend

Todos os requisitos do projeto serão testados **automaticamente** por meio do `Jest`. Basta executar o comando abaixo:

```bash
npm test
```
---

## Deploy - Stranger Things

### Backend

O Backend possui a seguinte estrutura:

```
├── README.md
├── index.js
├── data
│  ├── dataset
│  │  └── stranger-things-characters.json
│  └── repository
│     └── StrangerThings.js
├── services
│  └── StrangerThings.js
├── package-lock.json
└── package.json
```

---

#### API

A API consiste em um serviço simples com um endpoint `/` que retorna uma listagem com os personagens da série **Stranger Things**.

---

#### Resposta

A lista de personagem possui os seguintes campos:

- **name**: Nome do personagem;

- **status**: se o personagem está vivo ou não na série. Os valores possíveis são `alive`, `deceased` ou `unknown`;

- **origin**: o local de origem do personagem.

A resposta é em formato `JSON`, e o retorno é sempre um array de objetos. Abaixo, um exemplo:

```JSON
[
  {
    "name": "Will",
    "status": "Alive",
    "origin": "Byers Family"
  }
]
```

---

#### Filtros

Todos os campos da estrutura de retorno da resposta podem ser utilizados como filtros. Para isso, basta passar na `query string` o filtro desejado. No exemplo abaixo, estamos filtrando pelo _nome_ do personagem:

> localhost:3000?name=el

Os filtros são feitos utilizando uma `regex`, buscando pelo texto passado na `query string` em qualquer parte do campo, sem diferenciar maiúsculas de minúsculas.

Nesse caso o retorno seria:

```JSON
[
  {
    "name":"Russell",
    "status":"Alive",
    "origin":"Hawkings Middle School"
  },
  {
    "name":"Eleven",
    "status":"Alive",
    "origin":"Hopper Family"
  }
]
```

---

#### Modo `upside down` - Backend

Na API, no arquivo `index.js`, há a seguinte variável de controle:

```javascript
const hereIsTheUpsideDown = true;
```

Caso ela seja `true`, a API ativará o modo "Mundo Invertido", conforme a série, e começará a responder desta forma:

```JSON
[
  {
    "name":"llǝssnᴚ",
    "origin":"looɥɔS ǝlppᴉW sƃuᴉʞʍɐH",
    "status":"ǝʌᴉl∀"
  },
  {
    "name":"uǝʌǝlƎ",
    "origin":"ʎlᴉɯɐℲ ɹǝddoH",
    "status":"ǝʌᴉl∀"
  }
]
```

---

#### Monitoramento

Para monitorar sua aplicaçao no heroku usando o dashboard do PM2, siga os passos abaixo:

1.Crie um novo `bucket` no dashboard de monitoramento web do `PM2`. Em seguida, pelo dashboard, adicione as chaves criadas aos `apps` do Heroku criados anteriomente.

2.Deverão ser adicionadas três variáveis para cada app:

   - O nome do server. No caso, utilizaremos um nome diferente para cada um dos apps;

   - Chave pública;

   - Chave privada.

3.Verifique no Dashboard se os processos estão sendo exibidos e monitorados.

---

## Desenvolvimento

O código não está utilizando variáveis de ambiente. Você vai configurá-lo para utilizá-las, tornando parametrizáveis a porta e o _modo upside down_.

Em seguida, você deverá adicionar o modulo `PM2` ao projeto utilizando o arquivo `ecosystem`, fazendos as adaptações necessárias no `package.json`.

Você vai realizar o deploy do projeto (frontend e backend) no _Heroku_. Para isso, você deverá prepará-los, adicionando os respectivos `Procfiles`. Eles deverão apontar para os scripts adicionados ao `package.json` que utilizam o `PM2`. Por último, você deverá realizar o deploy do projeto, conforme requisitos, no _Heroku_. Os comandos utilizados deverão ser adicionados no README.md de cada projeto. Para mais informações sobre - [Procfiles](https://app.betrybe.com/course/back-end/deployment/infraestrutura-deploy-com-heroku/30597149-145b-49a1-924c-bd8050a8f249/conteudo/dcb89fc5-1093-458d-9b2f-fbac0b18f9bc/introducao-ao-heroku/8e3bf957-decc-40b9-a854-eb406ede0ca9?use_case=side_bar) e [ecosystem](https://app.betrybe.com/course/back-end/deployment/deploy-gerenciadores-de-processos/915a6dce-162b-4015-b499-31ecae9e9411/conteudo/a3b991be-5a2d-4a82-9a38-d96eab5534b5/ecosystem-file/90d1dda4-555a-4cc3-9757-22d72836e230?use_case=side_bar) visite o Course.

Todos esses passos estão detalhados nos requisitos abaixos.

---

# Requisitos do projeto

⚠️ Lembre-se que o seu projeto só será avaliado se estiver passando por **todos os _checks_** do **Linter**. Utilize o comando `npm run lint` no seu terminal para verificar os _checks_ do **Linter** 😉 ⚠️

Os requisitos estão agrupados por `frontend` e `backend`. Realize as alterações nos respectivos diretórios [disponbilizados para você](#Deploy---Stranger-Things).

### Backend

#### 1 - Verifica as variáveis de ambiente

Altere o backend para utilizar variáveis de ambiente para contrololar os seguintes comportamentos:

   1. A porta que a API escutará, essa variável deve ter, nescessariamente, o nome PORT e o seu valor deve ser 3000.

   2. O modo "upsideDown". Essa variável espera um valor boleano e deverá se chamar UPSIDEDOWN_MODE. Lembre-se que as variáveis de ambiente são `strings`.

   O que será testado:
   - Se existe a variável de ambiente PORT.
   - Se a variável de ambiente UPSIDEDOWN_MODE existe e se ela é um boleano.

**Importante**: Para esse projeto, as variáveis de ambiente devem ser definidas em um arquivo .env e o arquivo deve ser enviando no seu PR(Pull Request). ISSO NÃO É UMA PRÁTICA DE MERCADO, o arquivo .env deve ser sempre incluido do .gitignore pois contém informações sensíveis, aqui será enviado apenas por motivo de avaliação.

#### 2 - Verifica se o módulo pm2 foi instalado no projeto

Adicione o módulo PM2 à API.

O que será testado:
 - Se o módulo `pm2` esta instalado nas dependências.

#### 3 - Verifica a configuração do ecosystem.config.yml

Adicione o [arquivo](https://app.betrybe.com/course/back-end/deployment/deploy-gerenciadores-de-processos/915a6dce-162b-4015-b499-31ecae9e9411/conteudo/a3b991be-5a2d-4a82-9a38-d96eab5534b5/ecosystem-file/90d1dda4-555a-4cc3-9757-22d72836e230?use_case=side_bar) `ecosystem.config.yml`. O arquivo deverá realizar as seguintes configurações:

  1. Ativar o Modo Cluster;

  2. Subir duas instâncias do processo;

  3. Não assistir à alterações no diretório (modo`watch` desativado);

  4. Reiniciar o processo caso ele consuma mais de 200MB de memória.

  **importante**: O arquivo `ecosystem` deve ter a extensão yml e não yaml.

  O que será testado:
  - Se o ecosystem tem a propriedade name
  - Se o script a ser executado é o index.js.
  - Se o modo de execução está configurado para cluster.
  - Se o numero de instancias está definido como 2.
  - Se o modo watch esta configurado para estar desativado.
  - Se a reiniciação de memória máxima esta configurada como 200M. [Documentação do pm2](https://pm2.keymetrics.io/docs/usage/memory-limit)

#### 4 - Verifica se os scripts do package.json estão corretos

Adicione/altere dois `scripts` no `package.json`:

  1. `start`: Deverá iniciar o server utilizando o módulo do `PM2` e apontando para o arquivo `ecosystem` criado;

  2. `start:dev`: Deverá iniciar o server utilizando o módulo do `PM2`, **sem** apontar para o arquivo `ecosystem` e com o parâmetro para "observar alterações no diretório" **ativado**.

Execute ambos em sua máquina para validar se o comportamento é o esperado.

O que será testado:
  - Se o comando `start` inicia o server com pm2 e se usa o ecosystem.
  - Se o comando `start:dev` inicia o server com pm2, se não usa o ecosystem e abre em watchMode.

#### 5 - Verifica a configuração do arquivo Procfile

Defina um [arquivo](https://app.betrybe.com/course/back-end/deployment/infraestrutura-deploy-com-heroku/30597149-145b-49a1-924c-bd8050a8f249/conteudo/dcb89fc5-1093-458d-9b2f-fbac0b18f9bc/introducao-ao-heroku/8e3bf957-decc-40b9-a854-eb406ede0ca9?use_case=side_bar) `Procfile`, utilizando a mesma configuração do script `start` do `package.json`: iniciar o server utilizando o módulo do `PM2`, apontando para o arquivo `ecosystem` criado anteriormente.

Lembre-se: como nossos serviços receberão acessos HTTP externos, precisamos definir os `Dynos` como sendo do tipo `web`.

O que será testado:
- Se o dyno é do tipo web.
- Se o script inicia o server com pm2 e se usa o ecosystem.

#### 6 - Verifica o Deploy no Heroku

**IMPORTANTE**: Uma variável de ambiente com o nome GITHUB_USER deverá ser criada com o seu usuário do github.

**IMPORTANTE**: O heroku limita o tamanho do nome de uma aplicação para ter no máximo **30 caracteres**, se o seu usuário do GitHub possuir mais que 27 caracteres você não conseguirá criar uma aplicação com o nome no padrão solicitado pelo requisito. Caso esteja nessa condição, avise nosso time de instrunção que iremos ajudá-lo.

1. Crie dois `apps` do Heroku a partir do mesmo código fonte (código da API). O nome do seu app no heroku deverá conter seu nome de usuário no github seguido de "-bk" ou "-bd". Por exemplo, se seu nome de usuário no github for "student" seus app deverão ter o nome "sudent-bk" e "student-bd" e as urls abaixo:

   - https://student-bk.herokuapp.com/ -para o app hawkins

   - https://student-bd.herokuapp.com/ -para o app upside-down

2. Configure a variável de ambiente criada para controlar o modo `upsideDown`. Cada um dos `apps` deverá ter valores distintos, da seguinte maneira:

   - O app `hawkins` deverá ter o valor `false`;

   - O app `upside-down` deverá ter o valor `true`.

3. Utilizando o `git`, faça o deploy de ambos os `apps` no Heroku.

Acesse os URLs geradas e valide se ambas as API's estão no ar e funcionando como esperado.
**Importante**: As URLS deverão ser geradas pelo heroku e não devem ser modificadas.

O que será testado:
  - Se ao fazer uma requisição do tipo GET para o endpoint da api Hawkins serão retornadas as informações corretas.
  - Se ao fazer uma requisição do tipo GET para o endpoint da api upsideDown serão retornadas as informações corretas.

---
:keyboard: com :purple_heart: por [Anderson Silva (Andy)](https://www.linkedin.com/in/andssilva/) 😊

