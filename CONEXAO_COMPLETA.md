# 🚀 Guia Completo de Conexão Backend-Frontend

## ✅ O que foi implementado

### 1. **Cliente HTTP Centralizado** (`src/services/api.js`)
- Todas as requisições HTTP passam por um único ponto
- Configuração única de URL base
- Tratamento de erros consistente
- Fácil de manter e estender

### 2. **Formulários Integrados**
- **FormCliente.jsx**: Cadastra clientes no backend
- **FormProduto.jsx**: Cadastra produtos no backend
- **FormPedido.jsx**: Cria pedidos no backend
- Todos com feedback visual (loading, sucesso, erro)

### 3. **Variáveis de Ambiente**
- `.env.local`: Configuração local (gitignored)
- `.env.example`: Modelo para referência
- `VITE_API_URL`: URL configurável da API

---

## 🔍 Endpoints Disponíveis

### Clientes
```javascript
import { cadastrarCliente } from '../services/api';

// Cadastrar cliente
await cadastrarCliente({
  nome: 'João Silva',
  email: 'joao@email.com',
  telefone: '11999999999',
  endereco: 'Rua A, 123',
  senha: 'senha123'
});
```

### Produtos
```javascript
import { cadastrarProduto } from '../services/api';

// Cadastrar produto
await cadastrarProduto({
  nome: 'Marmita Premium',
  tipo: 'Tradicional',
  descricao: 'Arroz, feijão, carne e legumes'
});
```

### Pedidos
```javascript
import { 
  cadastrarPedido, 
  adicionarItemPedido, 
  listarPedidosCompletos 
} from '../services/api';

// Criar pedido
const pedido = await cadastrarPedido({
  id_cliente: 1,
  data: '2026-06-19',
  status: 'pendente',
  total: 0
});

// Adicionar item ao pedido
await adicionarItemPedido({
  id_pedido: pedido.id_pedido,
  id_produto: 1,
  qtd_pedido: 2,
  valor_unitario: 15.50
});

// Listar todos os pedidos
const pedidos = await listarPedidosCompletos();
```

---

## 🛠️ Próximas Implementações Sugeridas

### 1. **Dashboard com Listagem de Pedidos**
```javascript
// Criar um novo componente Dashboard.jsx que use:
import { listarPedidosCompletos } from '../services/api';

// Exibir lista de pedidos com detalhes dos clientes e produtos
```

### 2. **Autenticação de Cliente**
```javascript
// Adicionar em src/services/api.js:
export const login = (email, senha) => {
  return apiRequest('/login', 'POST', { email, senha });
};

// Criar componente LoginCliente.jsx
```

### 3. **CRUD Completo**
```javascript
// Adicionar em src/services/api.js:
export const buscarClientePorId = (id) => {
  return apiRequest(`/clientes/${id}`, 'GET');
};

export const atualizarCliente = (id, dados) => {
  return apiRequest(`/clientes/${id}`, 'PUT', dados);
};

export const deletarCliente = (id) => {
  return apiRequest(`/clientes/${id}`, 'DELETE');
};
```

### 4. **Paginação**
```javascript
export const listarPedidos = (page = 1, limit = 10) => {
  return apiRequest(`/pedidos?page=${page}&limit=${limit}`, 'GET');
};
```

### 5. **Filtros e Busca**
```javascript
export const buscarPedidosPorCliente = (id_cliente) => {
  return apiRequest(`/pedidos?cliente=${id_cliente}`, 'GET');
};

export const buscarPedidosPorStatus = (status) => {
  return apiRequest(`/pedidos?status=${status}`, 'GET');
};
```

---

## 📦 Dependências do Frontend

Atual (em `package.json`):
```json
{
  "react": "^19.2.6",
  "react-dom": "^19.2.6"
}
```

Opcionais recomendados:
```bash
# Para melhorar notificações
npm install react-hot-toast

# Para requisições mais simples (alternativa ao fetch)
npm install axios

# Para gerenciamento de estado
npm install zustand

# Para formulários mais robustos
npm install react-hook-form
```

---

## 🔐 Segurança - Itens a Considerar

1. **Validação Frontend**: Validar dados antes de enviar
2. **Validação Backend**: Já está implementada! ✓
3. **Autenticação**: Implementar login/token JWT
4. **HTTPS**: Usar em produção
5. **CORS**: Já está configurado corretamente ✓
6. **Senha**: Já está usando hash (werkzeug) ✓

---

## 🚀 Deploy

### Backend (Flask)
```bash
# Produção - usar Gunicorn
pip install gunicorn
gunicorn main:app
```

### Frontend (React)
```bash
# Build para produção
npm run build

# Servir com um servidor HTTP
# (pode usar GitHub Pages, Vercel, Netlify, etc)
```

---

## 📝 Estrutura Final do Projeto

```
brafront/
├── backend_python/
│   └── main.py                          # Flask API
├── front/AtvMetodosAPI/
│   ├── .env.local                       # ⭐ Variáveis de ambiente
│   ├── .env.example                     # ⭐ Modelo
│   ├── src/
│   │   ├── services/
│   │   │   └── api.js                   # ⭐ Cliente HTTP
│   │   └── Pages/PainelAdm/AdmComponents/
│   │       ├── FormCliente.jsx          # ⭐ Atualizado
│   │       ├── FormProduto.jsx          # ⭐ Atualizado
│   │       └── FormPedido.jsx           # ⭐ Atualizado
│   └── vite.config.js
├── SETUP_CONEXAO.md                     # ⭐ Este arquivo
└── EXEMPLOS_INTEGRACAO.md               # ⭐ Exemplos

⭐ = Novo ou Atualizado
```

---

## ❓ Perguntas Frequentes

### P: Como mudar a porta do backend?
**R**: Atualize em `main.py`:
```python
app.run(debug=True, port=3000)
```
E em `.env.local`:
```
VITE_API_URL=http://localhost:3000
```

### P: Como debugar requisições?
**R**: Abra DevTools (F12) → Network → veja as requisições HTTP

### P: Posso usar Postman para testar a API?
**R**: Sim! Importe os endpoints em Postman ou Insomnia

### P: Como adicionar mais campos no formulário?
**R**: 
1. Adicione o campo no `formData` (useState)
2. Adicione um `<input>` no form
3. Atualize a chamada para a API se necessário no backend

---

## 📞 Suporte

Se encontrar problemas:
1. Verifique se backend está rodando: `python main.py`
2. Verifique se frontend está rodando: `npm run dev`
3. Abra console do navegador (F12) para ver erros
4. Verifique logs do backend no terminal
5. Confirme `.env.local` com URL correta

---

**Criado em**: 19/06/2026
**Status**: ✅ Backend e Frontend Conectados
