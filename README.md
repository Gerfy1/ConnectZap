# ConnectZap
Projeto voltado a CRM com integração ao Whatsapp
[ ConnectZap ]

Usar o padrão Feature Branch:

- main: Código de produção estável
- develop: Código de testes, é aqui que juntamos as tarefas antes de jogar para main

# Branchs de trabalho: Cada nova func cria uma branch separada

Padrão de nomes para Branches: Usar prefixos para saber oq cada um tá fazendo

- feat/nome-da-func (para coisas novas)
	ex: feat/login-tela, feat/baileys-connection, feat/envio-mensagem
- fix/nome-do-bug (para correção)
	ex: fix/qr-code-error, fix/layout-mobile
- chore/nome-da-tarefa (configurações, docs, limpeza)
	ex: chore/setup-eslint, chore/update-readme

# A Estrutura da pasta: [Tipo monorepo]
Iremos usar mono repo simples com as duas principais na raiz, isso facilita rodar o projeto todo de uma vez e compartilhar tipos (typescript).

Uma sugetão feita por prompt:
```
connect-zap/
├── .github/                 # configuraçoes do Git/Actions
├── docs/                    # documentação simples do projeto
│
├── backend/                 # (Node.js + Baileys + Prisma)
│   ├── src/
│   │   ├── config/          # aariaveis de ambiente, configs do banco
│   │   ├── controllers/     # quem recebe a requisição HTTP (Ex: SessionController)
│   │   ├── services/        # A logica pesada
│   │   │   ├── WppService/  # Lógica do Baileys (Connect, SendMsg)
│   │   │   └── AuthService/ # Login, JWT
│   │   ├── routes/          # Rotas da API (v1/sessions, v1/chats)
│   │   ├── models/          # Se não usar Prisma, ficaria aqui. Com Prisma, fica na raiz do back.
│   │   ├── libs/            # Onde fica a classe "socket.io" e o "wppconnect/baileys"
│   │   └── app.ts           # entrada do servidor
│   ├── prisma/              # schema do banco de dados
│   └── package.json
│
├── frontend/                # (React/Next.js + Tailwind)
│   ├── src/
│   │   ├── components/      # botoes, Modais, Inputs
│   │   ├── pages/           # telas (Login, Dashboard, Configs)
│   │   ├── contexts/        # authContext (Guardar usuario logado)
│   │   ├── hooks/           # useWebSocket, useAuth
│   │   ├── services/        # chamadas pra API (axios/api.ts)
│   │   └── styles/
│   └── package.json
│
└── README.md                # instruções de como rodar o projeto
```


# [Trello] https://trello.com/invite/b/693084acf1ba70ee8e18b692/ATTIba3ae1e939a80095090b6d0dee19763949E11692/kanban-whatsapp-project

Serão 4 colunas: Backlog (Caixa de entrada das tasks e Ideias futuras), To Do (Fazer nessa semana), Doing (Fazendo agora), Done

As Tasks Iniciais (Cards) essenciais para o MVP


# Divisão do trabalho: Quem faz oq?

Dev A (Focado no Backend/Infra):
-Cuida do banco de dados (Prisma).
-Cuida da integração com a Baileys.
-Garante que o QR Code chegue no frontend via WebSocket.
-Meta: Fazer o WhatsApp conectar e dizer "estou online".

Dev B (Focado no Frontend/Produto):

-Cuida das telas e rotas.
-Consome a API que o Dev A está criando.
-Deixa o chat bonito e responsivo.
-Meta: Fazer o usuário conseguir ler o QR Code e ver a lista de conversas carregando.

Combiar o formato dos dados(JSON) antes de codar. Exemplo: "Cara, vou te mandar a lista de chats assim: { id: 1, name: 'João', lastMessage: 'Oi' }. Pode ser?" Isso evita que o Front espere "nome" e o Back mande "name".

Então ter um padrão
# Lembrando que usaremos Multi-tenant
