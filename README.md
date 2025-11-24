Chat DeepSeek com Streamlit e Groq

Este projeto implementa uma aplicação simples utilizando Streamlit e o modelo Llama 3.3 70B (versão Groq) para criar um chatbot interativo. A aplicação mantém o histórico de mensagens na sessão e exibe as interações no próprio layout do Streamlit.

🚀 Funcionalidades

Interface web simples utilizando Streamlit

Armazenamento de histórico de mensagens na sessão

Integração com Groq via langchain_groq

Interação estilo chat (usuário x IA)

📦 Dependências

Certifique-se de instalar as dependências abaixo:

pip install streamlit python-dotenv langchain-groq
🔑 Configuração da Chave de API

Crie um arquivo .env na raiz do projeto contendo:

GROQ_API_KEY=SEU_TOKEN_AQUI

A biblioteca dotenv carregará essa chave automaticamente.

▶️ Como executar a aplicação

No terminal, dentro do diretório do projeto:

streamlit run app.py
🧠 Código Fonte Principal

Abaixo está o código utilizado pela aplicação:

from dotenv import load_dotenv, find_dotenv
load_dotenv(find_dotenv())
import streamlit as st
from langchain_groq import ChatGroq


llm = ChatGroq(model="llama-3.3-70b-versatile")


st.set_page_config(page_title="Chat DeepSeek", layout="centered")
st.title("Teste com DeepSeek")


if "messages" not in st.session_state:
    st.session_state["messages"] = []


messages = st.session_state["messages"]
for type, content in messages:
    chat = st.chat_message(type)
    chat.markdown(content)


in_message = st.chat_input("Envie sua dúvida:")
if in_message:
    messages.append(("human", in_message))
    chat = st.chat_message("human")
    chat.markdown(in_message)


    response = llm.invoke(messages).content
    messages.append(("ai", response))


    chat = st.chat_message("ai")
    chat.markdown(response)
📁 Estrutura Sugerida do Projeto
📂 projeto
 ├── app.py
 ├── .env
 ├── README.md
 └── requirements.txt
📄 Exemplo de requirements.txt
streamlit
python-dotenv
langchain-groq
📝 Observações

O modelo selecionado é llama-3.3-70b-versatile, que roda via Groq.

Certifique-se de que sua chave Groq está ativa e válida.

O histórico de mensagens persiste enquanto a sessão do navegador estiver ativa.