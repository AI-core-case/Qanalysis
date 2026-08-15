# QAgents

Um esquadrão de agentes de IA para o trabalho repetitivo de QA: escrever caso de teste, analisar bug, revisar PR, publicar resultado, manter memória do produto entre sessões.

Feito por quem faz QA, para quem faz QA.

## O que ele resolve

QA gasta boa parte do dia em tarefas que são estruturadas mas não automatizáveis por script: transformar um card em cenário de teste, investigar uma falha e escrever o bug direito, revisar se o PR quebrou algum fluxo conhecido. Este projeto entrega agentes especializados para cada uma dessas etapas.

## Requisitos

- [Claude Code](https://claude.com/claude-code) com uma assinatura ativa (Pro, Max ou Team)
- Git

O projeto é gratuito e open source. O que custa é o modelo — **cada pessoa roda com a própria assinatura**, e nada é cobrado por este repositório.

### Para a agente de evidência

A `jams-reporter` lê gravações pelo CLI do [Jam](https://jam.dev). Sem ele, ela avisa e para — não existe caminho alternativo, e isso é proposital: o CLI permite filtrar os dados antes de eles entrarem no contexto, o que mantém a leitura barata.

- CLI do Jam instalado e acessível no `PATH`
- Token em `JAM_TOKEN`, na variável de ambiente

Se você não usa Jam, as outras agentes funcionam normalmente.

## Instalação

```bash
git clone https://github.com/QAgents-AI/qagents.git
cd qagents
cp .env.example .env    # preencha com os seus valores
```

Abra o Claude Code na pasta do projeto. Os agentes ficam disponíveis automaticamente.

## Os seus dados nunca saem daqui

O projeto separa **motor** de **dados**:

- O que está versionado: agentes, prompts, workflows, estrutura — nada específico de ninguém
- O que fica só na sua máquina: `.env`, `.memory/` e `.qa-runs/`, todos ignorados pelo git

Ou seja: você pluga o seu contexto sem risco de vazar nada para o repositório público.

## Estrutura

```
.claude/agents/     agentes especializados
.claude/skills/     habilidades reutilizáveis
.github/workflows/  automações de CI
.memory/            sua memória local (ignorada pelo git)
```

## Contribuindo

Issues e pull requests são bem-vindos. Se você é QA e sentiu falta de um agente, abra uma issue contando o problema — é assim que a lista cresce.

## Licença

MIT
