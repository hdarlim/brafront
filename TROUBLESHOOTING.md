# 🔧 Troubleshooting - Guia de Resolução de Problemas

## 🚨 Problemas Comuns e Soluções

---

### ❌ Erro: "Failed to fetch"

**Descrição**: Aparece no console do navegador quando tenta enviar um formulário

**Causas Possíveis**:
1. Backend não está rodando
2. URL está incorreta
3. Porta está bloqueada
4. Firewall está bloqueando

**Como Resolver**:

```bash
# 1. Verifique se backend está rodando
# Terminal 1:
cd backend_python
python main.py

# Deveria aparecer:
# WARNING in app.run() is not recommended ...
# * Running on http://127.0.0.1:5000
```

Se não aparecer isso, backend NÃO está rodando.

```bash
# 2. Verifique se porta 5000 está em uso
lsof -i :5000

# Se houver algo rodando, mate o processo:
kill -9 <PID>

# Depois tente novamente
python main.py
```

```bash
# 3. Verifique .env.local
cat front/AtvMetodosAPI/.env.local

# Deveria ter:
# VITE_API_URL=http://localhost:5000
```

Se estiver diferente, atualize.

---

### ❌ Erro: "CORS error" ou "blocked by CORS policy"

**Descrição**: Aviso no console sobre CORS

**Solução**: 
Verifique se `CORS(app)` está em `main.py`:

```python
from flask_cors import CORS

app = Flask(__name__)
CORS(app)  # ← Deve estar aqui
```

Se não estiver, adicione e reinicie o backend.

---

### ❌ Erro: "json.decoder.JSONDecodeError"

**Descrição**: Erro ao processar resposta JSON

**Causas**: 
- Backend retornou HTML em vez de JSON (erro 404 ou 500)
- Endpoint não existe

**Solução**:

```javascript
// Verifique no DevTools → Network qual URL está sendo chamada
// Ex: http://localhost:5000/clientes

// Veja se o endpoint existe em main.py
# Procure por @app.route('/clientes', methods=['POST'])
```

Se não encontrar, o endpoint não está implementado.

---

### ❌ "Email já cadastrado" ou "IntegrityError"

**Descrição**: Erro ao tentar cadastrar cliente com email que já existe

**Solução**:
Use um email diferente a cada teste:

```javascript
// Em FormCliente.jsx ou no browser console:
const email = `teste${Date.now()}@email.com`; // Sempre único

// Ou use um email genuinamente diferente
```

---

### ❌ "TypeError: Cannot read property 'statusCode'"

**Descrição**: Erro no manipulador de respostas

**Causa**: Response não é um objeto válido

**Solução**:
Verifique que o backend está retornando JSON válido:

```python
# Em main.py, verifique que TODAS as rotas retornam jsonify()
return jsonify({"mensagem": "..."}), 201  # ✓ Correto
# return {"mensagem": "..."}, 201          # ✗ Errado
```

---

### ❌ "Pedido não encontrado" ou "Cliente não existe"

**Descrição**: FormPedido não consegue criar pedido

**Causa**: ID do cliente não existe no banco de dados

**Solução**:
1. Primeiro cadastre um cliente (use FormCliente)
2. Anote o ID retornado (aparece na mensagem de sucesso)
3. Use esse ID no FormPedido

Ou use o SQLite para verificar:

```bash
sqlite3 backend_python/sistema_extensao.db
sqlite> SELECT id_cliente, nome FROM Cliente;

# Você verá algo como:
# 1 | João Silva
# 2 | Maria Santos
```

---

### ❌ "Port 5000 is already in use"

**Descrição**: Não consegue iniciar o backend

**Solução**:

```bash
# Opção 1: Matar processo que está usando porta 5000
lsof -i :5000
# Pega o PID (ex: 12345)
kill -9 12345

# Opção 2: Usar porta diferente
# Em main.py, mude:
# app.run(debug=True, port=3000)  # Nova porta

# E atualize .env.local:
# VITE_API_URL=http://localhost:3000
```

---

### ❌ "ModuleNotFoundError: No module named 'flask'"

**Descrição**: Biblioteca Flask não está instalada

**Solução**:

```bash
# Instale as dependências
pip install flask flask-cors werkzeug

# Ou crie um ambiente virtual (recomendado)
python -m venv venv
source venv/bin/activate  # Linux/Mac
# ou
venv\Scripts\activate     # Windows

# Instale as dependências
pip install flask flask-cors werkzeug
```

---

### ❌ "No module named 'sqlite3'"

**Descrição**: SQLite não está disponível (raro)

**Solução**:
SQLite3 vem com Python. Se não tiver, reinstale Python.

---

### ❌ "npm ERR! code ERESOLVE"

**Descrição**: Erro ao instalar dependências do frontend

