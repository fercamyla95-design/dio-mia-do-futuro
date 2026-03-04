# Código da Aplicação


```
import json
import pandas as pd 
import streamlit as st 
import requests 

#Carregar dados
OLLAMA_URL = "http://127.0.0.1:11434"
MODELO = "gemma:2b"

caminho_base = "/home/lenovo/Downloads/DIO/MIA_Github"

perfil = json.load(open(caminho_base + "perfil.json"))
transacoes = pd.read_csv(caminho_base + "transacoes.csv")
historico = pd.read_csv(caminho_base + "historico.csv")
produtos = json.load(open(caminho_base + "produtos.json"))

#Notar contexto
contexto = f"""
CLIENTE: {perfil['nome']}, {perfil['idade']}, anos, perfil {perfil['perfil_investidor']}
OBJETIVO:l['objetivo_principal']
PATRIMÔNIO: R$ {perfil['patrimonio_total']} | RESERVA: R$ {perfil['reserva_emergencia_atual']}
TRANSAÇÕES RECENTES:
{transacoes.to_string(index=False)}
ATENDIMENTOS ANTERIORES:
{historico.to_string(index=False)}
PRODUTOS DISPONÍVEIS:
{json.dumps(produtos, indent=2, ensure_ascii=False)}
"""
#Systemm Prompt 
SYSTEM_PROMPT = """Você é a MIA, um assistente artificial amigável e educado.

Objetivo:
auxiliar idosos de forma simples e direta, usando os dados do cliente como exmplo prático.

REGRAS:
1. Sempre baseie suas respostas nos dados fornecidos para dar resposta personalizadas
2. Nunca invente informações financeiras
3. Se não souber algo, admita: "Não tenho esta informação, mas posso explicar..."
4. Nunca recomende investimentos financeiros específicos - apenas explique como funciona
5. Linguagem simples e direta, para um bom entendimento de idosos
6. Sempre pergunte se o cliente entendeu a informação passada
7. Repita a informação sempre que necessário cada vez mais de forma mais simples possivel
"""

#Chamar Ollama
def perguntar(msg):
    prompt = f"""
    {SYSTEM_PROMPT}
    CONTEXTO DO CLIENTE:
    {contexto}
    pergunta: {msg}"""
    r = requests.post(OLLAMA_URL, json-{"model": MODELO, "prompt":prompt, "stream": False})
    return r.json()['response']

#Interface
st.title("Olá, sou MIA, seu assistênte artificial")
if pergunta := st.chat_input("Sua dúvida sonre finanças..."):
    st.chat_message("user").write(pergunta)
    with st.spinner("..."):
        st.chat_message("assistant").write(perguntar(pergunta))


```
