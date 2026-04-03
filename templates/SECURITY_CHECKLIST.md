# Security Checklist — [Nome do Projeto]

Execute este checklist em toda feature antes do merge em `main`.

---

## Autenticação e Autorização

- [ ] Endpoints protegidos com autenticação adequada
- [ ] Autorização verifica permissões no servidor — nunca no cliente
- [ ] Tokens com expiração configurada
- [ ] Secrets via variáveis de ambiente — nunca hardcoded, nunca em logs

## Input Validation

- [ ] Toda entrada de usuário validada e sanitizada
- [ ] SQL injection prevention: ORM parametrizado em todas as queries
- [ ] Dados de entrada com limites de tamanho definidos

## APIs e Comunicação

- [ ] SSRF protection em HTTP clients externos
- [ ] Timeout configurado em todas as chamadas externas (< 10s)
- [ ] Rate limiting configurado nos endpoints públicos
- [ ] Headers de segurança configurados (CSP, HSTS, X-Frame-Options)

## Dados Sensíveis

- [ ] Dados sensíveis não aparecem em logs
- [ ] PII não persiste além do necessário (LGPD/GDPR)
- [ ] Dados em trânsito criptografados (HTTPS/TLS)

## Infraestrutura

- [ ] Imagens Docker sem vulnerabilidades críticas (CVE scan)
- [ ] Dependências atualizadas — sem CVEs críticos conhecidos
- [ ] Configurações de produção separadas do código

---

**Revisão humana obrigatória** para qualquer item marcado como exceção.
