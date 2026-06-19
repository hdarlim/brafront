# 🔌 Conexão Backend-Frontend Configurada

A conexão entre backend (Flask) e frontend (React) foi configurada com sucesso!

## 📋 Como Rodar a Aplicação

### 1️⃣ **Backend (Python Flask)**

No terminal, navegue até a pasta `backend_python/`:

```bash
cd backend_python
python main.py
```

O backend iniciará em: **http://localhost:5000**

### 2️⃣ **Frontend (React + Vite)**

Em outro terminal, navegue até `front/AtvMetodosAPI/`:

```bash
cd front/AtvMetodosAPI
npm install    # Primeira vez apenas
npm run dev
```

O frontend iniciará em: **http://localhost:5173** (padrão Vite)

---

## 🔄 Fluxo de Comunicação

### 📤 Requisições Disponíveis

| Formulário | Método | Endpoint | Descrição |
|-----------|--------|----------|-----------|
| FormCliente | POST | `/clientes` | Cadastra novo cliente |
| FormProduto | POST | `/produtos` | Cadastra novo produto |
| FormPedido | POST | `/pedidos` | Cria novo pedido |
| - | POST | `/itens-pedido` | Adiciona itens ao pedido |
| Dashboard | GET | `/pedidos/completos` | Lista todos os pedidos com detalhes |

---

## ⚙️ Configuração de Variáveis de Ambiente

No arquivo `.env.local` (já criado):

```
VITE_API_URL=http://localhost:5000
```

Se o backend estiver em outra porta/host, atualize esta variável.

---

## 📁 Estrutura de Arquivos da Integração

```
front/AtvMetodosAPI/
├── .env.local                    # Variáveis de ambiente (não commitar)
├── .env.example                  # Exemplo de configuração
├── src/
│   ├── services/
│   │   └── api.js               # 🔑 Cliente HTTP centralizado
│   └── Pages/PainelAdm/AdmComponents/
│       ├── FormCliente.jsx      # Atualizado
│       ├── FormProduto.jsx      # Atualizado
│       └── FormPedido.jsx       # Atualizado
```

---

## ✅ Testes de Funcionamento

### 1. Testar Cadastro de Cliente

1. Acesse o frontend em `http://localhost:5173`
2. Preencha o formulário "Cadastrar Cliente"
3. Clique em "Salvar Cliente"
4. Deve aparecer mensagem de sucesso: ✓ Cliente cadastrado com sucesso!

### 2. Testar Cadastro de Produto

1. Preencha o formulário "Cadastrar Produto"
2. Clique em "Salvar Produto"
3. Deve aparecer mensagem de sucesso: ✓ Produto cadastrado com sucesso!

### 3. Testar Cadastro de Pedido

1. Preencha o formulário "Registrar Novo Pedido" com:
   - ID de um cliente existente
   - Data do pedido
   - Status (ex: "pendente")
   - Total
2. Clique em "Gerar Pedido"
3. Deve aparecer mensagem de sucesso: ✓ Pedido registrado com sucesso!

---

## 🐛 Troubleshooting

### ❌ "Erro: Failed to fetch"

**Causa**: Backend não está rodando ou URL está incorreta

**Solução**:
1. Verifique se `python main.py` está rodando (terminal separado)
2. Confirme que está em `http://localhost:5000`
3. Verifique `.env.local` se `VITE_API_URL` está correto

### ❌ "CORS error"

**Causa**: Backend pode estar bloqueando requisições

**Solução**: 
- Verificar se `CORS(app)` está no `main.py` (já está configurado ✓)

### ❌ Mensagens de erro do servidor

Verifique o console do backend (terminal onde rodou `python main.py`) para ver logs de erro

---

## 🔧 Próximos Passos (Opcionais)

1. **Autenticação**: Implementar login de clientes
2. **Dashboard**: Exibir listagem de pedidos usando `GET /pedidos/completos`
3. **Validação**: Adicionar validação no frontend antes de enviar
4. **Upload de Imagens**: Adicionar suporte para fotos de produtos
5. **Notificações**: Implementar toast notifications para melhor UX

---

## 📝 Resumo das Mudanças

✅ Criado `src/services/api.js` - Cliente HTTP centralizado  
✅ Atualizado `FormCliente.jsx` - Integrado com API  
✅ Atualizado `FormProduto.jsx` - Integrado com API  
✅ Atualizado `FormPedido.jsx` - Integrado com API  
✅ Criado `.env.local` - Configuração de variáveis  
✅ Criado `.env.example` - Modelo para `.env.local`  

Backend já tinha CORS configurado! ✓
