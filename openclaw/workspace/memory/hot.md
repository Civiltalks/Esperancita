# HOT - Contexto quente da Esperancita

Atualizado: 2026-05-08

## Prioridades imediatas

1. Finalizar estruturacao da Esperancita localmente.
2. Validar skills visiveis e prontas.
3. Manter GitHub sincronizado.
4. Preparar acesso SSH para VPS Hostinger.
5. Preparar Etapa 2: arquivos de comportamento, atividade e criterios.

## Bloqueios

- Deploy na Hostinger depende de SSH autorizado na VPS.
- Contexto pessoal/profissional detalhado do usuario ainda precisa validacao humana.
- Dominio/subdominio publico ainda nao definido.

## Decisoes recentes

- Conversa principal usa OAuth/conta OpenAI, nao API key.
- API OpenAI fica para transcricao/Whisper.
- GitHub oficial da Esperancita e `Civiltalks/Esperancita`.
- Segredos e estado privado nao entram no Git.

## Proximo comando seguro

```powershell
openclaw config validate
openclaw skills check --agent main
git status --short --branch
```
