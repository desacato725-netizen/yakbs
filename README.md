# agreedkey — pacote Vercel

## Publicação

1. Extraia este pacote.
2. Importe a pasta na Vercel ou faça deploy pelo CLI.
3. O arquivo principal é `index.html` e os headers de segurança estão em `vercel.json`.

A source já está conectada ao backend Manus:

`https://sielzadaapi-fn6m4d85.manus.space`

A validação usa `POST /api/auth/login` com key e identificador do dispositivo, e a sessão usa `GET /api/auth/session` com Bearer token. O token fica em `sessionStorage`, não na URL nem em cookie cross-site.

## Segurança aplicada

- HTTPS e HSTS na Vercel.
- Content Security Policy sem `unsafe-eval`, restringindo conexões ao backend Manus.
- `X-Frame-Options: DENY`, `frame-ancestors 'none'`, `nosniff` e `Referrer-Policy: no-referrer`.
- Permissions Policy bloqueando câmera, microfone, geolocalização, pagamentos e USB.
- Requests com `cache: no-store`, `credentials: omit`, `redirect: error` e `referrerPolicy: no-referrer`.
- Session token em `sessionStorage` e HWID local separado para o vínculo de dispositivo.

A senha administrativa, a criação das keys e a validação real continuam exclusivamente no backend Manus. Não coloque senhas, tokens administrativos ou chaves privadas neste HTML.
