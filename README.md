# 🍜 Sistema de Gestão de Marmitas - Integração Backend-Frontend

> **Status**: ✅ Conexão Backend-Frontend **COMPLETA**

## 🎯 O que é este projeto?

Sistema web para gerenciar clientes, produtos (marmitas) e pedidos em tempo real.

- **Backend**: Python + Flask + SQLite
- **Frontend**: React + Vite + JavaScript
- **API**: RESTful com CORS habilitado

---

## 🚀 Comece Agora (30 segundos)

### Terminal 1 - Backend
```bash
cd backend_python
python main.py
```
Backend rodará em: **http://localhost:5000**

### Terminal 2 - Frontend
```bash
cd front/AtvMetodosAPI
npm run dev
```
Frontend rodará em: **http://localhost:5173**

### Pronto! 🎉
Abra no navegador: **http://localhost:5173**

---

## 📖 Documentação Rápida

| Arquivo | Descrição |
|---------|-----------|
| [LEIA-ME-PRIMEIRO.md](./LEIA-ME-PRIMEIRO.md) | ⭐ **Comece aqui** (5 min) |
| [README_INTEGRACAO.md](./README_INTEGRACAO.md) | Visão geral (10 min) |
| [SETUP_CONEXAO.md](./SETUP_CONEXAO.md) | Como rodar (5 min) |
| [FLUXO_DADOS.md](./FLUXO_DADOS.md) | Arquitetura (15 min) |
| [EXEMPLOS_INTEGRACAO.md](./EXEMPLOS_INTEGRACAO.md) | Exemplos de código (20 min) |
| [TROUBLESHOOTING.md](./TROUBLESHOOTING.md) | Resolver problemas |
| [STATUS.txt](./STATUS.txt) | Status visual rápido |

---

## 🌐 Funcionalidades

### ✅ Implementado
- ✓ Cadastro de clientes com hash de senha
- ✓ Cadastro de produtos (marmitas)
- ✓ Criação de pedidos
- ✓ Adição de itens aos pedidos
- ✓ Listagem de pedidos com detalhes
- ✓ Validação de dados
- ✓ Mensagens de feedback (sucesso/erro)
- ✓ CORS habilitado
- ✓ Banco de dados com integridade referencial

### 📋 Sugestões
- [ ] Dashboard com gráficos
- [ ] Login de clientes
- [ ] Busca e filtros
- [ ] Upload de imagens
- [ ] Pagamento online
- [ ] Relatórios em PDF

---

## 📁 Estrutura de Pastas

```
brafront/
├── backend_python/
│   └── main.py                 (Flask API)
│
├── front/AtvMetodosAPI/
│   ├── .env.local              (Configuração)
│   ├── src/
│   │   ├── services/
│   │   │   └── api.js          (Client HTTP)
│   │   ├── components/
│   │   │   └── TesteAPI.jsx    (Teste integração)
│   │   └── Pages/.../
│   │       └── AdmComponents/
│   │           ├── FormCliente.jsx
│   │           ├── FormProduto.jsx
│   │           └── FormPedido.jsx
│   └── package.json
│
└── Documentação/
    ├── LEIA-ME-PRIMEIRO.md
    ├── README_INTEGRACAO.md
    ├── SETUP_CONEXAO.md
    ├── FLUXO_DADOS.md
    ├── EXEMPLOS_INTEGRACAO.md
    ├── TROUBLESHOOTING.md
    ├── CHECKLIST.md
    ├── INDICE.md
    └── STATUS.txt
```

---

## 🔌 Integração Backend-Frontend

```
React Form (Frontend)
        ↓
api.js (Client HTTP)
        ↓ (POST/GET JSON)
Flask Routes (Backend)
        ↓
SQLite Database
        ↑
Flask Response (JSON)
        ↑
Component State
```

---

## 📡 Endpoints Disponíveis

