# Para analisar depois

Tudo que ficou em aberto, num lugar só. Nada aqui está decidido.

---

## 1. Decisões da agente de evidência

**Dois comandos que poderiam entrar:**
- ancorar o achado no segundo exato da gravação, para o dev abrir e já ver
- checar se o bug já foi registrado antes, em vez de gerar duplicata

Os dois exigiriam dar permissão de escrita a uma agente que hoje só lê. É o
único motivo para não terem entrado.

---

## 2. Como a agente é acionada

**Webhook `jam.created`** — testado e funcionando em 15/08/2026. Dispara no
momento em que o QA grava.

Traz: link, autor, horário, tipo, origem, URL da página, navegador, sistema,
tela. Opcionais: título e descrição — **é aqui que o padrão `TQ-123 — título X`
chega junto do gatilho**.

Não traz: console, rede, nem o carimbo da aplicação.

Outros eventos: `recording_link.created`, `intercom.recorder.recorded`,
`intercom.recorder.opted_out`.

**Integração Jam + GitHub** — o QA escolhe GitHub ao salvar e nasce uma issue no
repositório. Testado: veio só o link, sem console nem rede no corpo. O título
veio automático e genérico.

A explorar: o **Edit fields** da extensão controla quais campos aparecem na hora
de criar a issue. Pode ser ali que o ID do cenário e o marcador passam a ser
preenchidos.

---

## 3. Outras agentes possíveis

**A que reproduz (Playwright).** Controla um navegador de verdade lendo a
estrutura da página, não a imagem — barato e preciso. Abre três coisas:
reproduzir o bug em vez de só ler evidência; gravar vídeo e publicar como
evidência; forjar resposta do servidor para testar erro de API sem derrubar nada.

Aviso da documentação: não é barreira de segurança.

**As de suporte.** O Jam tem Recording Links — link público que o cliente abre e
grava sem instalar nada — e integração com Intercom, com evento próprio para
quando o cliente **recusa** gravar.

A diferença que muda o desenho: no QA, quem grava conhece o padrão e escreve o
marcador. **No suporte, quem grava é o cliente** — não sabe nada disso. Todo o
contrato de entrada que montamos não vale ali.

---

## 4. Depende de plano ou de configuração alheia

**Sentry.** Mostra erro de backend junto da captura, numa aba do Jam. Resolve o
bug sem rastro no navegador. Exige plano Team, o Jam dentro de um time, e o
produto com Sentry configurado. A verificar: se sai pelo CLI ou só na tela.

---

## 5. Otimizações — só depois de rodar de verdade

- **Duas etapas**: relatório parcial em segundos, completo depois. A ansiedade
  vem do silêncio, não da duração.
- **Leitores em paralelo**: uma coordenadora dispara três e junta. O tempo vira
  o do mais lento, não a soma.
- **Segundo plano**: disparar a leitura enquanto as perguntas ainda estão sendo
  feitas.

---

## 6. Testar

Rodar com um Jam real, olhar a saída, e só então decidir se outras situações
pedem agentes separados.
