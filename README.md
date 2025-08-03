# Projeto: Catálogo Virtual com Agentes de IA para Conectar Empresas e Pessoas

## Visão Geral

Este projeto cria um catálogo virtual inteligente que permite o cadastro e a busca de empresas por usuários, com foco em uma determinada região. A arquitetura inclui agentes de IA para interação via linguagem natural, um backend robusto em Python com observabilidade via **LangSmith**, e um frontend simples para consumo via navegador. Com o uso de engenharia de contexto e banco vetorial, os agentes se tornam semanticamente mais eficazes e personalizados.

---

## 1. Arquitetura da Solução

```mermaid
graph TD
  A[Usuário Final] -->|Frontend Streamlit| B(Interface Web)
  B --> C(Agente de Busca com Embeddings)
  B --> D(Agente de Cadastro)
  C --> E(API Backend FastAPI)
  D --> E
  E --> F[(PostgreSQL + ChromaDB)]
  E --> G(LangSmith Observabilidade)
  G --> I[Dashboard LangSmith]

```
## 2. Requisitos
- Python 3.11+
- PostgreSQL (local)
- Virtualenv / Poetry / Pipenv (gerenciador de dependências)

## 3. Setup Local Passo a Passo

  3.1. Clone o repositório
  ```
    git clone https://github.com/seuusuario/ia-catalog.git
    cd ia-catalog
  ```
    
  3.2 - Crie o ambiente virtual e instale dependências
  ```
      python -m venv venv
      source venv/bin/activate   # Windows: .\venv\Scripts\activate
      pip install -r requirements.txt
  ```
  3.3 - Configurar variáveis de ambiente no .env
  ```
      OPENAI_API_KEY=sk-...
      LANGCHAIN_API_KEY=ls-...
      LANGCHAIN_TRACING_V2=true
      LANGCHAIN_PROJECT=agent-catalog
      PG_URI=postgresql://usuario:senha@localhost:5432/postgres
  ```

  3.4. Crie a tabela no PostgreSQL
  ```
    CREATE TABLE company (
    company_id SERIAL PRIMARY KEY,
    company_name TEXT,
    company_category TEXT,
    company_city TEXT,
    company_phone TEXT,
    company_email TEXT
    );
  ```

  3.5. Inicie o backedn FASTAPI - acesse: http://localhost:8000/docs
  ```
    cd backend
    uvicorn main:app --reload
  ```

  3.6. Inicie o frontend Streamlit - acesse: http://localhost:8501
  ```
    cd frontend
    streamlit run app.py
  ```
## 4 - Monitoramento LangSmith
  - Acesse: https://smith.langchain.com
  - Crie uma conta gratuita
  - Gere sua API_KEY
  - Monitore os agentes, entradas, saídas, consumo de token e latência

## 5 - Estrutura do Projeto
```
  ai-catalog/
  ├── backend/
  │   ├── main.py
  │   ├── agents/
  │   │   ├── register_agent.py
  │   │   └── search_agent.py
  │   ├── db/
  │   │   └── models.py
  │   └── vector/
  │       └── vectorstore.py
  ├── frontend/
  │   └── app.py
  ├── vectordb/              #persiste os embeddings local
  ├── .env
  ├── requirements.txt
  └── README.md
```

## 6. Features Incluídas
  ✅ Cadastro de empresas via linguagem natural
  ✅ Busca vetorial semântica usando embeddings
  ✅ Armazenamento em PostgreSQL e ChromaDB
  ✅ Frontend responsivo em Streamlit
  ✅ Observabilidade completa com LangSmith
  ✅ Separação clara entre camadas: agentes, API, vetor, banco