```javascript
// Frontend pode usar:
import { 
  cadastrarCliente,
  cadastrarProduto,
  cadastrarPedido,
  adicionarItemPedido,
  listarPedidosCompletos 
} from './services/api';
```

| Rota | Método | Descrição |
|------|--------|-----------|
| `/clientes` | POST | Cadastrar novo cliente |
| `/produtos` | POST | Cadastrar novo produto |
| `/pedidos` | POST | Criar novo pedido |
| `/itens-pedido` | POST | Adicionar item ao pedido |
| `/pedidos/completos` | GET | Listar todos os pedidos |

---

## ⚙️ Configuração

### .env.local (já criado)
```
VITE_API_URL=http://localhost:5000
```

Se o backend estiver em outra porta, atualize aqui.

---

## 🧪 Testar Integração

### Teste 1: Via Formulário
1. Abra http://localhost:5173
2. Preencha "Cadastrar Cliente"
3. Clique em "Salvar"
4. Veja mensagem ✓

### Teste 2: Via DevTools
1. F12 → Network
2. Envie formulário
3. Veja requisição HTTP
4. Verifique resposta JSON

### Teste 3: Via SQLite
```bash
sqlite3 backend_python/sistema_extensao.db
SELECT * FROM Cliente;
```

---

## 🐛 Problemas?

| Erro | Solução |
|------|---------|
| "Failed to fetch" | Backend não está rodando: `python main.py` |
| "CORS error" | CORS já está habilitado ✓ |
| "Email já cadastrado" | Use um email diferente |
| Banco vazio | Reinicie backend: `Ctrl+C` → `python main.py` |

👉 Mais em [TROUBLESHOOTING.md](./TROUBLESHOOTING.md)

---

## 🎓 Como Contribuir

1. Leia a documentação
2. Entenda a arquitetura (ver [FLUXO_DADOS.md](./FLUXO_DADOS.md))
3. Veja exemplos ([EXEMPLOS_INTEGRACAO.md](./EXEMPLOS_INTEGRACAO.md))
4. Faça suas mudanças
5. Teste tudo

---

## 📊 Stats

| Item | Valor |
|------|-------|
| Arquivos criados | 7 |
| Arquivos atualizados | 4 |
| Endpoints implementados | 5 |
| Documentação | 9 arquivos |
| Status | ✅ Pronto |

---

## 🎯 Próximos Passos

1. **Ler documentação**: [LEIA-ME-PRIMEIRO.md](./LEIA-ME-PRIMEIRO.md)
2. **Rodar aplicação**: Seguir "Comece Agora" acima
3. **Testar integração**: Enviar formulário
4. **Explorar código**: Ver [EXEMPLOS_INTEGRACAO.md](./EXEMPLOS_INTEGRACAO.md)
5. **Adicionar features**: Dashboard, Login, etc.

---

## 📞 Referência Rápida

```bash
# Backend
cd backend_python && python main.py

# Frontend
cd front/AtvMetodosAPI && npm run dev

# Testar Banco
sqlite3 backend_python/sistema_extensao.db "SELECT * FROM Cliente;"

# Ver logs (em terminal do backend)
# (Veja requisições HTTP em tempo real)
```

---

## ✅ Checklist de Verificação

- [x] Backend funcionando
- [x] Frontend funcionando
- [x] API client criado
- [x] Formulários integrados
- [x] Banco de dados pronto
- [x] CORS configurado
- [x] Documentação completa
- [x] Componente de teste
- [x] Guia de troubleshooting
- [x] Exemplos de código

🎉 **Tudo pronto para usar!**

---

## 📄 Licença

Projeto educacional - Use livremente

---

## 👥 Autores

Desenvolvido para aplicação de Gestão de Marmitas

---

**Última atualização**: 19/12/2024  
**Versão**: 1.0  
**Status**: ✅ Integração Completa

👉 **Comece pelo arquivo [LEIA-ME-PRIMEIRO.md](./LEIA-ME-PRIMEIRO.md)**
