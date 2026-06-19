# 🎯 Fluxo de Dados - Backend ↔ Frontend

## Diagrama da Arquitetura

```
┌─────────────────────────────────────────────────────────────────┐
│                    🌐 Frontend (React + Vite)                   │
│                    http://localhost:5173                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  Componentes React                                      │   │
│  │  ├── FormCliente.jsx                                    │   │
│  │  ├── FormProduto.jsx                                    │   │
│  │  ├── FormPedido.jsx                                     │   │
│  │  └── Dashboard (opcional)                               │   │
│  └─────────────────────────────────────────────────────────┘   │
│                           ↓                                      │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  src/services/api.js (Client HTTP Centralizado)         │   │
│  │  ├── cadastrarCliente()                                 │   │
│  │  ├── cadastrarProduto()                                 │   │
│  │  ├── cadastrarPedido()                                  │   │
│  │  ├── adicionarItemPedido()                              │   │
│  │  └── listarPedidosCompletos()                           │   │
│  └─────────────────────────────────────────────────────────┘   │
│                           ↓                                      │
│              .env.local (VITE_API_URL)                          │
│         http://localhost:5000 (ou outra porta)                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
                         HTTP/JSON
                             ↕
         (requisições POST/GET com CORS habilitado)
                             ↕
┌─────────────────────────────────────────────────────────────────┐
│                   🔧 Backend (Flask + SQLite)                    │
│                    http://localhost:5000                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  Rotas da API                                           │   │
│  │  ├── POST   /clientes                                   │   │
│  │  ├── POST   /produtos                                   │   │
│  │  ├── POST   /pedidos                                    │   │
│  │  ├── POST   /itens-pedido                               │   │
│  │  └── GET    /pedidos/completos                          │   │
│  └─────────────────────────────────────────────────────────┘   │
│                           ↓                                      │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  Banco de Dados (SQLite)                                │   │
│  │  ├── Tabela Cliente                                     │   │
│  │  ├── Tabela Produto                                     │   │
│  │  ├── Tabela Pedido                                      │   │
│  │  └── Tabela Item_Pedido                                 │   │
│  └─────────────────────────────────────────────────────────┘   │
│                 sistema_extensao.db                             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📊 Fluxo de Requisições (Exemplos)

### 1️⃣ Cadastrar Cliente

```
┌─────────────────┐
│  FormCliente    │
│  (React)        │
└────────┬────────┘
         │ handleSubmit()
         ↓
┌─────────────────┐
│  api.js         │
│  cadastrar      │
│  Cliente()      │
└────────┬────────┘
         │ fetch POST /clientes
         ↓
┌─────────────────┐
│  Flask Backend  │
│  main.py        │
└────────┬────────┘
         │ INSERT INTO Cliente
         ↓
┌─────────────────┐
│  SQLite         │
│  Tabela Cliente │
└────────┬────────┘
         │ ✓ Cliente adicionado
         ↓
┌─────────────────┐
│  Response JSON  │
│  {              │
│    mensagem,    │
│    id_cliente   │
│  }              │
└────────┬────────┘
         │ Volta para api.js
         ↓
┌─────────────────┐
│  FormCliente    │
│  setStatus()    │
│  Exibe ✓        │
└─────────────────┘
```

### 2️⃣ Listar Pedidos

```
┌──────────────┐
│  Dashboard   │
│  useEffect   │
└──────┬───────┘
       │ listarPedidosCompletos()
       ↓
┌──────────────┐
│  api.js      │
│  fetch GET   │
└──────┬───────┘
       │
       ↓
┌──────────────┐
│  Flask:      │
│  /pedidos/   │
│  completos   │
└──────┬───────┘
       │ SELECT JOIN
       ↓
┌──────────────┐
│  SQLite      │
│  (JOIN de    │
│  3 tabelas)  │
└──────┬───────┘
       │ Array de objetos
       ↓
┌──────────────┐
│  Response:   │
│  [{          │
│   id_pedido, │
│   nome_clie, │
│   itens: []  │
│  }]          │
└──────┬───────┘
       │
       ↓
┌──────────────┐
│  Dashboard   │
│  setPedidos()│
│  map/render  │
└──────────────┘
```

---

## 🔗 Modelo de Dados Relacionais

```
┌──────────────────────┐
│      CLIENTE         │
├──────────────────────┤
│ id_cliente (PK)      │
│ nome                 │
│ email (UNIQUE)       │
│ telefone             │
│ endereco             │
│ senha (HASH)         │
└──────────────────────┘
         ↑
         │ 1:N
         │
┌──────────────────────┐         ┌──────────────────────┐
│       PEDIDO         │    N:M  │     ITEM_PEDIDO      │
├──────────────────────┤────────→├──────────────────────┤
│ id_pedido (PK)       │         │ id_pedido (FK)       │
│ id_cliente (FK)      │         │ id_produto (FK)      │
│ data                 │         │ qtd_pedido           │
│ status               │         │ valor_unitario       │
│ total                │         └──────────────────────┘
└──────────────────────┘                   ↑
                                           │
                                           │ N:M
                                           │
                            ┌──────────────────────┐
                            │     PRODUTO          │
                            ├──────────────────────┤
                            │ id_produto (PK)      │
                            │ tipo                 │
                            │ nome                 │
                            │ descricao            │
                            └──────────────────────┘
```

---

## 🔄 Estados dos Componentes

```
FormCliente Component State Flow:

'idle' (inicial)
  ↓
[Usuário preenche formulário]
  ↓
[Clica em enviar]
  ↓
'loading' (enviando)
  ↓
[Resposta do servidor]
  ├→ ✓ Sucesso → 'success' → (limpar após 3s) → 'idle'
  └→ ✗ Erro    → 'error'   → (quando muda input) → 'idle'
```

---

## 🌐 Fluxo HTTP

### Request (Frontend → Backend)

```http
POST /clientes HTTP/1.1
Host: localhost:5000
Content-Type: application/json
Origin: http://localhost:5173

{
  "nome": "João Silva",
  "email": "joao@email.com",
  "telefone": "11999999999",
  "endereco": "Rua A, 123",
  "senha": "senha123"
}
```

### Response (Backend → Frontend)

```http
HTTP/1.1 201 Created
Access-Control-Allow-Origin: *
Content-Type: application/json

{
  "mensagem": "Cliente cadastrado com sucesso!",
  "id_cliente": 1
}
```

---

## 📝 Arquivo .env.local

```
VITE_API_URL=http://localhost:5000
  ↓
import.meta.env.VITE_API_URL
  ↓
Usado em api.js
  ↓
const API_BASE_URL = import.meta.env.VITE_API_URL || 'http://localhost:5000'
```

---

## 🚀 Sequência de Inicialização

```
1. Usuário executa: npm run dev
   ├→ Vite inicia em :5173
   ├→ React carrega
   └→ .env.local é lido
   
2. Usuário abre: http://localhost:5173
   ├→ App.jsx carrega
   ├→ PaginaAdm carrega
   └→ Formulários aparecem
   
3. Backend está rodando: python main.py
   ├→ Flask inicia em :5000
   ├→ CORS habilitado
   ├→ Banco de dados inicializado
   └→ Pronto para requisições
   
4. Usuário interage com formulário
   ├→ handleSubmit() executado
   ├→ api.js faz fetch
   ├→ Flask recebe requisição
   ├→ Dados salvos no SQLite
   └→ Response volta ao React
```

---

**Última atualização**: 19/12/2024
