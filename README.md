# 🍜 Sistema de Gestão de Marmitas

> **Status**: ✅ Backend-Frontend **Totalmente Integrado e Funcional**

## 📋 Índice
- [Visão Geral](#visão-geral)
- [Quick Start](#-quick-start)
- [Requisitos](#requisitos)
- [Instalação](#instalação)
- [Arquitetura](#arquitetura)
- [Funcionalidades](#funcionalidades)
- [Endpoints da API](#endpoints-da-api)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Como Usar](#como-usar)
- [Troubleshooting](#troubleshooting)

---

## 🎯 Visão Geral

Sistema web completo para gerenciar **clientes, produtos (marmitas) e pedidos** em tempo real.

### Stack Tecnológico

**Backend:**
- Python 3.x
- Flask (framework web)
- SQLite (banco de dados)
- Werkzeug (criptografia de senhas)

**Frontend:**
- React 19+
- Vite (build tool)
- JavaScript ES6+
- Fetch API

**Integração:**
- RESTful API com JSON
- CORS habilitado
- Sem dependências externas desnecessárias

---

## 🚀 Quick Start

### Pré-requisitos
- Python 3.x instalado
- Node.js e npm instalados
- Git (opcional)

### Em 2 Minutos:

**Terminal 1 - Backend:**
```bash
cd backend_python
pip install flask flask-cors werkzeug
python main.py
```
✓ Acesso em: **http://localhost:5000**

**Terminal 2 - Frontend:**
```bash
cd front/AtvMetodosAPI
npm install
npm run dev
```
✓ Acesso em: **http://localhost:5173**

**Abra no navegador:** http://localhost:5173 ✅

Pronto! A aplicação está rodando.

---

## 📦 Requisitos

### Backend
```bash
# Dependências Python (instale com):
pip install flask flask-cors werkzeug
```

### Frontend
```bash
# Dependências Node.js (npm install):
- react@^19.2.6
- react-dom@^19.2.6
- vite@^8.0.12
```

---

## 📥 Instalação Detalhada

### 1. Clonar/Abrir o Projeto
```bash
cd /caminho/para/brafront
```

### 2. Backend Setup
```bash
cd backend_python

# Criar ambiente virtual (opcional mas recomendado)
python -m venv venv
source venv/bin/activate  # Linux/Mac
# ou
venv\Scripts\activate     # Windows

# Instalar dependências
pip install flask flask-cors werkzeug

# Rodar
python main.py
```

Você verá:
```
WARNING in app.run() is not recommended...
* Running on http://127.0.0.1:5000
```

### 3. Frontend Setup
```bash
cd front/AtvMetodosAPI

# Instalar dependências
npm install

# Rodar em desenvolvimento
npm run dev
```

Você verá:
```
  VITE v8.0.12  ready in XXX ms

  ➜  Local:   http://localhost:5173/
```

### 4. Acessar a Aplicação
Abra seu navegador em: **http://localhost:5173**

---

## 🏗️ Arquitetura

### Diagrama de Fluxo

```
┌─────────────────────────────────────┐
│     Navegador (Frontend)            │
│     React + Vite                    │
│     http://localhost:5173           │
├─────────────────────────────────────┤
│  Componentes:                       │
│  ├─ FormCliente                     │
│  ├─ FormProduto                     │
│  ├─ FormPedido                      │
│  └─ TesteAPI (validação)            │
│                                     │
│  Estado gerenciado com useState()   │
└────────────┬────────────────────────┘
             │
             ↓ (Requisição HTTP POST/GET)
             │
┌────────────────────────────────────┐
│   API Client (services/api.js)     │
│   Centraliza todas as requisições  │
│   URL: http://localhost:5000       │
└────────────┬───────────────────────┘
             │
             ↓ (JSON)
             │
┌────────────────────────────────────┐
│     Backend (Flask)                │
│     Python + main.py               │
│     http://localhost:5000          │
├────────────────────────────────────┤
│  Rotas:                            │
│  ├─ POST /clientes                 │
│  ├─ POST /produtos                 │
│  ├─ POST /pedidos                  │
│  ├─ POST /itens-pedido             │
│  └─ GET /pedidos/completos         │
│                                    │
│  Validação de dados                │
│  Hash de senhas (Werkzeug)         │
│  CORS habilitado                   │
└────────────┬───────────────────────┘
             │
             ↓ (SQL)
             │
┌────────────────────────────────────┐
│   Banco de Dados (SQLite)          │
│   sistema_extensao.db              │
├────────────────────────────────────┤
│  Tabelas:                          │
│  ├─ Cliente (id, nome, email...)   │
│  ├─ Produto (id, nome, tipo...)    │
│  ├─ Pedido (id, data, status...)   │
│  └─ Item_Pedido (id_ped, id_prod)  │
│                                    │
│  Integridade referencial (FK)      │
│  Cascata de deleção                │
└────────────────────────────────────┘
```

### Fluxo de uma Requisição

```
1. Usuário preenche formulário
2. Clica em "Salvar"
3. handleSubmit() é executado
4. Chama função de api.js (ex: cadastrarCliente)
5. api.js faz fetch POST para http://localhost:5000/clientes
6. Backend recebe, valida dados
7. Backend insere no SQLite
8. Backend retorna JSON com resultado
9. Component recebe resposta
10. setState atualiza com mensagem de sucesso/erro
11. Usuário vê feedback visual
```

---

## ✨ Funcionalidades

### ✅ Implementadas

#### 1. Gestão de Clientes
```javascript
- Cadastro de novos clientes
- Campos: nome, email, telefone, endereço, senha
- Validação: email é obrigatório e único
- Segurança: senha é hasheada com Werkzeug
- Resposta: ID do cliente criado
```

#### 2. Gestão de Produtos (Marmitas)
```javascript
- Cadastro de produtos
- Campos: nome, tipo (Tradicional/Fit/Vegana), descrição
- Sem duplicação automática
- Armazenamento de informações de ingredientes
```

#### 3. Gestão de Pedidos
```javascript
- Criação de pedidos vinculados a clientes
- Campos: id_cliente, data, status, total
- Status: pendente, preparando, pronto, entregue
- Cálculo automático do total
- Histórico de pedidos
```

#### 4. Itens de Pedido
```javascript
- Adição de produtos aos pedidos
- Campos: id_pedido, id_produto, quantidade, valor_unitário
- Validação: produto e pedido devem existir
- Atualização automática do total do pedido
- Prevenção de duplicação de itens
```

#### 5. Listagem e Consulta
```javascript
- GET /pedidos/completos
- Retorna pedidos com detalhes de cliente e produtos
- JOIN de 3 tabelas (Pedido, Cliente, Produto)
- Informações completas para dashboard (pronto para implementar)
```

#### 6. Validação de Dados
```javascript
- Validação no frontend (estado, tipos)
- Validação no backend (obrigatoriedade, tipos)
- Mensagens de erro específicas
- Feedback visual para o usuário
```

#### 7. Tratamento de Erros
```javascript
- Try-catch em requisições
- Mensagens de erro claras
- Status HTTP apropriados (201, 400, 500)
- Logs no backend para debug
```

---

## 📡 Endpoints da API

### Base URL
```
http://localhost:5000
```

### Clientes

**Cadastrar Cliente**
```http
POST /clientes
Content-Type: application/json

{
  "nome": "João Silva",
  "email": "joao@email.com",
  "telefone": "11999999999",
  "endereco": "Rua A, 123",
  "senha": "senha123"
}

Response (201):
{
  "mensagem": "Cliente cadastrado com sucesso!",
  "id_cliente": 1
}
```

### Produtos

**Cadastrar Produto**
```http
POST /produtos
Content-Type: application/json

{
  "nome": "Marmita Tradicional",
  "tipo": "Tradicional",
  "descricao": "Arroz, feijão, carne e legumes"
}

Response (201):
{
  "mensagem": "Produto cadastrado com sucesso!",
  "id_produto": 1
}
```

### Pedidos

**Criar Pedido**
```http
POST /pedidos
Content-Type: application/json

{
  "id_cliente": 1,
  "data": "2026-06-19",
  "status": "pendente",
  "total": 0
}

Response (201):
{
  "mensagem": "Pedido iniciado com sucesso!",
  "id_pedido": 1
}
```

**Adicionar Item ao Pedido**
```http
POST /itens-pedido
Content-Type: application/json

{
  "id_pedido": 1,
  "id_produto": 1,
  "qtd_pedido": 2,
  "valor_unitario": 15.50
}

Response (201):
{
  "mensagem": "Item adicionado ao pedido com sucesso!"
}
```

**Listar Pedidos Completos**
```http
GET /pedidos/completos

Response (200):
[
  {
    "id_pedido": 1,
    "data": "2026-06-19",
    "status": "pendente",
    "total": 31.00,
    "nome_cliente": "João Silva",
    "itens": [
      {
        "qtd_pedido": 2,
        "valor_unitario": 15.50,
        "nome_produto": "Marmita Tradicional"
      }
    ]
  }
]
```

### Códigos de Status HTTP

| Código | Significado | Exemplo |
|--------|-------------|---------|
| 201 | Criado com sucesso | POST /clientes |
| 200 | Sucesso | GET /pedidos/completos |
| 400 | Erro no cliente | Email duplicado |
| 500 | Erro no servidor | Exceção não tratada |

---

## 📁 Estrutura do Projeto

```
brafront/
│
├── backend_python/                    # Backend Flask
│   ├── main.py                        # Aplicação principal
│   ├── sistema_extensao.db            # Banco SQLite (gerado)
│   └── venv/                          # Ambiente virtual (opcional)
│
├── front/AtvMetodosAPI/               # Frontend React
│   ├── .env.local                     # Configuração (local)
│   ├── .env.example                   # Modelo de configuração
│   ├── package.json                   # Dependências Node
│   ├── vite.config.js                 # Configuração Vite
│   ├── index.html                     # HTML raiz
│   │
│   └── src/
│       ├── main.jsx                   # Ponto de entrada React
│       ├── App.jsx                    # Componente raiz
│       ├── App.css                    # Estilos globais
│       │
│       ├── services/
│       │   └── api.js                 # ⭐ Client HTTP centralizado
│       │
│       ├── components/
│       │   └── TesteAPI.jsx           # Componente de teste
│       │
│       └── Pages/
│           └── PainelAdm/
│               ├── Dashboard/
│               │   └── Dashboard.jsx
│               ├── PaginaAdm/
│               │   ├── PaginaAdm.jsx
│               │   └── PaginaAdm.module.css
│               └── AdmComponents/
│                   ├── FormCliente.jsx       # ⭐ Cadastro cliente
│                   ├── FormProduto.jsx       # ⭐ Cadastro produto
│                   ├── FormPedido.jsx        # ⭐ Cadastro pedido
│                   └── Sidebar.jsx
│
└── Documentação/                      # Guias detalhados
    ├── README.md                      # Este arquivo
    ├── INDICE.md                      # Índice completo
    ├── LEIA-ME-PRIMEIRO.md            # Comece aqui
    ├── SETUP_CONEXAO.md               # Como rodar
    ├── FLUXO_DADOS.md                 # Diagramas
    ├── EXEMPLOS_INTEGRACAO.md         # Exemplos de código
    ├── CONEXAO_COMPLETA.md            # Guia completo
    ├── TROUBLESHOOTING.md             # Problemas e soluções
    ├── CHECKLIST.md                   # Verificação
    └── STATUS.txt                     # Status visual
```

---

## 📖 Como Usar

### 1. Cadastrar um Cliente

1. Acesse: http://localhost:5173
2. Preencha o formulário "Cadastrar Cliente" com:
   - Nome: João Silva
   - Email: joao@email.com (único!)
   - Telefone: 11999999999
   - Endereço: Rua A, 123
   - Senha: senha123

3. Clique em "Salvar Cliente"
4. Você verá: ✓ Cliente cadastrado com sucesso!
5. Anote o ID do cliente (aparece na resposta)

### 2. Cadastrar um Produto

1. Preencha "Cadastrar Produto (Marmita)" com:
   - Nome: Marmita Tradicional
   - Tipo: Tradicional
   - Descrição: Arroz, feijão, carne, brócolis

2. Clique em "Salvar Produto"
3. Você verá: ✓ Produto cadastrado com sucesso!

### 3. Criar um Pedido

1. Preencha "Registrar Novo Pedido" com:
   - ID do Cliente: 1 (do passo 1)
   - Data: (use a data de hoje)
   - Status: pendente
   - Total: 0 (será preenchido automaticamente)

2. Clique em "Gerar Pedido"
3. Você verá: ✓ Pedido registrado com sucesso!

### 4. Verificar no Banco de Dados

```bash
# Terminal:
sqlite3 backend_python/sistema_extensao.db

# No prompt SQLite:
sqlite> SELECT * FROM Cliente;
sqlite> SELECT * FROM Produto;
sqlite> SELECT * FROM Pedido;
```

---

## 🧪 Testes da Integração

### Teste 1: Via Formulário (Manual)
```
1. Preencha um formulário
2. Clique em enviar
3. Veja mensagem de sucesso ✓
```

### Teste 2: Via DevTools (Desenvolvedor)
```
1. Abra http://localhost:5173
2. Pressione F12 (DevTools)
3. Vá para aba "Network"
4. Preencha e envie formulário
5. Veja a requisição HTTP na lista
6. Clique nela e veja Request e Response
```

### Teste 3: Via SQLite (Banco de Dados)
```bash
sqlite3 backend_python/sistema_extensao.db
SELECT * FROM Cliente;
.quit
```

### Teste 4: Via Componente TesteAPI
```javascript
// Adicione em App.jsx temporariamente:
import TesteAPI from './components/TesteAPI'

export default function App() {
  return <TesteAPI />
}

// Salve e veja os testes executarem automaticamente
```

---

## ⚙️ Configuração

### Variáveis de Ambiente

Arquivo: `front/AtvMetodosAPI/.env.local`
```ini
# URL do Backend
VITE_API_URL=http://localhost:5000

# Se o backend estiver em outra máquina:
# VITE_API_URL=http://192.168.1.100:5000
```

### Mudar Portas

**Backend (Flask):**
```python
# Em backend_python/main.py, na última linha:
app.run(debug=True, port=3000)  # Mude 5000 para 3000
```

**Frontend (React):**
```bash
# Em outro terminal:
cd front/AtvMetodosAPI
npm run dev -- --port 3173  # Mude 5173 para 3173
```

---

## 🐛 Troubleshooting

### ❌ Erro: "Failed to fetch"

**Causa**: Backend não está rodando

**Solução**:
```bash
# Terminal 1:
cd backend_python
python main.py

# Você verá:
# * Running on http://127.0.0.1:5000
```

### ❌ Erro: "CORS policy blocked"

**Causa**: CORS não está habilitado no backend

**Solução**: Verifique em `main.py`:
```python
from flask_cors import CORS

app = Flask(__name__)
CORS(app)  # ← Deve estar aqui
```

### ❌ Erro: "Email already exists"

**Causa**: Email já foi cadastrado antes

**Solução**: Use um email diferente:
```javascript
// Use timestamp para garantir unicidade
const email = `usuario${Date.now()}@email.com`
```

### ❌ Erro: "ModuleNotFoundError: No module named 'flask'"

**Causa**: Dependências não instaladas

**Solução**:
```bash
pip install flask flask-cors werkzeug
```

### ❌ Erro: "Port 5000 already in use"

**Causa**: Outra aplicação está usando a porta

**Solução**:
```bash
# Matar processo na porta 5000:
lsof -i :5000
kill -9 <PID>

# Ou usar outra porta em main.py:
app.run(debug=True, port=3000)
```

### ❌ Banco de dados vazio

**Causa**: Banco não foi inicializado

**Solução**:
```bash
# Delete e recrie:
rm backend_python/sistema_extensao.db
python backend_python/main.py
```

👉 **Mais informações**: Ver [TROUBLESHOOTING.md](./TROUBLESHOOTING.md)

---

## 💻 Scripts Úteis

### Backend
```bash
# Rodar
cd backend_python && python main.py

# Com ambiente virtual
cd backend_python
source venv/bin/activate
python main.py

# Reinstalar dependências
pip install --upgrade pip
pip install flask flask-cors werkzeug
```

### Frontend
```bash
# Rodar em desenvolvimento
cd front/AtvMetodosAPI && npm run dev

# Build para produção
npm run build

# Preview do build
npm run preview

# Limpar cache
npm cache clean --force
rm -rf node_modules package-lock.json
npm install
```

### Banco de Dados
```bash
# Abrir SQLite
sqlite3 backend_python/sistema_extensao.db

# Ver tabelas
.tables

# Ver schema da tabela
.schema Cliente

# Consultar dados
SELECT * FROM Cliente;
SELECT * FROM Produto;
SELECT * FROM Pedido;

# Contar registros
SELECT COUNT(*) FROM Cliente;

# Sair
.quit
```

---

## 📚 Documentação Completa

Para informações mais detalhadas:

| Documento | Descrição |
|-----------|-----------|
| [LEIA-ME-PRIMEIRO.md](./LEIA-ME-PRIMEIRO.md) | Comece aqui (5 min) |
| [FLUXO_DADOS.md](./FLUXO_DADOS.md) | Diagramas de arquitetura |
| [EXEMPLOS_INTEGRACAO.md](./EXEMPLOS_INTEGRACAO.md) | Exemplos de código |
| [TROUBLESHOOTING.md](./TROUBLESHOOTING.md) | Problemas e soluções |
| [CONEXAO_COMPLETA.md](./CONEXAO_COMPLETA.md) | Guia técnico completo |
| [SETUP_CONEXAO.md](./SETUP_CONEXAO.md) | Setup passo a passo |
| [INDICE.md](./INDICE.md) | Índice de documentação |
| [CHECKLIST.md](./CHECKLIST.md) | Verificação completa |

---

## 🚀 Deploy

### Deploy Backend (Heroku/Railway)
```bash
# Criar requirements.txt
pip freeze > requirements.txt

# Deploy no Railway:
railway link
railway up
```

### Deploy Frontend (Vercel/Netlify)
```bash
# Build
npm run build

# Deploy no Vercel:
npm install -g vercel
vercel
```

---

## 📝 Notas Importantes

1. **Segurança**:
   - Senhas são hasheadas com Werkzeug ✓
   - CORS está configurado ✓
   - Validação de entrada no backend ✓

2. **Performance**:
   - SQLite é suficiente para desenvolvimento
   - Para produção, considere PostgreSQL

3. **Desenvolvimento**:
   - Use DevTools (F12) para debug
   - Verifique logs do backend em tempo real
   - Use componente TesteAPI para validar integração

4. **Banco de Dados**:
   - Backup: `cp sistema_extensao.db sistema_extensao.db.backup`
   - Reset: `rm sistema_extensao.db` (recria vazio)

---

## ✅ Checklist Final

Antes de usar em produção:

- [x] Backend funcionando
- [x] Frontend funcionando
- [x] API integrada
- [x] Formulários testados
- [x] Banco de dados verificado
- [x] CORS habilitado
- [x] Documentação completa
- [x] Tratamento de erros
- [ ] Adicionar autenticação
- [ ] Adicionar validação frontend
- [ ] Testes unitários
- [ ] Deploy planejado

---

## 📞 Suporte e Referência

### Comandos Rápidos
```bash
# Backend
cd backend_python && python main.py

# Frontend
cd front/AtvMetodosAPI && npm run dev

# Banco
sqlite3 backend_python/sistema_extensao.db
```

---

## 📄 Licença

Projeto educacional - Licença Livre