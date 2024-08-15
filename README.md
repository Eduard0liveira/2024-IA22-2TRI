# Tutorial: Iniciando um Projeto Node.js com TypeScript

## Introdução

Neste tutorial, você aprenderá a configurar um servidor básico usando Node.js e TypeScript e a configurar um banco de dados SQLite. Vamos fazer isso passo a passo para garantir que tudo esteja claro, especialmente se você está começando agora.

### O que você vai precisar

1. **Node.js**: [Download do Node.js](https://nodejs.org/)
2. **Visual Studio Code (VSCode)**: [Download do VSCode](https://code.visualstudio.com/)

## Instalação do Node.js

### 1. Baixar o Node.js

1. Acesse o site [Node.js](https://nodejs.org/).
2. Clique no botão "LTS" (Long Term Support) para baixar a versão recomendada.

   ![Baixar Node.js](https://nodejs.org/static/images/logos/nodejs-new-pantone-black.png)

### 2. Instalar o Node.js

1. Execute o instalador baixado.
2. Siga as instruções do instalador, aceitando os termos e mantendo as configurações padrão.
3. Após a instalação, abra o terminal:
   - **No Windows**: Pressione `Win + R`, digite `cmd` e pressione `Enter`.
   - **No macOS**: Pressione `Cmd + Space`, digite `Terminal` e pressione `Enter`.
   - **No Linux**: Pressione `Ctrl + Alt + T`.

4. No terminal, digite `node -v` e pressione `Enter` para verificar a instalação. Você deve ver a versão do Node.js instalada.

## Instalação do Visual Studio Code (VSCode)

### 1. Baixar o VSCode

1. Acesse [Visual Studio Code](https://code.visualstudio.com/).
2. Clique no botão "Download" para o seu sistema operacional.

   ![Baixar VSCode](https://code.visualstudio.com/assets/images/brand/visual-studio-code-logo.png)

### 2. Instalar o VSCode

1. Execute o instalador baixado.
2. Siga as instruções do instalador, aceitando os termos e mantendo as configurações padrão.

## Abrindo o Terminal no VSCode

1. **Abra o VSCode**:
   - Clique no ícone do VSCode na sua área de trabalho ou menu de aplicativos.

   ![Abrir VSCode](https://code.visualstudio.com/assets/images/hero/home.png)

2. **Abra o Terminal no VSCode**:
   - No menu superior, clique em **Terminal**.
   - Selecione **New Terminal** no menu suspenso.

   ![Abrir Terminal no VSCode](https://code.visualstudio.com/assets/docs/editor/integrated-terminal/terminal-menu.png)

   - Alternativamente, você pode usar o atalho de teclado `Ctrl + Shift + ` (crase) no Windows e `Cmd + Shift + ` (crase) no macOS.

## Passo 1: Configurando o Projeto

### 1. Crie uma Pasta para o Projeto

1. **No VSCode**, clique em **File** no canto superior esquerdo.
2. Selecione **Open Folder...**.
3. Escolha ou crie uma nova pasta para o seu projeto e clique em **Select Folder**.

   ![Abrir Pasta no VSCode](https://code.visualstudio.com/assets/docs/editor/multiroot-workspaces/open-folder.png)

### 2. Inicialize um Projeto Node.js

1. **No terminal** (que aparece na parte inferior do VSCode), digite:
   ```bash
   npm init -y
   ```
   - Esse comando cria um arquivo `package.json` com configurações padrão.

### 3. Instale as Dependências Necessárias

1. **No terminal**, execute:
   ```bash
   npm install express cors sqlite3
   npm install --save-dev typescript nodemon ts-node @types/express @types/cors @types/node
   ```
   - `express`, `cors`, e `sqlite3` são pacotes principais para o servidor e o banco de dados.
   - `typescript`, `nodemon`, `ts-node` são ferramentas para desenvolver com TypeScript.
   - `@types/express`, `@types/cors`, e `@types/node` fornecem tipos TypeScript para essas bibliotecas.

### 4. Configure o TypeScript

1. **Inicialize o TypeScript**:
   ```bash
   npx tsc --init
   ```
   - Isso cria um arquivo `tsconfig.json` com a configuração padrão para o TypeScript.

### 5. Configure o `tsconfig.json`

1. **Abra o arquivo `tsconfig.json`**:
   - No painel esquerdo do VSCode, clique em **Explorer**.
   - Encontre e abra o arquivo `tsconfig.json`.

   ![Abrir Arquivo no VSCode](https://code.visualstudio.com/assets/docs/getstarted/keybindings/keyboard-shortcuts.png)

2. **Atualize as configurações**:
   - Modifique o arquivo para o seguinte conteúdo:
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

### 6. Crie a Estrutura de Diretórios e Arquivos

1. **No terminal**, execute:
   ```bash
   mkdir src
   touch src/app.ts
   ```
   - `mkdir src` cria a pasta `src`.
   - `touch src/app.ts` cria o arquivo `app.ts` dentro da pasta `src`.

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
   - Esse script permite iniciar o servidor em modo de desenvolvimento, usando `nodemon` para reiniciar automaticamente quando houver alterações.

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
   - Esse código configura um servidor básico com Express.

### 3. Inicie o Servidor

1. **No terminal**, execute:
   ```bash
   npm run dev
   ```
   - O comando inicia o servidor em modo de desenvolvimento.

2. **Verifique se o servidor está funcionando**:
   - Abra o navegador e acesse `http://localhost:3333`. Você deve ver a mensagem `Hello World`.

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
   - Esse código configura a conexão com o banco de dados SQLite e cria uma tabela `users` se ela não existir.

### 2. Adicione a Rota para Inserir Usuários

1. **Abra o arquivo `src/app.ts`**:
   - No painel esquerdo do VSCode, clique em **Explorer**.
   - Encontre e abra o arquivo `src/app.ts`.

2. **Adicione a seguinte rota**:
   ```typescript
   import { connect } from './database';

   app.post('/users', async (req, res) => {
     const db = await connect();
     const { name, email } = req.body;

     const result = await db.run('INSERT INTO users (name, email)


   - Se tudo estiver correto, você verá a resposta com a lista de usuários inseridos.
### 2. Adicione a Rota para Inserir Usuários (Continuação)

1. **Abra o arquivo `src/app.ts`**:
   - No painel esquerdo do VSCode, clique em **Explorer**.
   - Encontre e abra o arquivo `src/app.ts`.

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
   - `app.post('/users', async (req, res) => { ... });` define uma rota POST para adicionar um novo usuário.
   - `const { name, email } = req.body;` extrai os dados do corpo da requisição.
   - `const result = await db.run('INSERT INTO users (name, email) VALUES (?, ?)', [name, email]);` insere o novo usuário no banco de dados.
   - `const user = await db.get('SELECT * FROM users WHERE id = ?', [result.lastID]);` recupera o usuário recém-adicionado.
   - `res.json(user);` envia a resposta com os dados do usuário inserido.

### 3. Teste a Inserção de Dados

1. **Crie um arquivo para testar as requisições**:
   - No painel esquerdo do VSCode, clique em **Explorer**.
   - Clique com o botão direito na raiz do projeto e selecione **New File**.
   - Nomeie o arquivo como `requests.http`.

   ![Criar Novo Arquivo no VSCode](https://code.visualstudio.com/assets/docs/getstarted/keybindings/keyboard-shortcuts.png)

2. **Adicione o seguinte conteúdo ao arquivo `requests.http`**:
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

   ![Enviar Requisição no VSCode](https://code.visualstudio.com/assets/docs/editor/rest-client/rest-client-send-request.png)

4. **Verifique a resposta**:
   - Se tudo estiver correto, você verá a resposta com os dados do usuário inserido, como no exemplo abaixo:
     ```json
     {
       "id": 1,
       "name": "John Doe",
       "email": "johndoe@mail.com"
     }
     ```

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
   - `app.get('/users', async (req, res) => { ... });` define uma rota GET para listar todos os usuários.
   - `const users = await db.all('SELECT * FROM users');` recupera todos os usuários do banco de dados.
   - `res.json(users);` envia a resposta com a lista de usuários.

### 2. Teste a Rota para Listar Todos os Usuários

1. **Adicione a seguinte requisição ao arquivo `requests.http`**:
   ```
   GET http://localhost:3333/users
   ```

2. **Envie a requisição**:
   - Abra o arquivo `requests.http` e clique no botão "Send Request" acima da linha `GET http://localhost:3333/users`.

3. **Verifique a resposta**:
   - Você deve ver a lista de usuários no formato JSON.

### 3. Atualize um Usuário

1. **Abra o arquivo `src/app.ts`**:
   - No painel esquerdo do VSCode, clique em **Explorer**.
   - Encontre e abra o arquivo `src/app.ts`.

2. **Adicione a rota para atualizar um usuário**:
   ```typescript
   app.put('/users/:id', async (req, res) => {
     const db = await connect();
     const { id } = req.params;
     const { name, email } = req.body;

     await db.run('UPDATE users SET name = ?, email = ? WHERE id = ?', [name, email, id]);

     const user = await db.get('SELECT * FROM users WHERE id = ?', [id]);
     res.json(user);
   });
   ```
   - `app.put('/users/:id', async (req, res) => { ... });` define uma rota PUT para atualizar um usuário existente.
   - `await db.run('UPDATE users SET name = ?, email = ? WHERE id = ?', [name, email, id]);` atualiza o usuário com o ID fornecido.
   - `const user = await db.get('SELECT * FROM users WHERE id = ?', [id]);` recupera o usuário atualizado.
   - `res.json(user);` envia a resposta com os dados do usuário atualizado.

### 4. Teste a Atualização de Dados

1. **Adicione a seguinte requisição ao arquivo `requests.http`**:
   ```
   PUT http://localhost:3333/users/1
   Content-Type: application/json

   {
     "name": "Jane Doe",
     "email": "janedoe@mail.com"
   }
   ```

2. **Envie a requisição**:
   - Abra o arquivo `requests.http` e clique no botão "Send Request" acima da linha `PUT http://localhost:3333/users/1`.

3. **Verifique a resposta**:
   - Você deve ver a resposta com os dados do usuário atualizado.

### 5. Exclua um Usuário

1. **Abra o arquivo `src/app.ts`**:
   - No painel esquerdo do VSCode, clique em **Explorer**.
   - Encontre e abra o arquivo `src/app.ts`.

2. **Adicione a rota para excluir um usuário**:
   ```typescript
   app.delete('/users/:id', async (req, res) => {
     const db = await connect();
     const { id } = req.params;

     await db.run('DELETE FROM users WHERE id = ?', [id]);

     res.status(204).send();
   });
   ```
   - `app.delete('/users/:id', async (req, res) => { ... });` define uma rota DELETE para excluir um usuário.
   - `await db.run('DELETE FROM users WHERE id = ?', [id]);` remove o usuário com o ID fornecido.
   - `res.status(204).send();` envia uma resposta de sucesso sem conteúdo.

### 6. Teste a Exclusão de Dados

1. **Adicione a seguinte requisição ao arquivo `requests.http`**:
   ```
   DELETE http://localhost:3333/users/1
   ```

2. **Envie a requisição**:
   - Abra o arquivo `requests.http` e clique no botão "Send Request" acima da linha `DELETE http://localhost:3333/users/1`.

3. **Verifique a resposta**:
   - Você deve receber uma resposta sem conteúdo (status 204).

---

Vamos continuar com o tutorial para garantir que você consiga testar o frontend do seu projeto Node.js com sucesso.

---

# Agora iremos fazer o Frontend para o Projeto Node.js com TypeScript

## Passo 1: Criar a Pasta `public`

1. **Abra o Visual Studio Code**.

   ![Ícone do VSCode](https://code.visualstudio.com/assets/images/branding/blue.png)

2. **Criar uma Nova Pasta**:
   - No painel lateral esquerdo, clique com o botão direito na pasta raiz do seu projeto.
   - Selecione **"Nova Pasta"**.
   - Nomeie a nova pasta como `public`.

   ![Criar Pasta no VSCode](https://code.visualstudio.com/assets/docs/getstarted/firststeps/new-folder.png)

## Passo 2: Criar os Arquivos HTML, CSS e JS

### 2.1 Criar o Arquivo `index.html`

1. **Criar Novo Arquivo**:
   - Clique com o botão direito na pasta `public` que você acabou de criar.
   - Selecione **"Novo Arquivo"**.
   - Nomeie o arquivo como `index.html`.

   ![Criar Arquivo no VSCode](https://code.visualstudio.com/assets/docs/getstarted/firststeps/new-file.png)

2. **Adicionar Código ao Arquivo `index.html`**:
   - Abra o arquivo `index.html` que você criou.
   - Cole o seguinte código:

     ```html
     <!DOCTYPE html>
     <html lang="pt-BR">
     <head>
         <meta charset="UTF-8">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         <title>Meu Projeto Node.js</title>
         <link rel="stylesheet" href="styles.css">
     </head>
     <body>
         <header>
             <h1>Bem-vindo ao Meu Projeto Node.js</h1>
         </header>
         <main>
             <section id="content">
                 <p>Esta é a interface do usuário para o projeto.</p>
                 <button id="fetchDataBtn">Buscar Dados</button>
                 <div id="dataOutput"></div>
             </section>
         </main>
         <script src="script.js"></script>
     </body>
     </html>
     ```

   - **Salvar Arquivo**: Pressione `Ctrl + S` (ou `Cmd + S` no macOS).

   ![Arquivo HTML](https://www.htmlcodetutorial.com/images/htmleditor.gif)

### 2.2 Criar o Arquivo `styles.css`

1. **Criar Novo Arquivo**:
   - Na pasta `public`, clique com o botão direito novamente.
   - Selecione **"Novo Arquivo"**.
   - Nomeie o arquivo como `styles.css`.

2. **Adicionar Código ao Arquivo `styles.css`**:
   - Abra o arquivo `styles.css`.
   - Cole o seguinte código:

     ```css
     body {
         font-family: Arial, sans-serif;
         margin: 0;
         padding: 0;
         display: flex;
         flex-direction: column;
         align-items: center;
         justify-content: center;
         min-height: 100vh;
         background-color: #f4f4f4;
     }

     header {
         background-color: #333;
         color: #fff;
         width: 100%;
         padding: 1rem 0;
         text-align: center;
     }

     main {
         padding: 2rem;
         background-color: #fff;
         border-radius: 8px;
         box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
     }

     button {
         background-color: #28a745;
         color: white;
         border: none;
         padding: 10px 20px;
         cursor: pointer;
         border-radius: 5px;
     }

     button:hover {
         background-color: #218838;
     }

     #dataOutput {
         margin-top: 1rem;
         padding: 10px;
         background-color: #e9ecef;
         border-radius: 5px;
         width: 100%;
         text-align: left;
     }
     ```

   - **Salvar Arquivo**: Pressione `Ctrl + S` (ou `Cmd + S` no macOS).

### 2.3 Criar o Arquivo `script.js`

1. **Criar Novo Arquivo**:
   - Na pasta `public`, clique com o botão direito novamente.
   - Selecione **"Novo Arquivo"**.
   - Nomeie o arquivo como `script.js`.

2. **Adicionar Código ao Arquivo `script.js`**:
   - Abra o arquivo `script.js`.
   - Cole o seguinte código:

     ```javascript
     document.getElementById('fetchDataBtn').addEventListener('click', fetchData);

     async function fetchData() {
         try {
             const response = await fetch('/api/data');
             const data = await response.json();
             document.getElementById('dataOutput').innerText = JSON.stringify(data, null, 2);
         } catch (error) {
             document.getElementById('dataOutput').innerText = 'Erro ao buscar dados';
             console.error('Erro:', error);
         }
     }
     ```

   - **Salvar Arquivo**: Pressione `Ctrl + S` (ou `Cmd + S` no macOS).

## Passo 3: Configurar o Servidor para Servir os Arquivos Estáticos

1. **Abrir o Arquivo Principal do Servidor**:
   - No Visual Studio Code, abra o arquivo principal do servidor, que pode ser chamado de `server.ts` ou `index.ts`.

2. **Adicionar Código para Servir Arquivos Estáticos**:
   - Encontre a parte do código onde o Express é inicializado.
   - Adicione o seguinte código logo após a inicialização do Express:

     ```typescript
     import express from 'express';
     const app = express();

     app.use(express.static('public'));

     // Código adicional do servidor
     ```

   - **Salvar Arquivo**: Pressione `Ctrl + S` (ou `Cmd + S` no macOS).

   ![Adicionar Código no VSCode](https://code.visualstudio.com/assets/docs/editor/code-snippets/adding-code.png)

## Passo 4: Testar o Frontend

1. **Executar o Servidor**:
   - No terminal do Visual Studio Code, execute o servidor com o comando:
     ```bash
     npm run dev
     ```
   - Isso iniciará o servidor, que agora deve servir também os arquivos estáticos da pasta `public`.

2. **Abrir o Navegador e Acessar o Projeto**:
   - Abra o Google Chrome ou outro navegador da sua escolha.
   - Na barra de endereços, digite o seguinte URL:
     ```
     http://localhost:3000
     ```
   - Pressione `Enter`.

   ![Barra de Endereços do Chrome](https://www.lifewire.com/thmb/nPV2F4g9hOt7VxIfZxSow7S58to=/768x0/filters:no_upscale():max_bytes(150000):strip_icc()/chrome-address-bar-5b7d0820c9e77c00274c5444.png)

3. **Verificar se a Página Está Sendo Exibida Corretamente**:
   - Você deve ver a página com a interface do usuário que você criou. Clique no botão "Buscar Dados" e veja se os dados são exibidos corretamente na página.

---

Seguindo estes passos, você terá configurado o frontend do seu projeto Node.js e garantido que ele funcione corretamente com o backend.

### Testando o Projeto no Google Chrome

Agora que você configurou seu backend com Node.js e o frontend (se aplicável), aqui estão as etapas para testar o projeto no Google Chrome:

---

## 1. Abrindo o Projeto no Google Chrome

### 1.1 Verificando o Servidor Backend

1. **Certifique-se de que o servidor está em execução**:
   - No Visual Studio Code (VSCode), abra o terminal (`Terminal > New Terminal`).
   - Execute o comando:
     ```bash
     npm run dev
     ```
   - Isso inicia o servidor no modo de desenvolvimento. Você deve ver a mensagem `Server running on port 3333` no terminal.

   ![Executar Comando no VSCode](https://code.visualstudio.com/assets/docs/editor/terminal/terminal-run.png)

2. **Abra o Google Chrome**:
   - Clique no ícone do Google Chrome na sua área de trabalho ou no menu de aplicativos.

   ![Ícone do Google Chrome](https://upload.wikimedia.org/wikipedia/commons/4/42/Google_Chrome_icon_%282011%29.png)

3. **Acesse o servidor local**:
   - Na barra de endereços do Google Chrome, digite o seguinte URL:
     ```
     http://localhost:3333
     ```
   - Pressione `Enter`.

   ![Barra de Endereços do Chrome](https://www.lifewire.com/thmb/nPV2F4g9hOt7VxIfZxSow7S58to=/768x0/filters:no_upscale():max_bytes(150000):strip_icc()/chrome-address-bar-5b7d0820c9e77c00274c5444.png)

4. **Verifique a resposta**:
   - Se tudo estiver configurado corretamente, você verá a mensagem `Hello World` exibida na página.

---

## 2. Testando as Requisições HTTP com o Frontend (Se Aplicável)

### 2.1 Testando com o Frontend

Se você tiver uma interface frontend que se comunica com o backend, você precisará seguir as etapas para garantir que tudo esteja funcionando bem. Vamos supor que você tenha uma interface básica para adicionar e listar usuários.

1. **Abra o Google Chrome**:
   - Clique no ícone do Google Chrome na sua área de trabalho ou no menu de aplicativos.

2. **Acesse o frontend**:
   - Se o frontend estiver em um servidor separado, digite o URL correspondente na barra de endereços. Por exemplo:
     ```
     http://localhost:3000
     ```
   - Se o frontend for parte do mesmo projeto e servido pelo mesmo servidor backend, use o URL do backend:
     ```
     http://localhost:3333
     ```

3. **Interaja com a interface**:
   - Se houver formulários para adicionar usuários ou outros elementos interativos, preencha os campos e envie as requisições.
   - Observe o comportamento da aplicação e certifique-se de que os dados estão sendo manipulados corretamente.

   ![Interface do Usuário no Chrome](https://www.guidingtech.com/wp-content/uploads/2021/03/Chrome_DevTools_20210316-1440x803.png)

### 2.2 Testando Requisições com o `requests.http`

Se você estiver usando o arquivo `requests.http` para enviar requisições diretamente, siga estes passos:

1. **Abra o arquivo `requests.http` no VSCode**:
   - No painel esquerdo do VSCode, clique em **Explorer**.
   - Encontre e abra o arquivo `requests.http`.

2. **Envie requisições**:
   - Para testar as requisições HTTP, clique no botão "Send Request" acima de cada bloco de código de requisição.

   ![Enviar Requisição no VSCode](https://code.visualstudio.com/assets/docs/editor/rest-client/rest-client-send-request.png)

3. **Verifique a resposta**:
   - Veja a resposta da requisição na janela de resultados do Rest Client no VSCode.

---

## Resumo

1. **Para testar o backend**:
   - Certifique-se de que o servidor está em execução (`npm run dev`).
   - Acesse `http://localhost:3333` no Google Chrome.

2. **Para testar o frontend**:
   - Abra o frontend no Google Chrome no URL apropriado (`http://localhost:3000` ou similar).
   - Interaja com a interface e verifique a comunicação com o backend.

3. **Para testar diretamente com `requests.http`**:
   - Abra o arquivo `requests.http` no VSCode e envie as requisições.

Seguindo estas etapas, você poderá garantir que tanto o backend quanto o frontend estejam funcionando corretamente e se comunicando como esperado. Se você encontrar algum problema, verifique o terminal para mensagens de erro e ajuste o código conforme necessário.
