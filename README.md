# Tutorial: Iniciando um Projeto Node.js com TypeScript

## Introdução

Neste tutorial, você aprenderá a configurar um servidor básico usando Node.js e TypeScript e a configurar um banco de dados SQLite. Vamos fazer isso passo a passo para garantir que tudo esteja claro.

### O que você vai precisar

1. **Node.js**: [Download do Node.js](https://nodejs.org/)
2. **Visual Studio Code (VSCode)**: [Download do VSCode](https://code.visualstudio.com/)

### Instalação do Node.js

1. **Baixe o Node.js**:
   - Acesse o site [Node.js](https://nodejs.org/).
   - Clique no botão de download recomendado para a versão LTS (Long Term Support).

2. **Instale o Node.js**:
   - Execute o instalador baixado.
   - Siga as instruções, aceitando os termos e mantendo as configurações padrão.
   - Após a instalação, abra o terminal (Prompt de Comando no Windows ou Terminal no macOS/Linux) e digite `node -v` para verificar a instalação. Você deve ver a versão do Node.js instalada.

### Instalação do Visual Studio Code (VSCode)

1. **Baixe o VSCode**:
   - Acesse [Visual Studio Code](https://code.visualstudio.com/).
   - Clique no botão de download para o seu sistema operacional.

2. **Instale o VSCode**:
   - Execute o instalador baixado.
   - Siga as instruções, aceitando os termos e mantendo as configurações padrão.

### Instalação da Extensão Rest Client no VSCode

1. **Abra o VSCode**:
   - Clique no ícone do VSCode para abri-lo.

2. **Acesse a aba de Extensões**:
   - No menu lateral esquerdo, clique no ícone de extensões (parece uma caixa aberta). 
   - Alternativamente, pressione `Ctrl+Shift+X` no teclado.

3. **Pesquise e instale a extensão Rest Client**:
   - Na barra de pesquisa, digite `Rest Client`.
   - Encontre a extensão `Rest Client` desenvolvida por `Huachao Mao` e clique no botão `Install`.

---

## Passo 1: Configurando o Projeto

### 1. Crie uma Pasta para o Projeto

1. **Abra o VSCode**.
2. **Crie ou abra uma pasta**:
   - No menu superior, clique em **File > Open Folder...**.
   - Selecione ou crie uma nova pasta para o seu projeto e clique em **Select Folder**.

### 2. Abra o Terminal no VSCode

1. **No VSCode**, vá até **Terminal > New Terminal** no menu superior.
2. **O terminal aparecerá na parte inferior da tela**. Este é o lugar onde você digitará comandos.

### 3. Inicialize um Projeto Node.js

1. **No terminal**, digite:
   ```bash
   npm init -y
   ```
   - Este comando cria um arquivo `package.json` com configurações padrão. Esse arquivo é essencial para gerenciar as dependências e scripts do seu projeto.

### 4. Instale as Dependências Necessárias

1. **No terminal**, execute:
   ```bash
   npm install express cors sqlite3
   npm install --save-dev typescript nodemon ts-node @types/express @types/cors @types/node
   ```
   - `express`, `cors`, e `sqlite3` são pacotes principais para o servidor e o banco de dados.
   - `typescript`, `nodemon`, `ts-node` são ferramentas para desenvolver com TypeScript.
   - `@types/express`, `@types/cors`, e `@types/node` fornecem tipos TypeScript para essas bibliotecas.

### 5. Configure o TypeScript

1. **Inicialize o TypeScript**:
   ```bash
   npx tsc --init
   ```
   - Isso cria um arquivo `tsconfig.json` com a configuração padrão para o TypeScript.

### 6. Configure o `tsconfig.json`

1. **Abra o arquivo `tsconfig.json`**:
   - No painel esquerdo do VSCode, clique em **Explorer**.
   - Encontre e abra o arquivo `tsconfig.json`.

2. **Atualize as configurações**:
   - Modifique o arquivo para se parecer com o seguinte:
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
   - `outDir` define onde os arquivos JavaScript serão salvos após a compilação.
   - `rootDir` define a pasta onde os arquivos TypeScript estão localizados.

### 7. Crie a Estrutura de Diretórios e Arquivos

1. **No terminal**, execute:
   ```bash
   mkdir src
   touch src/app.ts
   ```
   - `mkdir src` cria a pasta `src`.
   - `touch src/app.ts` cria o arquivo `app.ts` dentro da pasta `src`.

---

## Passo 2: Configurando o Servidor

### 1. Configure o `package.json`

1. **Abra o arquivo `package.json`**:
   - No painel esquerdo do VSCode, clique em **Explorer**.
   - Encontre e abra o arquivo `package.json`.

2. **Adicione o seguinte script**:
   ```json
   "scripts": {
     "dev": "npx nodemon src/app.ts --exec ts-node"
   }
   ```
   - Este script permite iniciar o servidor em modo de desenvolvimento, usando `nodemon` para reiniciar automaticamente quando houver alterações.

### 2. Crie o Arquivo Inicial do Servidor

1. **Abra o arquivo `src/app.ts`**:
   - No painel esquerdo do VSCode, clique em **Explorer**.
   - Encontre e abra o arquivo `src/app.ts`.

2. **Adicione o seguinte código**:
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

   - `import express from 'express';` e `import cors from 'cors';` importam os pacotes necessários.
   - `const app = express();` cria uma instância do servidor Express.
   - `app.use(cors());` e `app.use(express.json());` configuram o middleware para CORS e JSON.
   - `app.get('/', (req, res) => { res.send('Hello World'); });` define uma rota que responde com "Hello World".
   - `app.listen(port, () => { console.log(`Server running on port ${port}`); });` inicia o servidor na porta 3333 e exibe uma mensagem no terminal.

### 3. Inicie o Servidor

1. **No terminal**, execute:
   ```bash
   npm run dev
   ```
   - O comando inicia o servidor em modo de desenvolvimento.

2. **Verifique se o servidor está funcionando**:
   - Abra o navegador e acesse `http://localhost:3333`. Você deve ver a mensagem `Hello World`.

---

## Passo 3: Configurando o Banco de Dados

### 1. Crie o Arquivo de Configuração do Banco de Dados

1. **No terminal**, execute:
   ```bash
   touch src/database.ts
   ```
   - Cria um arquivo `database.ts` para gerenciar a conexão com o banco de dados.

2. **Abra o arquivo `src/database.ts`**:
   - No painel esquerdo do VSCode, clique em **Explorer**.
   - Encontre e abra o arquivo `src/database.ts`.

3. **Adicione o seguinte código**:
   ```typescript
   import { open, Database } from 'sqlite';
   import sqlite3 from 'sqlite3';

   let instance: Database | null = null;

   export async function connect() {
     if (instance) return instance;

     const db = await open({
       filename: './src/database.sqlite',
       driver: sqlite3.Database
     });

     await db.exec(`
       CREATE TABLE IF NOT EXISTS users (
         id INTEGER PRIMARY KEY AUTOINCREMENT,
         name TEXT,
         email TEXT
       )
     `);

     instance = db;
     return db;
   }
   ```

   - `import { open, Database } from 'sqlite';` e `import sqlite3 from 'sqlite3';` importam as bibliotecas necessárias para trabalhar com SQLite.
   - `connect` é uma função que estabelece a conexão com o banco de dados e cria a tabela `users` se ela não existir.

### 2. Adicione a Rota para Inserir Usuários

1. **Abra o arquivo `src/app.ts`**:
   - No painel esquerdo do VSCode, clique em **Explorer**.
   - Encontre e abra o arquivo

 `src/app.ts`.

2. **Adicione a seguinte rota**:
   ```typescript
   import { connect } from './database';

   app.post('/users', async (req, res) => {
     const db = await connect();
     const { name, email } = req.body;

     const result = await db.run('INSERT INTO users (name, email) VALUES (?, ?)', [name, email]);
     const user = await db.get('SELECT * FROM users WHERE id = ?', [result.lastID]);

     res.json(user);
   });
   ```

   - `app.post('/users', async (req, res) => { ... });` define uma rota que insere um novo usuário no banco de dados.
   - `const { name, email } = req.body;` extrai os dados da requisição.
   - `const result = await db.run('INSERT INTO users (name, email) VALUES (?, ?)', [name, email]);` insere o usuário na tabela.
   - `const user = await db.get('SELECT * FROM users WHERE id = ?', [result.lastID]);` recupera o usuário inserido.
   - `res.json(user);` envia a resposta com os dados do usuário.

### 3. Teste a Inserção de Dados

1. **Crie um arquivo `requests.http`**:
   - No painel esquerdo do VSCode, clique em **Explorer**.
   - Clique com o botão direito na raiz do projeto e selecione **New File**.
   - Nomeie o arquivo como `requests.http`.

2. **Adicione o seguinte conteúdo ao arquivo**:
   ```
   POST http://localhost:3333/users
   Content-Type: application/json

   {
     "name": "John Doe",
     "email": "johndoe@mail.com"
   }
   ```

3. **Envie a requisição**:
   - Abra o arquivo `requests.http` e clique no botão "Send Request" acima da linha `POST http://localhost:3333/users`.

4. **Verifique a resposta**:
   - Se tudo estiver correto, você verá a resposta com o usuário inserido:
     ```json
     {
       "id": 1,
       "name": "John Doe",
       "email": "johndoe@mail.com"
     }
     ```

---

## Passo 4: Adicionando Rotas CRUD

### 1. Liste Todos os Usuários

1. **Abra o arquivo `src/app.ts`**:
   - No painel esquerdo do VSCode, clique em **Explorer**.
   - Encontre e abra o arquivo `src/app.ts`.

2. **Adicione a rota para listar todos os usuários**:
   ```typescript
   app.get('/users', async (req, res) => {
     const db = await connect();
     const users = await db.all('SELECT * FROM users');

     res.json(users);
   });
   ```

   - A rota `/users` permite listar todos os usuários no banco de dados.
   - `const users = await db.all('SELECT * FROM users');` recupera todos os usuários.
   - `res.json(users);` envia a resposta com a lista de usuários.

### 2. Teste a Rota para Listar Todos os Usuários

1. **Adicione a seguinte requisição ao arquivo `requests.http`**:
   ```
   GET http://localhost:3333/users
   ```

2. **Envie a requisição**:
   - Abra o arquivo `requests.http` e clique no botão "Send Request" acima da linha `GET http://localhost:3333/users`.

3. **Verifique a resposta**:
   - Se tudo estiver correto, você verá a resposta com a lista de usuários inseridos.

---
