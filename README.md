# Guia para Iniciar um Projeto Node.js com TypeScript

Este guia irá mostrar como configurar e iniciar um projeto Node.js com TypeScript usando o Visual Studio Code (VS Code) em três ambientes diferentes: Linux, Windows e Codespace.

Obs: Caso fique com dúvidas, acesse o site [chatgpt](https://chatgpt.com/), mas não faça tudo dependendo dele.

## O que é cada coisa?

- **Servidor**: Um servidor é um programa que atende a pedidos de outros programas, chamados clientes. Em um site, por exemplo, o servidor envia as páginas para o navegador do usuário.
- **Node.js**: É um ambiente de execução JavaScript no lado do servidor. Permite rodar JavaScript fora do navegador.
- **TypeScript**: É uma linguagem de programação desenvolvida pela Microsoft que é um superconjunto de JavaScript, adicionando tipagem estática.
- **VS Code (Visual Studio Code)**: É um editor de código-fonte desenvolvido pela Microsoft. É leve e possui muitas extensões úteis.
- **Express**: É um framework para Node.js que facilita a criação de aplicações web e APIs.
- **GitHub**: É uma plataforma de hospedagem de código-fonte que usa Git para controle de versão.
- **Codespace**: É uma ferramenta oferecida pelo GitHub para desenvolver diretamente na nuvem, usando VS Code no navegador.

## Parte 1: Linux

### Pré-requisitos

1. **Node.js** e **npm** instalados no seu sistema.
2. **Visual Studio Code** (VS Code) instalado.

### Instalar VS Code no Linux
- **Linux**: Vá ao site do [Visual Studio Code](https://code.visualstudio.com/), baixe o instalador e siga as instruções de instalação. Para distribuições baseadas em Debian/Ubuntu, você pode usar o seguinte comando:
  ```sh
  sudo apt update
  sudo apt install code
  ```

### Instalar Node.js e npm no Linux
- **Linux**: Acesse o site do [Node.js](https://nodejs.org/), baixe a versão LTS e siga as instruções de instalação. Ou você pode usar o seguinte comando:
  ```sh
  sudo apt update
  sudo apt install nodejs npm
  ```

### Criar o Projeto no Linux

1. **Crie um diretório para o projeto e acesse-o pelo VS Code**
   ```sh
   mkdir meu-projeto
   cd meu-projeto
   code .
   ```

2. **Abra o terminal integrado no VS Code** (Ctrl + `)

### Inicializar o Projeto

1. **Inicialize o projeto com npm**
   ```sh
   npm init -y
   ```

2. **Instale as dependências necessárias**
   ```sh
   npm install express cors sqlite3 sqlite
   npm install --save-dev typescript nodemon ts-node @types/express @types/cors
   ```

### Inicialize o TypeScript
   ```sh
   npx tsc --init
   ```

### Crie a Estrutura de Diretórios e Arquivos
   ```sh
   mkdir src
   touch src/app.ts
   ```

### Configurar o TypeScript

1. **Abra o arquivo `tsconfig.json` e faça as seguintes alterações**
   ```json
   {
     "compilerOptions": {
       "target": "ES2017",
       "module": "commonjs",
       "outDir": "./dist",
       "rootDir": "./src",
       "strict": true,
       "esModuleInterop": true,
       "skipLibCheck": true,
       "forceConsistentCasingInFileNames": true
     }
   }
   ```

### Configurar o `package.json`

1. **Adicione o seguinte script ao seu `package.json`**
   ```json
   "scripts": {
     "dev": "npx nodemon src/app.ts"
   }
   ```

### Criar o Arquivo Inicial do Servidor

1. **No arquivo `src/app.ts`, adicione o seguinte código**
   ```typescript
   import express from 'express';
   import cors from 'cors';

   const port = 3333;
   const app = express();

   app.use(cors());
   app.use(express.json());

   app.get('/', (req, res) => {
     res.send('Hello World');
   });

   app.listen(port, () => {
     console.log(`Server running on port ${port}`);
   });
   ```

### Inicializar o Servidor

1. **No terminal integrado, rode o servidor**
   ```sh
   npm run dev
   ```

Se tudo ocorrer bem, você verá a mensagem `Server running on port 3333` no terminal.

### Testar o Servidor

1. **Abra o navegador e acesse [http://localhost:3333](http://localhost:3333)**
   - Você verá a mensagem `Hello World`.

---

## Parte 2: Windows

### Pré-requisitos

1. **Node.js** e **npm** instalados no seu sistema.
2. **Visual Studio Code** (VS Code) instalado.

### Instalar VS Code no Windows
- **Windows**: Vá ao site do [Visual Studio Code](https://code.visualstudio.com/), baixe o instalador e siga as instruções de instalação.

### Instalar Node.js e npm no Windows
- **Windows**: Acesse o site do [Node.js](https://nodejs.org/), baixe a versão LTS e siga as instruções de instalação.

### Criar o Projeto no Windows

1. **Crie um diretório para o projeto e acesse-o pelo VS Code**
   - Abra o prompt de comando ou PowerShell e execute:
   ```sh
   mkdir meu-projeto
   cd meu-projeto
   code .
   ```

2. **Abra o terminal integrado no VS Code** (Ctrl + `)

### Inicializar o Projeto

1. **Inicialize o projeto com npm**
   ```sh
   npm init -y
   ```

2. **Instale as dependências necessárias**
   ```sh
   npm install express cors sqlite3 sqlite
   npm install --save-dev typescript nodemon ts-node @types/express @types/cors
   ```

### Inicialize o TypeScript
   ```sh
   npx tsc --init
   ```

### Crie a Estrutura de Diretórios e Arquivos

   - Use o comando `type` no PowerShell para criar o arquivo:
   ```sh
   mkdir src
   type nul > src/app.ts
   ```

### Configurar o TypeScript

1. **Abra o arquivo `tsconfig.json` e faça as seguintes alterações**
   ```json
   {
     "compilerOptions": {
       "target": "ES2017",
       "module": "commonjs",
       "outDir": "./dist",
       "rootDir": "./src",
       "strict": true,
       "esModuleInterop": true,
       "skipLibCheck": true,
       "forceConsistentCasingInFileNames": true
     }
   }
   ```

### Configurar o `package.json`

1. **Adicione o seguinte script ao seu `package.json`**
   ```json
   "scripts": {
     "dev": "npx nodemon src/app.ts"
   }
   ```

### Criar o Arquivo Inicial do Servidor

1. **No arquivo `src/app.ts`, adicione o seguinte código**
   ```typescript
   import express from 'express';
   import cors from 'cors';

   const port = 3333;
   const app = express();

   app.use(cors());
   app.use(express.json());

   app.get('/', (req, res) => {
     res.send('Hello World');
   });

   app.listen(port, () => {
     console.log(`Server running on port ${port}`);
   });
   ```

### Inicializar o Servidor

1. **No terminal integrado, rode o servidor**
   ```sh
   npm run dev
   ```

Se tudo ocorrer bem, você verá a mensagem `Server running on port 3333` no terminal.

### Testar o Servidor

1. **Abra o navegador e acesse [http://localhost:3333](http://localhost:3333)**
   - Você verá a mensagem `Hello World`.

---

## Parte 3: Codespace

### Criar uma Conta no Codespace

1. **Criar uma Conta**
   - Acesse o [GitHub Codespaces](https://github.com/features/codespaces) e crie uma conta.
   - Após criar a conta, você pode criar um novo Codespace a partir do seu repositório ou diretamente do GitHub.

### Criar o Projeto no Codespace

1. **Crie um Novo Codespace**
   - Vá para o repositório no GitHub onde deseja criar o Codespace.
   - Clique no botão `Code` e selecione `Open with Codespaces` e, em seguida, `New codespace`.

2. **Abra o terminal integrado no Codespace** (Ctrl + `)

### Inicializar o Projeto

1. **Inicialize o projeto com npm**
   ```sh
   npm init -y
   ```

2. **Instale as dependências necessárias**
   ```sh
   npm install express cors sqlite3 sqlite
   npm install --save-dev typescript nodemon ts-node @types/express @types/cors
   ```

### Inicialize o TypeScript
   ```sh
   npx tsc --init
   ```

### Crie a Estrutura de Diretórios e Arquivos
   ```sh
   mkdir src
   touch src/app.ts
   ```



### Configurar o TypeScript

1. **Abra o arquivo `tsconfig.json` e faça as seguintes alterações**
   ```json
   {
     "compilerOptions": {
       "target": "ES2017",
       "module": "commonjs",
       "outDir": "./dist",
       "rootDir": "./src",
       "strict": true,
       "esModuleInterop": true,
       "skipLibCheck": true,
       "forceConsistentCasingInFileNames": true
     }
   }
   ```

### Configurar o `package.json`

1. **Adicione o seguinte script ao seu `package.json`**
   ```json
   "scripts": {
     "dev": "npx nodemon src/app.ts"
   }
   ```

### Criar o Arquivo Inicial do Servidor

1. **No arquivo `src/app.ts`, adicione o seguinte código**
   ```typescript
   import express from 'express';
   import cors from 'cors';

   const port = 3333;
   const app = express();

   app.use(cors());
   app.use(express.json());

   app.get('/', (req, res) => {
     res.send('Hello World');
   });

   app.listen(port, () => {
     console.log(`Server running on port ${port}`);
   });
   ```

### Inicializar o Servidor

1. **No terminal integrado, rode o servidor**
   ```sh
   npm run dev
   ```

Se tudo ocorrer bem, você verá a mensagem `Server running on port 3333` no terminal.

### Testar o Servidor

1. **Abra o navegador e acesse [http://localhost:3333](http://localhost:3333)**
   - Você verá a mensagem `Hello World`.

