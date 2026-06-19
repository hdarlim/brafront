#!/usr/bin/env markdown
# 🚀 GUIA RÁPIDO - Sistema de Gestão de Marmitas

> **Seu projeto está 100% pronto para usar! Leia este arquivo em 5 minutos.**

---

## ⚡ Comece em 2 Minutos

### Terminal 1 - Backend
```bash
cd backend_python
pip install flask flask-cors werkzeug  # Primeira vez apenas
python main.py
```
✓ Backend pronto em: **http://localhost:5000**

### Terminal 2 - Frontend  
```bash
cd front/AtvMetodosAPI
npm install    # Primeira vez apenas
npm run dev
```
✓ Frontend pronto em: **http://localhost:5173**

### No Navegador
Abra: **http://localhost:5173**

🎉 **Pronto! Teste preenchendo um formulário!**

---

## 📚 Documentação Completa

Todos os arquivos estão na pasta raiz do projeto:

| 📄 Arquivo | ⏱️ Tempo | 📖 Descrição |
|-----------|---------|-------------|
| **README.md** | 20 min | 🌟 **COMECE AQUI** - Guia completo do projeto |
| **FLUXO_DADOS.md** | 15 min | Diagramas e arquitetura |
| **EXEMPLOS_INTEGRACAO.md** | 20 min | Exemplos de código |
| **TROUBLESHOOTING.md** | 15 min | Problemas e soluções |
| **LEIA-ME-PRIMEIRO.md** | 5 min | Resumo rápido |
| **SETUP_CONEXAO.md** | 10 min | Setup passo a passo |
| **CONEXAO_COMPLETA.md** | 30 min | Referência técnica |
| **CHECKLIST.md** | 10 min | Verificação completa |
| **STATUS.txt** | 2 min | Status visual |
| **INDICE.md** | 5 min | Índice de documentação |

**Total**: 📚 **10 arquivos de documentação completa**

---

## ✨ O que o Projeto Faz

Sistema web para gerenciar **clientes, produtos (marmitas) e pedidos**.

### ✅ Funcionalidades Implementadas

✓ **Cadastro de Clientes**
- Nome, email, telefone, endereço
- Senha hasheada com Werkzeug
- Email é único

✓ **Cadastro de Produtos**
- Nome, tipo (Tradicional/Fit/Vegana)
- Descrição de ingredientes
- Sem limite de produtos

✓ **Criação de Pedidos**
- Vinculado a clientes
- Data, status (pendente/preparando/pronto/entregue)
- Total calculado automaticamente

✓ **Gestão de Itens**
- Adicionar produtos aos pedidos
- Quantidade e valor unitário
- Total atualizado automaticamente

✓ **Listagem de Pedidos**
- Todos os pedidos com detalhes
- Nome do cliente + produtos
- Pronto para dashboard

---

## 🔧 Tecnologias

| Layer | Tecnologia | Versão |
|-------|-----------|--------|
| Backend | Python + Flask | 3.x |
| Frontend | React + Vite | 19.x / 8.x |
| Banco | SQLite | 3 |
| API | REST + JSON | - |

---

## 🌐 Endpoints Disponíveis

### POST /clientes
Cadastra um novo cliente
```json
{
  "nome": "João Silva",
  "email": "joao@email.com",
  "telefone": "11999999999",
  "endereco": "Rua A, 123",
  "senha": "senha123"
}
```

### POST /produtos
Cadastra um novo produto
```json
{
  "nome": "Marmita Tradicional",
  "tipo": "Tradicional",
  "descricao": "Arroz, feijão, carne"
}
```

### POST /pedidos
Cria um novo pedido
```json
{
  "id_cliente": 1,
  "data": "2024-12-19",
  "status": "pendente",
  "total": 0
}
```

### POST /itens-pedido
Adiciona item ao pedido
```json
{
  "id_pedido": 1,
  "id_produto": 1,
  "qtd_pedido": 2,
  "valor_unitario": 15.50
}
```

### GET /pedidos/completos
Retorna todos os pedidos com detalhes

---

## 📁 Estrutura do Projeto

```
brafront/
├── backend_python/
│   └── main.py                 ← Aplicação Flask
│
├── front/AtvMetodosAPI/
│   ├── .env.local              ← Configuração
│   ├── src/
│   │   ├── services/api.js     ← Client HTTP ⭐
│   │   └── Pages/.../
│   │       └── AdmComponents/
│   │           ├── FormCliente.jsx
│   │           ├── FormProduto.jsx
│   │           └── FormPedido.jsx
│   └── package.json
│
└── [Toda a documentação está aqui na raiz]
    ├── README.md
    ├── FLUXO_DADOS.md
    ├── EXEMPLOS_INTEGRACAO.md
    └── ...
```

