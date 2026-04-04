# PlanejadorDeMetas

Aplicacao full-stack para cadastrar metas semanais, acompanhar pendencias e registrar conclusoes ao longo da semana.

O projeto e dividido em duas partes:

- `server/`: API em Node.js com Fastify, Drizzle ORM e PostgreSQL
- `web/`: interface em React com Vite, React Query e Tailwind CSS

## O que a aplicacao faz

- cadastra metas com frequencia semanal desejada
- lista metas pendentes da semana
- registra conclusao de uma meta
- mostra resumo semanal com total de metas e progresso
- agrupa conclusoes por dia da semana

## Stack

### Backend

- Node.js
- TypeScript
- Fastify
- Drizzle ORM
- PostgreSQL
- Zod

### Frontend

- React
- TypeScript
- Vite
- Tailwind CSS
- TanStack Query
- React Hook Form
- Radix UI

## Estrutura do projeto

```text
server/
  src/db/              schema, conexao e seed
  src/functions/       regras de negocio
  src/http/routes/     rotas HTTP
  migrations/          migrations do Drizzle
web/
  src/components/      componentes de interface
  src/http/            chamadas para a API
```

## Funcionalidades principais

### Cadastro de metas

Cada meta possui:

- titulo
- frequencia semanal desejada de 1 a 7 vezes

### Resumo semanal

O resumo mostra:

- total de metas previstas para a semana
- total de metas concluidas
- percentual de progresso
- historico de metas concluidas por dia

### Pendencias

As metas pendentes sao calculadas no backend considerando:

- metas criadas ate o fim da semana atual
- quantidade de conclusoes ja registradas no periodo
- frequencia semanal definida para cada meta

## Como executar

Pre-requisitos:

- Node.js instalado
- PostgreSQL disponivel

### 1. Configurar o backend

Entre na pasta `server` e garanta um arquivo `.env` com:

```env
DATABASE_URL=postgresql://usuario:senha@localhost:5432/seu_banco
```

Instale as dependencias:

```bash
cd server
npm install
```

Rode a API:

```bash
npm run dev
```

A API sobe na porta:

```text
http://localhost:3333
```

### 2. Popular dados iniciais

Ainda na pasta `server`:

```bash
npm run seed
```

### 3. Rodar o frontend

Em outro terminal:

```bash
cd web
npm install
npm run dev
```

O frontend consome a API em `http://localhost:3333`.

## Endpoints principais

- `POST /goals`
- `POST /completions`
- `GET /pending-goals`
- `GET /summary`

## Banco de dados

O schema atual possui duas tabelas principais:

- `goals`
- `goal_completions`

As migrations ficam em `server/migrations/` e o schema Drizzle esta em `server/src/db/schema.ts`.

## Observacoes importantes

- o frontend usa URL fixa para buscar o resumo em `http://localhost:3333`
- a configuracao da API depende da variavel `DATABASE_URL`
- o projeto possui seed inicial para facilitar testes manuais
- o repositório contem `node_modules/` versionado no estado atual

## Melhorias futuras

- criar um `.env.example`
- parametrizar a URL da API no frontend por variavel de ambiente
- adicionar autenticacao
- adicionar testes automatizados no backend e no frontend
- remover arquivos versionados desnecessarios, como `node_modules/`
