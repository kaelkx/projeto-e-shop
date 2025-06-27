
# 📊 Integração de Soluções NoSQL com Streamlit para Visualização de Dados

Este projeto simula uma aplicação para a empresa fictícia **E-Shop Brasil**, que está em processo de modernização de sua infraestrutura digital. A proposta é permitir o gerenciamento de dados de forma eficiente e escalável utilizando tecnologias modernas como **MongoDB**, **Docker** e **Streamlit**.

---

## 🎯 Objetivo

Desenvolver uma aplicação Python com interface interativa (Streamlit) que realize operações **CRUD** (Criar, Ler, Atualizar e Deletar) conectando-se a um banco de dados **NoSQL (MongoDB)**. A aplicação roda de forma containerizada com Docker para facilitar a implantação e portabilidade.

---

## 🧱 Tecnologias Utilizadas

- 🐍 Python
- 📦 MongoDB (NoSQL)
- 🌐 Streamlit (interface web)
- 🐳 Docker e Docker Compose
- 🧪 Faker (geração de dados falsos)

---

## 📁 Estrutura do Projeto

```
projeto-e-shop/
├── app/
│   ├── main.py          # Interface Streamlit
│   ├── db.py            # Conexão com MongoDB
│   └── utils.py         # Funções auxiliares
├── scripts/
│   └── generate_data.py # Geração de dados com Faker
├── docker-compose.yml   # Configuração dos containers
├── Dockerfile           # Container da aplicação
├── requirements.txt     # Dependências Python
└── README.md            # Este arquivo
```

---

## ⚙️ Instalação e Execução com Docker

### 1. Clonar o repositório

```bash
git clone https://github.com/seu-usuario/projeto-e-shop.git
cd projeto-e-shop
```

### 2. Subir os containers com Docker Compose

```bash
docker-compose up --build
```

Acesse a aplicação no navegador:

👉 http://localhost:8501

---

## 🧪 Geração de Dados com Faker

Um script em `scripts/generate_data.py` gera **1 milhão de registros falsos** para simular uma base realista de clientes.

### Exemplo de cliente gerado:

```json
{
  "nome": "Carlos Roberto",
  "email": "carlos.roberto@gmail.com",
  "telefone": "(11) 98765-4321",
  "idade": 35
}
```

### Como executar o script (fora do Docker):

```bash
python scripts/generate_data.py
```

---

## 🖥️ Trechos de Código Importantes

### Conexão com MongoDB – `app/db.py`

```python
from pymongo import MongoClient

def get_connection():
    client = MongoClient("mongodb://mongo:27017/")
    db = client["eshop"]
    return db
```

### Operações CRUD com Streamlit – `app/main.py`

```python
import streamlit as st
from app.db import get_connection

db = get_connection()
clientes = db["clientes"]

st.title("E-Shop CRUD de Clientes")

nome = st.text_input("Nome")
email = st.text_input("Email")

if st.button("Cadastrar"):
    clientes.insert_one({"nome": nome, "email": email})
    st.success("Cliente cadastrado com sucesso!")

if st.button("Listar clientes"):
    for cliente in clientes.find().limit(5):
        st.write(cliente)
```

---

## 📦 Exemplo de `docker-compose.yml`

```yaml
version: '3.8'
services:
  mongo:
    image: mongo
    ports:
      - "27017:27017"

  streamlit:
    build: .
    ports:
      - "8501:8501"
    volumes:
      - .:/app
    working_dir: /app
    command: streamlit run app/main.py
    depends_on:
      - mongo
```

---

## 📌 Requisitos Atendidos da Atividade

- ✅ CRUD com MongoDB
- ✅ Interface com Streamlit
- ✅ Banco NoSQL (MongoDB)
- ✅ Uso de Docker
- ✅ Script de geração com Faker (+1 milhão de dados)
- ✅ Código organizado em estrutura modular
- ✅ Projeto documentado e pronto para GitHub

---

## 👨‍💻 Autor

**Pablo Kael**  
Projeto desenvolvido como parte da disciplina de Banco de Dados NoSQL.

---