---

## 🧪 Testando a Integração

### Teste 1: Formulário (Manual)
1. Abra http://localhost:5173
2. Preencha "Cadastrar Cliente"
3. Clique em "Salvar"
4. Veja: ✓ Cliente cadastrado com sucesso!

### Teste 2: DevTools (Desenvolvedor)
```
1. F12 → Network
2. Preencha e envie formulário
3. Veja a requisição HTTP
4. Veja Response em JSON
```

### Teste 3: Banco de Dados
```bash
sqlite3 backend_python/sistema_extensao.db
SELECT * FROM Cliente;
```

---

## ⚙️ Configuração

### .env.local
```
VITE_API_URL=http://localhost:5000
```

Se o backend estiver em outra porta:
1. Mude `app.run(debug=True, port=3000)` em `main.py`
2. Atualize `.env.local` com a nova porta
3. Reinicie backend

---

## 🐛 Erros Comuns?

| ❌ Erro | ✅ Solução |
|--------|----------|
| "Failed to fetch" | Backend não está rodando: `python main.py` |
| "Email já existe" | Use um email diferente |
| "CORS error" | Backend já tem CORS ✓ |
| Banco vazio | Reinicie backend |

👉 **Mais em**: [TROUBLESHOOTING.md](./TROUBLESHOOTING.md)

---

## 📊 Como Funciona (Fluxo)

```
1. Usuário preenche formulário (FormCliente)
                ↓
2. Clica "Salvar Cliente"
                ↓
3. handleSubmit() é executado
                ↓
4. api.js faz fetch POST /clientes
                ↓
5. Backend recebe e valida dados
                ↓
6. Backend insere no SQLite
                ↓
7. Backend retorna JSON
                ↓
8. Component atualiza estado
                ↓
9. Usuário vê mensagem de sucesso ✓
```

---

## 🎯 Próximas Features

### Fáceis (1-2 horas)
- [ ] Adicionar busca de clientes
- [ ] Filtro por status de pedido
- [ ] Listar pedidos em um dashboard

### Médias (4-8 horas)
- [ ] Login de clientes
- [ ] Editar e deletar dados
- [ ] Upload de imagens

### Complexas (1-2 dias)
- [ ] Dashboard com gráficos
- [ ] Pagamento online (Stripe/PayPal)
- [ ] Notificações por email

---

## 💡 Exemplos de Uso

### Adicionar um novo formulário

1. Criar componente React
2. Adicionar função em `src/services/api.js`
3. Chamar função no `handleSubmit`
4. Testar com DevTools

👉 Ver: [EXEMPLOS_INTEGRACAO.md](./EXEMPLOS_INTEGRACAO.md)

### Adicionar um novo endpoint

1. Criar rota em `main.py`
2. Adicionar função em `api.js`
3. Importar no componente
4. Testar

👉 Ver: [README.md - Endpoints](./README.md#-endpoints-da-api)

---

## 📞 Precisa de Ajuda?

1. **Para rodar**: [README.md - Quick Start](./README.md#-quick-start)
2. **Para entender**: [FLUXO_DADOS.md](./FLUXO_DADOS.md)
3. **Para codificar**: [EXEMPLOS_INTEGRACAO.md](./EXEMPLOS_INTEGRACAO.md)
4. **Para debugar**: [TROUBLESHOOTING.md](./TROUBLESHOOTING.md)
5. **Para tudo**: [README.md](./README.md)

---

## ✅ Checklist Antes de Usar

- [x] Backend instalado
- [x] Frontend instalado
- [x] Integração configurada
- [x] Formulários funcionando
- [x] Banco de dados pronto
- [x] Documentação completa
- [ ] Você testou um formulário?

**Próximo passo**: Teste agora!

---

## 🎉 Status Final

| Item | Status |
|------|--------|
| Backend | ✅ Pronto |
| Frontend | ✅ Pronto |
| Integração | ✅ Pronto |
| Documentação | ✅ Completa |
| **TUDO** | ✅ **PRONTO PARA USAR** |

---

## 📖 Leitura Recomendada

**Próximas 30 minutos**:
1. Rodar a aplicação (2 min)
2. Ler [README.md](./README.md) (20 min)
3. Testar um formulário (5 min)
4. Entender com [FLUXO_DADOS.md](./FLUXO_DADOS.md) (15 min)

**Depois**:
- Ver exemplos: [EXEMPLOS_INTEGRACAO.md](./EXEMPLOS_INTEGRACAO.md)
- Fazer mudanças no código
- Adicionar novas features

---

**Criado em**: 19/12/2024  
**Status**: ✅ Completo e Testado  
**Tempo de leitura**: 5 minutos  

🚀 **Bom desenvolvimento!**
