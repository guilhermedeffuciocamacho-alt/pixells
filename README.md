# Pixelly — Vercel

## Estrutura
- `index.html` — site
- `api/submit.js` — endpoint seguro que envia os pedidos ao Discord
- `vercel.json` — configuração da função

## Configuração na Vercel

1. Suba este projeto para um repositório GitHub.
2. Importe o repositório na Vercel.
3. Em **Project Settings → Environment Variables**, crie:
   - **Name:** `DISCORD_WEBHOOK_URL`
   - **Value:** seu webhook do Discord
   - Marque o ambiente que será usado (Production, e Preview/Development se necessário).
4. Faça um novo deploy.

## Importante
Não coloque o webhook dentro do `index.html`. O frontend chama apenas `/api/submit`; a função da Vercel guarda e usa a variável secreta no servidor.

Como o webhook foi exposto em uma mensagem/chat, é recomendável **recriar/rotacionar o webhook no Discord** e usar o novo endereço em `DISCORD_WEBHOOK_URL`.

## Proteções incluídas
- Validação de campos no servidor
- Limite de 3 tentativas por janela de 60s por IP (best-effort por instância serverless)
- Cooldown após envio bem-sucedido
- Honeypot invisível para bots
- Validação de Origin
- Limites de tamanho dos textos
- `allowed_mentions: { parse: [] }` para evitar abuso de menções
- O webhook não é exposto ao navegador
