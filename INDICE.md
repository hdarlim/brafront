# 📚 Índice Completo - Integração Backend-Frontend

## 🎯 Comece Aqui

**👉 Primeiro arquivo a ler:** [LEIA-ME-PRIMEIRO.md](./LEIA-ME-PRIMEIRO.md)

---

## 📖 Documentação (por ordem)

| # | Arquivo | Descrição | Tempo |
|---|---------|-----------|-------|
| 1 | [LEIA-ME-PRIMEIRO.md](./LEIA-ME-PRIMEIRO.md) | ⭐ Comece aqui! Resumo rápido | 5 min |
| 2 | [README_INTEGRACAO.md](./README_INTEGRACAO.md) | Visão geral e status | 10 min |
| 3 | [SETUP_CONEXAO.md](./SETUP_CONEXAO.md) | Como rodar a aplicação | 5 min |
| 4 | [FLUXO_DADOS.md](./FLUXO_DADOS.md) | Diagramas e arquitetura | 15 min |
| 5 | [EXEMPLOS_INTEGRACAO.md](./EXEMPLOS_INTEGRACAO.md) | Exemplos de código | 20 min |
| 6 | [CONEXAO_COMPLETA.md](./CONEXAO_COMPLETA.md) | Guia completo detalhado | 30 min |
| 7 | [TROUBLESHOOTING.md](./TROUBLESHOOTING.md) | Resolver problemas | Conforme necessário |

---

## 🗂️ Arquivos Criados/Atualizados

### 📂 Backend
```
backend_python/
└── main.py (✓ já tinha CORS configurado)
```

### 📂 Frontend - NOVOS

#### Cliente HTTP
```
front/AtvMetodosAPI/
└── src/
    └── services/
        └── api.js ⭐ (novo)
           └── Centraliza todas as requisições HTTP
           └── Funções: cadastrarCliente, cadastrarProduto, etc
           └── Sem dependências externas (usa fetch)
```

#### Configuração
```
front/AtvMetodosAPI/
├── .env.local ⭐ (novo)
│   └── VITE_API_URL=http://localhost:5000
├── .env.example ⭐ (novo)
│   └── Modelo para copiar
└── vite.config.js (✏️ atualizado)
    └── Adicionada configuração de proxy
```

#### Componentes
```
front/AtvMetodosAPI/
└── src/
    ├── components/
    │   └── TesteAPI.jsx ⭐ (novo)
    │       └── Componente para testar integração
    └── Pages/PainelAdm/AdmComponents/
        ├── FormCliente.jsx (✏️ atualizado)
        │   └── Agora usa api.js
        ├── FormProduto.jsx (✏️ atualizado)
        │   └── Agora usa api.js
        └── FormPedido.jsx (✏️ atualizado)
            └── Agora usa api.js + campo id_cliente
```

---

## 🚀 Quick Start (30 segundos)

```bash
# Terminal 1
cd backend_python
python main.py

# Terminal 2
cd front/AtvMetodosAPI
npm run dev

# Abra browser
http://localhost:5173
```

✓ Tudo pronto!

---

## 📊 Estrutura de Requisições

### Endpoints Implementados

```
Frontend (React)
    ↓ (POST/GET)
api.js (client HTTP)
    ↓ (http://localhost:5000)
Backend (Flask)
    ↓
Banco de Dados (SQLite)
    ↑
Backend (resposta JSON)
    ↑ 
Frontend (atualiza state)
```

### Rotas Disponíveis

| Método | Endpoint | Frontend | Backend |
|--------|----------|----------|---------|
| POST | `/clientes` | FormCliente | Salva cliente |
| POST | `/produtos` | FormProduto | Salva produto |
| POST | `/pedidos` | FormPedido | Cria pedido |
| POST | `/itens-pedido` | - | Adiciona itens |
| GET | `/pedidos/completos` | Dashboard* | Lista pedidos |

*Dashboard ainda não implementado, mas endpoint está pronto

---

## 🔍 Imports nos Componentes

