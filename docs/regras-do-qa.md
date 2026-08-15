# Regras do QA — rascunho

Configuração e hábito humano. Nada aqui vai para o prompt das agentes.

## Ao capturar

- Gravação de no máximo **1 minuto**
- Bug de resposta de bot é **print**, nunca vídeo

## O que escrever

Formato:

```
<ID do cenário> — <título do cenário> <marcador>
<se souber: em que momento e o que apareceu de errado>
```

- **`X`** — o cenário falhou
- **`✔️`** — o cenário passou, mas apareceu outro bug

**Onde escrever:**
- Vídeo → na descrição, dentro do Jam
- Print → no chat, junto com a imagem

## Configuração

- Manter o resumo automático do Jam **desligado** — o campo de título e
  descrição é do processo
  <!-- falta: onde exatamente se desliga -->

## No chat

- Mandar só o link. Sem instrução, sem explicação.

## Uma conversa por assunto

**Continue na mesma conversa** enquanto for o mesmo bug ou o mesmo cenário — a
agente já tem o contexto e você não repete nada.

**Abra conversa nova ao trocar de assunto**: outro card, outro produto, outra
tarefa. Não use a mesma conversa o dia inteiro.

O motivo é custo: cada mensagem nova carrega junto tudo o que já foi dito antes.
Numa conversa que virou o dia, você paga o histórico inteiro para perguntar uma
coisa simples — e a agente ainda se confunde com assunto que já morreu.

## Para verificar depois

- https://jam.dev/docs/recording-links
