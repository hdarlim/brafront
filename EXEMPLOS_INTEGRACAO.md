/**
 * EXEMPLO: Como usar o cliente de API em novos componentes
 * 
 * Este arquivo mostra exemplos práticos de como integrar a API
 * em seus componentes React
 */

// ============================================
// EXEMPLO 1: Simples Form (como os atuais)
// ============================================
import { useState } from 'react';
import { cadastrarCliente } from '../services/api';

function ExemploForm() {
  const [formData, setFormData] = useState({ nome: '', email: '' });
  const [status, setStatus] = useState('idle');
  const [error, setError] = useState('');

  const handleChange = (e) => {
    setFormData(prev => ({ ...prev, [e.target.name]: e.target.value }));
  };

  const handleSubmit = async (e) => {
    e.preventDefault();
    setStatus('loading');
    try {
      const response = await cadastrarCliente(formData);
      setStatus('success');
      console.log('Cliente criado:', response);
    } catch (err) {
      setStatus('error');
      setError(err.message);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input name="nome" value={formData.nome} onChange={handleChange} />
      <button disabled={status === 'loading'}>
        {status === 'loading' ? 'Salvando...' : 'Salvar'}
      </button>
      {error && <p style={{color: 'red'}}>{error}</p>}
    </form>
  );
}

// ============================================
// EXEMPLO 2: Hook customizado React (useApi)
// ============================================
function useApi(apiFn) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  const execute = async (...args) => {
    setLoading(true);
    setError(null);
    try {
      const response = await apiFn(...args);
      setData(response);
      return response;
    } catch (err) {
      setError(err.message);
      throw err;
    } finally {
      setLoading(false);
    }
  };

  return { data, loading, error, execute };
}

// Uso do hook:
// const { data, loading, error, execute } = useApi(cadastrarCliente);
// const handleSubmit = async (cliente) => {
//   await execute(cliente);
// };

// ============================================
// EXEMPLO 3: Dashboard com listagem
// ============================================
import { useEffect } from 'react';
import { listarPedidosCompletos } from '../services/api';

function DashboardPedidos() {
  const [pedidos, setPedidos] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const carregarPedidos = async () => {
      try {
        const data = await listarPedidosCompletos();
        setPedidos(data);
      } catch (err) {
        console.error('Erro ao carregar pedidos:', err);
      } finally {
        setLoading(false);
      }
    };

    carregarPedidos();
  }, []);

  if (loading) return <p>Carregando...</p>;

  return (
    <div>
      <h2>Pedidos</h2>
      {pedidos.map(pedido => (
        <div key={pedido.id_pedido}>
          <p>Cliente: {pedido.nome_cliente}</p>
          <p>Total: R$ {pedido.total}</p>
          <p>Status: {pedido.status}</p>
          <ul>
            {pedido.itens?.map((item, idx) => (
              <li key={idx}>
                {item.nome_produto} x{item.qtd_pedido}
              </li>
            ))}
          </ul>
        </div>
      ))}
    </div>
  );
}

// ============================================
// EXEMPLO 4: Adicionar novo método à API
// ============================================
/*
Se precisar adicionar um novo endpoint, abra src/services/api.js e adicione:

// Exemplo: buscar cliente por ID
export const buscarClientePorId = (id) => {
  return apiRequest(`/clientes/${id}`, 'GET');
};

// Exemplo: atualizar cliente
export const atualizarCliente = (id, clienteData) => {
  return apiRequest(`/clientes/${id}`, 'PUT', clienteData);
};

// Exemplo: deletar cliente
export const deletarCliente = (id) => {
  return apiRequest(`/clientes/${id}`, 'DELETE');
};
*/

// ============================================
// EXEMPLO 5: Tratamento de erro global
// ============================================
/*
Se quiser um tratamento centralizado de erros, 
atualize o apiRequest em src/services/api.js:

async function apiRequest(endpoint, method = 'GET', data = null) {
  const options = {
    method,
    headers: { 'Content-Type': 'application/json' },
  };

  if (data && (method === 'POST' || method === 'PUT')) {
    options.body = JSON.stringify(data);
  }

  try {
    const response = await fetch(`${API_BASE_URL}${endpoint}`, options);
    
    if (!response.ok) {
      const errorData = await response.json();
      
      // Tratamento específico por código de status
      if (response.status === 401) {
        // Redirecionar para login
        window.location.href = '/login';
      }
      
      throw new Error(errorData.erro || `Erro ${response.status}`);
    }

    return await response.json();
  } catch (error) {
    console.error('Erro na API:', error);
    throw error;
  }
}
*/

// ============================================
// EXEMPLO 6: Toast Notifications (opcional)
// ============================================
/*
Para melhorar a UX, adicione uma biblioteca como 'react-hot-toast':

npm install react-hot-toast

Depois use em seus componentes:

import toast from 'react-hot-toast';

const handleSubmit = async () => {
  try {
    await cadastrarCliente(formData);
    toast.success('Cliente cadastrado com sucesso!');
  } catch (error) {
    toast.error(`Erro: ${error.message}`);
  }
};
*/

export { useApi, ExemploForm, DashboardPedidos };