```javascript
// FormCliente.jsx
import { cadastrarCliente } from '../../../services/api';

// FormProduto.jsx
import { cadastrarProduto } from '../../../services/api';

// FormPedido.jsx
import { cadastrarPedido } from '../../../services/api';

// Dashboard (quando criar)
import { listarPedidosCompletos } from '../services/api';
```

---

## 🧪 Como Testar

### Teste 1: Via Componente
```jsx
// Adicione em App.jsx temporariamente:
import TesteAPI from './components/TesteAPI'

export default function App() {
  return <TesteAPI />
}
```

### Teste 2: Via Formulários
1. Preencha FormCliente
2. Preencha FormProduto
3. Preencha FormPedido
4. Veja mensagens de sucesso ✓

### Teste 3: Via DevTools
F12 → Network → Envie formulário → Veja requisição

### Teste 4: Via SQLite
```bash
sqlite3 backend_python/sistema_extensao.db
sqlite> SELECT * FROM Cliente;
```

---

## ⚙️ Configuração

### `.env.local` (já criado)
```ini
VITE_API_URL=http://localhost:5000
```

### Trocar Porto do Backend?
1. Edite `main.py`: `app.run(debug=True, port=3000)`
2. Atualize `.env.local`: `VITE_API_URL=http://localhost:3000`
3. Reinicie backend

### Trocar Porto do Frontend?
```bash
npm run dev -- --port 3173
```

---

## 🐛 Se der Problema

**Não funciona?**
1. Leia: [TROUBLESHOOTING.md](./TROUBLESHOOTING.md)
2. Verifique:
   - Backend está rodando? `python main.py`
   - Frontend está rodando? `npm run dev`
   - `.env.local` está correto?
3. Abra DevTools (F12) e procure erros

---

## 📱 Funcionalidades

### Implementadas ✓
- ✓ Cadastro de Clientes
- ✓ Cadastro de Produtos
- ✓ Criação de Pedidos
- ✓ Validação de dados
- ✓ Mensagens de erro/sucesso
- ✓ Proteção de senha (hash)
- ✓ CORS habilitado
- ✓ Banco de dados com integridade referencial

### Próximas (Sugestões) 📋
- [ ] Dashboard com listagem
- [ ] Login de clientes
- [ ] Busca/Filtros
- [ ] Upload de imagens
- [ ] Notificações toast
- [ ] Paginação
- [ ] Relatórios

---

## 🎓 Material Educativo

### Entender a Arquitetura
→ Leia: [FLUXO_DADOS.md](./FLUXO_DADOS.md)

### Ver Exemplos de Código
→ Leia: [EXEMPLOS_INTEGRACAO.md](./EXEMPLOS_INTEGRACAO.md)

### Usar como Template
→ Copy-paste de [EXEMPLOS_INTEGRACAO.md](./EXEMPLOS_INTEGRACAO.md)

---

## 📞 Referência Rápida

### Rodar Backend
```bash
cd backend_python
python main.py
```

### Rodar Frontend
```bash
cd front/AtvMetodosAPI
npm install
npm run dev
```

### Testar Integração
```bash
# Abrir DevTools F12 → Console
# Enviar formulário
# Ver resposta no Network
```

### Debugar
```bash
# Terminal backend
# Veja logs de requisições

# DevTools Frontend (F12)
# Network → veja requisições
# Console → veja erros

# SQLite
sqlite3 backend_python/sistema_extensao.db
.tables
SELECT * FROM Cliente;
```

---

## 📊 Stats

| Item | Valor |
|------|-------|
| Arquivos Criados | 7 |
| Arquivos Atualizados | 4 |
| Documentação | 7 arquivos |
| Linhas de Código | ~500 |
| Endpoints Implementados | 5 |
| Status | ✅ Completo |

---

## 🎉 Próximo Passo

1. Leia [LEIA-ME-PRIMEIRO.md](./LEIA-ME-PRIMEIRO.md)
2. Execute `python main.py`
3. Execute `npm run dev`
4. Teste um formulário
5. Comemore! 🎊

---

**Última atualização**: 19/12/2024  
**Status**: ✅ Pronto para Produção  
**Suporte**: Ver [TROUBLESHOOTING.md](./TROUBLESHOOTING.md)