**Solução**:

```bash
cd front/AtvMetodosAPI

# Limpe cache e tente novamente
npm cache clean --force
npm install

# Se persistir, force instalação:
npm install --legacy-peer-deps
```

---

### ❌ "Cannot find module 'react'" após npm install

**Descrição**: Dependências não instaladas corretamente

**Solução**:

```bash
# Delete node_modules e package-lock.json
rm -rf node_modules
rm package-lock.json

# Reinstale
npm install

# Depois rode:
npm run dev
```

---

### ❌ "Formulário enviado mas nada acontece"

**Descrição**: Clica em enviar, mas não vê mensagem de sucesso ou erro

**Solução**:
Abra DevTools (F12) → Console e procure por erros.

Se vir erros, siga as soluções acima.

Se não vir nada, adicione logs:

```javascript
// Em api.js, adicione console.log:
async function apiRequest(endpoint, method = 'GET', data = null) {
  console.log(`📤 Requisição: ${method} ${endpoint}`, data);
  
  try {
    const response = await fetch(`${API_BASE_URL}${endpoint}`, options);
    console.log(`📥 Resposta:`, response);
    // ... resto do código
  }
}
```

---

### ❌ "Banco de dados vazio ou não inicializado"

**Descrição**: FormCliente foi criado mas não vê dados

**Solução**:
Verifique se `inicializar_banco()` foi executado:

```bash
# Em main.py, verifique que tem:
if __name__ == '__main__':
    inicializar_banco()  # ← Deve estar aqui
    app.run(debug=True)
```

Se não tiver, adicione.

Ou delete e deixe recriar:

```bash
rm backend_python/sistema_extensao.db
python backend_python/main.py  # Vai recriar
```

---

### ❌ "Mudei um arquivo mas não vejo mudança"

**Descrição**: Alterou código mas efeito não aparece

**Solução**:

```bash
# Frontend: Às vezes precisa recarregar manualmente
# DevTools → Network → "Disable Cache" enquanto está aberto

# Backend: Flask relança automaticamente em debug=True
# Se não relançar, reinicie:
# Ctrl+C
# python main.py

# Limpe cache do navegador:
# DevTools → F12 → Settings → Network → Desabilite cache
```

---

## 📊 Checklist de Verificação

Use este checklist quando tiver problemas:

- [ ] Backend está rodando? (`python main.py`)
- [ ] Backend está em `http://localhost:5000`?
- [ ] `.env.local` tem `VITE_API_URL=http://localhost:5000`?
- [ ] Frontend está rodando? (`npm run dev`)
- [ ] DevTools console mostra erros? (F12)
- [ ] Network tab mostra requisição? (F12 → Network)
- [ ] Resposta da requisição é JSON válido?
- [ ] Banco de dados foi inicializado? (`sistema_extensao.db` existe?)
- [ ] CORS está habilitado em `main.py`? (`CORS(app)`)

---

## 🔍 Como Debugar Requisições

### Via DevTools do Navegador

1. Abra `http://localhost:5173`
2. Pressione `F12` (DevTools)
3. Vá para aba `Network`
4. Preencha e envie um formulário
5. Veja a requisição na aba Network
6. Clique nela para ver detalhes:
   - Request (dados enviados)
   - Response (resposta do servidor)
   - Status code (201 = sucesso, 400 = erro, 500 = erro servidor)

### Via Logs do Backend

1. Terminal onde rodou `python main.py`
2. Verá logs de cada requisição:
   ```
   127.0.0.1 - - [19/Dec/2024 10:00:00] "POST /clientes HTTP/1.1" 201 -
   ```

### Via SQLite CLI

```bash
# Abra banco de dados
sqlite3 backend_python/sistema_extensao.db

# Veja dados
sqlite> SELECT * FROM Cliente;
sqlite> SELECT * FROM Produto;
sqlite> SELECT * FROM Pedido;
sqlite> SELECT * FROM Item_Pedido;

# Saia
sqlite> .quit
```

---

## 📞 Ainda com Dúvidas?

1. Verifique a documentação:
   - `SETUP_CONEXAO.md` - Como rodar
   - `EXEMPLOS_INTEGRACAO.md` - Exemplos de código
   - `CONEXAO_COMPLETA.md` - Guia completo
   - `FLUXO_DADOS.md` - Arquitetura

2. Procure erros no:
   - Console do navegador (F12)
   - Terminal do backend
   - arquivo `sistema_extensao.db`

3. Verifique os arquivos:
   - `.env.local` (variáveis corretas?)
   - `src/services/api.js` (sintaxe correta?)
   - `main.py` (CORS habilitado?)

---

**Última atualização**: 19/12/2024
**Última resolução testada**: Conexão backend-frontend ✓
