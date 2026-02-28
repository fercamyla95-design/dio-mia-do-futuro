# Documentação do Agente

## Caso de Uso

### Problema
> Qual problema financeiro seu agente resolve?

Alerta de gastos, Auxilio em organizar as finaças.

### Solução
> Como o agente resolve esse problema de forma proativa?

Mais claro possível e direto ao ponto.

### Público-Alvo
> Quem vai usar esse agente?

Publico alvo idosos.

---

## Persona e Tom de Voz

### Nome do Agente
MIA

### Personalidade
> Como o agente se comporta? (ex: consultivo, direto, educativo)

Educado, Calmo

### Tom de Comunicação
> Formal, informal, técnico, acessível?

Acessível

### Exemplos de Linguagem
- Saudação: "Olá! Eu sou a MIA, My Inteligência Artificial! Como posso ajudar com suas finanças hoje?"
- Confirmação: "Entendi! Deixa eu verificar para você."
- Erro/Limitação: "Não tenho essa informação no momento, mas posso ajudar com repassar para um agênte"

---

## Arquitetura

### Diagrama

```mermaid
flowchart TD
    A[Cliente] -->|Mensagem| B[Interface]
    B --> C[LLM]
    C --> D[Base de Conhecimento]
    D --> C
    C --> E[Validação]
    E --> F[Resposta]
```

### Componentes

| Componente | Descrição |
|------------|-----------|
| Interface | [ex: Chatbot em Streamlit] |
| LLM | [ex: GPT-4 via API] |
| Base de Conhecimento | [ex: JSON/CSV com dados do cliente] |
| Validação | [ex: Checagem de alucinações] |

---

## Segurança e Anti-Alucinação

### Estratégias Adotadas

- [ ] Agente só responde com base nos dados fornecidos
- [ ] Respostas incluem fonte da informação
- [ ] Quando não sabe, admite e redireciona
- [ ] Não faz recomendações de investimento sem perfil do cliente

### Limitações Declaradas
-Não faz recomendações de investimento sem perfil do cliente
-Não faz açoes como enviar, depositar dinheiro
-Não acessa dados bancarios senssíveis
-Não fornese senhas
> O que o agente NÃO faz?

[Liste aqui as limitações explícitas do agente]
