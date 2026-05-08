# Licoes aprendidas

## Estrategicas

### Token GitHub com permissao aparente pode falhar no Git - 2026-05-08

A API pode mostrar permissao administrativa, mas `git push` ainda pode retornar 403 se o PAT nao tiver escrita efetiva via Git. Sempre validar com push real e documentar erro.

### Telegram polling exige um gateway ativo por bot - 2026-05-08

Antes de migrar para VPS, evitar dois gateways usando o mesmo bot Telegram ao mesmo tempo.

### OpenClaw no Windows pode nao instalar gateway como servico sem permissao - 2026-05-08

`openclaw gateway install` pode falhar por permissao. Alternativa local: rodar gateway manualmente ou usar VPS para 24/7.

## Taticas

### SSH Hostinger - 2026-05-08

VPS `2.24.30.151` respondeu na porta 22. VPS `187.77.227.242` nao respondeu no teste local.
