# Back-end do Chatbot IAGRO

Este repositório contém o back-end Flask para um chatbot que usa Google Gemini e Socket.IO para comunicação em tempo real.

## Recursos

- Servidor Flask com suporte a WebSockets via `flask-socketio`
- Integração com Google Gemini (`google-genai`)
- Sessões de usuário usando `Flask` e `uuid4`
- Cada usuário recebe uma conversa individual armazenada em memória
- Respostas de IA escritas com foco em agronegócio brasileiro

## Como usar

1. Instale o Python 3.11+ ou versão compatível.
2. Crie e ative um ambiente virtual:

```bash
python -m venv venv
venv\Scripts\activate
```

3. Instale as dependências:

```bash
pip install -r requirements.txt
```

4. Crie um arquivo `.env` na pasta do projeto com a chave da API do Gemini:

```env
GENAI_KEY=sua_chave_gemini_aqui
```

5. Execute o servidor:

```bash
python app.py
```

6. Acesse a rota de status para verificar se o servidor está ativo:

```bash
http://127.0.0.1:5000/
```

## Como funciona

- `app.py` inicializa o Flask e o Socket.IO
- O endpoint `/` retorna um JSON simples com status
- O evento Socket.IO `connect` cria ou recupera a sessão do usuário
- O evento `enviar_mensagem` envia a mensagem do usuário para o Gemini
- O bot responde usando o evento `nova_mensagem`

## Ponto de atenção

- O histórico de chat é mantido em memória no dicionário `active_chats`
- Se o servidor for reiniciado, as sessões em memória serão perdidas
- Para produção, considere usar um armazenamento persistente e uma `secret_key` segura

## Dependências principais

- `flask`
- `flask-socketio`
- `google-genai`
- `python-dotenv`
- `gevent`
- `gunicorn`

## Personalização do bot

O bot usa um prompt de sistema em português para responder como um assistente de agronegócio:

- Respostas curtas e diretas
- Formatação markdown limpa
- Sem saudações ou encerramentos

## Observações

- Esta implementação funciona melhor com um front-end que suporte Socket.IO
- Caso utilize `gunicorn` em produção, execute com `gevent`/`gevent-websocket`

---

Created for o back-end do chatbot de agronegócio IAGRO.