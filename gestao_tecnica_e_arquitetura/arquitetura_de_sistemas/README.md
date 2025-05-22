# E-commerce

Este repositório contém o código para um **sistema de e-commerce** básico com **checkout** integrado.

O projeto segue uma arquitetura monolítica onde todos os componentes do sistema (checkout, pagamento, estoque) estão dentro de um único serviço. Esse modelo é adequado para sistemas menores ou para um MVP, mas tem limitações em termos de escalabilidade e flexibilidade à medida que o sistema cresce.

---

## Visão Geral

O sistema é composto pelas seguintes partes principais:

- **Frontend (React)**: Interface do usuário para realizar compras e iniciar o checkout.
- **Backend (Express + TypeScript)**: API que gerencia as requisições de checkout, pagamento e estoque.
- **Banco de Dados**: Armazena os dados de produtos, usuários e transações de pagamento.
- **Cache**: Usado para armazenar dados frequentemente acessados, como o inventário de produtos, para melhorar a performance.

---

## Tecnologias Utilizadas

- **Frontend**: React, TypeScript, Axios (para fazer requisições HTTP).
- **Backend**: Express, TypeScript, Node.js, JWT (para autenticação).
- **Banco de Dados**: PostgreSQL (para persistência dos dados de produtos, pagamentos e estoque).
- **Cache**: Redis (para armazenar em cache os dados de estoque frequentemente acessados).

---

## Arquitetura do Sistema (Monolítica)

A arquitetura atual do sistema é monolítica, o que significa que todos os componentes do sistema (checkout, pagamento, estoque) estão integrados em uma única aplicação. A comunicação entre as camadas do sistema é direta e não há isolamento entre os diferentes componentes.

### Exemplo de Arquitetura Monolítica:

```plaintext
            Frontend
                ↓
 Backend: Sistema de Checkout
     ↙              ↓              ↘
Estoque     Pagamento         Cache
```

- **Frontend**: O usuário interage com o sistema através da interface React. Quando o usuário finaliza a compra, ele envia os dados para o backend.
- **Backend (Express)**: O servidor Express gerencia as requisições de checkout e interage com o banco de dados de estoque e pagamento.
- **Banco de Dados**: O PostgreSQL armazena dados de produtos e transações. O estoque é atualizado diretamente no banco.
- **Cache**: O Redis é usado para armazenar em cache o estoque de produtos, evitando consultas repetitivas ao banco de dados.

## Instalação e Execução

### Pré-requisitos

- Node.js (v14 ou superior)
- PostgreSQL
- Redis (opcional, mas recomendado para cache)

---

### Configuração do Projeto

- Clone o repositório:

```bash
git clone https://github.com/seu-usuario/ecommerce-checkout.git
cd ecommerce-checkout
```

- Instalar as dependências:

```bash
npm install
```

- Configurar o banco de dados

---

### Configuração do Banco de Dados

Crie um banco de dados PostgreSQL local chamado `ecommerce` e execute as migrações:

```bash
psql -U postgres
CREATE DATABASE ecommerce;
```

Em seguida, configure as credenciais do banco de dados no arquivo `.env`:

```env
DB_HOST=localhost
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=sua-senha
DB_NAME=ecommerce
```

- Configurar o Redis (opcional, mas recomendado)

---

### Configuração do Redis (opcional)

Caso queira utilizar o Redis como cache, instale o Redis localmente ou utilize um serviço de Redis. Configure no arquivo `.env`:

```env
REDIS_HOST=localhost
REDIS_PORT=6379
```

---

### Inicialização

Para iniciar o servidor do backend:

```bash
npm run dev
```

---

## Estrutura do Projeto

A estrutura do projeto está organizada da seguinte forma:

```plaintext
ecommerce-checkout/
├── client/                       # Frontend (React)
│   └── src/
│       ├── components/          # Componentes React
│       ├── App.tsx             # Componente principal
│       └── index.tsx           # Arquivo de entrada
│   └── public/                 # Arquivos públicos (HTML, ícones, etc.)
│
├── server/                      # Backend (Express)
│   └── src/
│       ├── controllers/        # Lógica de negócios (ex: checkout)
│       ├── models/            # Modelos de dados (ex: usuários, estoque)
│       ├── routes/            # Rotas da API
│       └── utils/             # Utilitários (ex: autenticação, helpers)
│   ├── .env                    # Variáveis de ambiente
│   └── server.ts              # Arquivo de entrada do backend
│
├── .gitignore                  # Arquivos a serem ignorados pelo git
├── package.json                # Dependências do projeto
├── README.md                   # Documentação do projeto
└── tsconfig.json               # Configurações do projeto
```
