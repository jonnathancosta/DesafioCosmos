# 📦 Integração com Azure Cosmos DB (MongoDB API)

Este desafio, reealizado em 10/2024, demonstra como conectar ao **Azure Cosmos DB** usando a API compatível com **MongoDB**, com credenciais seguras armazenadas no **Azure Key Vault**.  
O notebook inclui exemplos práticos de **inserção, consulta, atualização** e **agregação de dados**, simulando um cenário de e-commerce.

---

## 🚀 Funcionalidades

- **Autenticação segura** usando Azure Key Vault e `DefaultAzureCredential`
- **Conexão ao Cosmos DB** via `pymongo`
- **Criação e popularização de coleções** (`produtos`, `usuarios`, `pedidos`)
- **Consultas simples e com filtros**
- **Atualização de estoque** após pedidos
- **Agregação** para análise de vendas por categoria

---

## 📂 Estrutura das coleções

- **produtos**  
  ```json
  {
    "produto_id": "prod001",
    "nome": "Camiseta de Algodão",
    "categoria": "Roupas",
    "preco": 49.99,
    "estoque": 120
  }
  ```

- **usuarios**  
  ```json
  {
    "usuario_id": "user001",
    "nome": "João Silva",
    "email": "joao.silva@email.com",
    "endereco": "Rua das Flores, 123, São Paulo, SP"
  }
  ```

- **pedidos**  
  ```json
  {
    "pedido_id": "ped001",
    "usuario_id": "user001",
    "produto_id": "prod003",
    "quantidade": 1
  }
  ```

---

## 🛠 Pré-requisitos

- Python 3.8+
- Conta no **Azure** com:
  - **Cosmos DB** criado com API do MongoDB
  - **Azure Key Vault** configurado com o segredo da string de conexão
- Bibliotecas Python:
  ```bash
  pip install pymongo azure-cosmos azure-identity azure-keyvault-secrets
  ```

---

## ⚙ Configuração

1. **Configurar Key Vault**  
   - Armazene no Key Vault o segredo com a *connection string* do Cosmos DB.  
   - Nome do segredo (exemplo):  
     ```
     db-academy-cadeiadeconexao
     ```

2. **Atualizar variáveis no notebook**  
   ```python
   key_vault_url = "https://SEU-KEYVAULT.vault.azure.net/"
   secret_name_connection_string = "NOME-DO-SEU-SEGREDO"
   ```

3. **Autenticação no Azure**  
   - Você pode usar `Azure CLI`, `Managed Identity` ou variáveis de ambiente para `DefaultAzureCredential`.

---

## ▶ Execução

O notebook está organizado em blocos que cobrem:

1. **Conexão segura**
   ```python
   from azure.identity import DefaultAzureCredential
   from azure.keyvault.secrets import SecretClient
   from pymongo import MongoClient
   ```

2. **Inserção de dados** (produtos, usuários e pedidos)
3. **Consultas** (listar todos os documentos e filtros específicos)
4. **Atualização de estoque** após um pedido
5. **Agregação de vendas por categoria**

Para rodar:

```bash
jupyter notebook cosmosdb.ipynb
```

---

## 📊 Exemplo de saída

**Listagem de produtos**
```
Bancos de dados disponíveis no Cosmos DB:
jonnathan_costa_DB
Lista de todos os produtos:
{'produto_id': 'prod001', 'nome': 'Camiseta de Algodão', ...}
```

**Consulta filtrada**
```
Produtos Eletrônicos com preço abaixo de 500:
Nome: Fone de Ouvido Bluetooth, Preço: 299.9
```

**Agregação**
```
Análise de Vendas por Categoria:
Categoria: Eletrônicos, Quantidade Total de Pedidos: 5
Categoria: Roupas, Quantidade Total de Pedidos: 3
```

---

## 📌 Observações

- **Segurança**: Nunca exponha a *connection string* diretamente no código. Sempre use Key Vault ou variáveis de ambiente.
- **Limpeza**: Ao testar, você pode precisar limpar coleções para evitar dados duplicados.
- **Escalabilidade**: Cosmos DB permite consultas e agregações de alta performance, mas lembre-se dos limites de RU/s.

---

