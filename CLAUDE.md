# QAgents — instruções do projeto

Esquadrão de agentes de QA. Cada uma faz uma coisa e para.

## Onde as coisas estão

- `.claude/agents/` — as agentes que rodam (em inglês)
- `agents/` — as mesmas em português, só para leitura e revisão
- `docs/` — o que falta decidir, como preparar a aplicação, regras de captura

Editou uma agente? Editou as duas versões.

## Modelo por agente

A regra é usar o máximo de capacidade necessário e o mínimo suficiente.

| Agente | Modelo | Por quê |
|---|---|---|
| `pr-analyst` | opus | Julgamento. O que ele erra contamina todos os cenários depois |
| `jams-reporter` | sonnet | Extração. Ler log e imagem e relatar o que está lá |
| `test-analyst` | sonnet | Comparação entre cenário e evidência |
| `api-test-writer` | sonnet | Escrita com padrão definido |

Não trocar de modelo no meio de uma sessão: quebra o cache e encarece tudo que
vem depois.

## Como toda agente daqui é escrita

**Toda decisão termina.** Cada caminho do prompt acaba em entregar e parar.
Agente sem condição de parada continua procurando depois de já ter a resposta —
é onde o tempo e o dinheiro somem.

**Uma tentativa.** Comando que falhou é relatado, não investigado. Diagnóstico
de ambiente é da pessoa, não da agente.

**Ferramenta é permissão, não sugestão.** A lista de `tools` é a única barreira
real. Regra escrita no texto se contorna; ferramenta ausente, não.

**Ninguém decide pela pessoa QA.** As agentes relatam, propõem e despacham. Quem
aprova é sempre humano.

**O passo caro é o último.** Imagem, vídeo e captura grande só depois de saber
onde olhar.

## Dados

Nada de dado real em exemplo — sempre fictício. Nada de token, cookie ou
credencial no texto. O que a agente escreve pode acabar numa issue pública.
