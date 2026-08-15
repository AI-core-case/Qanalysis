# Preparar a aplicação para gerar evidência boa

Opcional. As agentes funcionam sem isso — só entregam menos.

## O problema

A ferramenta de gravação vê o que aparece no navegador: tela, console, rede.
Ela não vê o que mora dentro do sistema — qual usuário estava logado, qual
versão estava no ar, quais recursos estavam ligados naquela conta.

É justamente isso que o desenvolvedor pergunta quando recebe um bug. E hoje
alguém digita a resposta na mão, em todo relatório.

## A solução

O time de desenvolvimento configura uma vez, na raiz da aplicação, o que deve
ir junto de toda gravação. A partir daí, toda evidência nasce carimbada.

```javascript
import { jam } from "@jam.dev/sdk";

jam.metadata(() => ({
  // quem
  userId: store.user.id,
  accountId: store.account.id,
  role: store.user.role,

  // onde
  environment: import.meta.env.MODE,
  appVersion: import.meta.env.VITE_VERSION,
  route: window.location.pathname,

  // o que estava ligado
  featureFlags: store.flags.enabled,

  // a ponte com o servidor
  traceId: store.session.traceId,
}));
```

A função é executada **no momento da captura**, não no carregamento da página.
O carimbo mostra o estado real da tela na hora do erro.

## O que vale carimbar, em ordem

1. **`traceId`** — o identificador de rastreio que o app já manda nas chamadas.
   É o campo mais valioso: liga a gravação ao log do servidor. O desenvolvedor
   abre a evidência, copia o identificador e acha a requisição exata no backend.
2. **`environment` e `appVersion`** — matam a pergunta "em qual ambiente e qual
   versão?"
3. **`featureFlags`** — explicam o bug que só acontece em uma conta
4. **`userId` e `accountId`** — reprodução
5. **`role`** — bugs de permissão

## Dois cuidados

**Só identificador, nunca dado pessoal.** `userId: 5492` sim; nome, e-mail,
telefone ou documento não. Evidência fica armazenada, e dado pessoal em
evidência é problema de conformidade.

**Limite de 10 KB.** Não carimbe o estado inteiro da aplicação. Se estourar, a
gravação é criada **sem** o carimbo — e a falha é silenciosa.

## Borrão automático de dado sensível

Com o domínio conectado, a ferramenta de gravação borra sozinha, **no navegador
e antes de enviar**: campo de senha, número de cartão, CPF e CNPJ, dados
bancários, telefone, e-mail, chave de API e token.

Isso não custa nada em tempo nem em processamento das agentes — quando a
gravação chega, já está borrada. É proteção na origem, muito melhor que mascarar
depois.

Para controlar caso a caso, marque no próprio HTML:

```html
<div data-jam-blur>conteúdo que deve sair borrado</div>
<div data-jam-no-blur>conteúdo que pode aparecer</div>
```

Três limitações conhecidas:

- Conteúdo dentro de quadro embutido (`iframe`) é borrado inteiro, sem seleção
- Pode haver um lampejo antes do borrão aplicar, no carregamento
- Redimensionar a janela pode expor o conteúdo por um instante

## O que muda para as agentes

Com o carimbo, o campo `Environment` do relatório vem preenchido sozinho, e a
pessoa QA escreve só o que a máquina não tem como saber: o cenário, o marcador
e o momento do erro.

Sem o carimbo, as agentes seguem funcionando — só perguntam mais.
