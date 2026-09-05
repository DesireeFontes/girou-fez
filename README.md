# 🎡 Girou, Fez

App de página única que sorteia uma tarefa doméstica curta e já emenda no cronômetro.
A ideia é tirar de você a etapa de *decidir* — você só escolhe quanto tempo tem, gira, e executa.

Sem build, sem dependências, sem servidor. É um arquivo HTML só.

---

## Como usar

1. Na aba **Roleta**, toque em quanto tempo você tem (5, 10, 15, 30 min ou "tanto faz").
2. A roleta monta com até 8 tarefas que cabem nesse tempo.
3. **Girar!** → cai numa tarefa → **Bora!** dispara o cronômetro com o tempo dela.
4. Se não serviu: *Gira de novo* (devolve pro bolo) ou *Essa não* (tira da rodada de hoje).
5. Na aba **Tarefas** você cadastra, escolhe um emoji e apaga o que não usa mais.

As tarefas ficam salvas no `localStorage` do navegador — ou seja, **no seu aparelho**.
Nada é enviado para servidor nenhum. Trocar de celular ou limpar os dados do navegador zera a lista.

---

## Rodar localmente

Abra o `index.html` no navegador. É isso.

---

## Publicar e instalar no celular

### Opção A — Netlify Drop (mais rápida)

1. Acesse `app.netlify.com/drop` e arraste o `index.html`.
2. Copie a URL que aparecer.

### Opção B — GitHub Pages

Só funciona com **repositório público** no plano Free.
Em *Settings → Pages*, escolha a branch `main` e a pasta `/ (root)`.

### Opção C — Cloudflare Pages + Access

Se quiser o app protegido por login: publique no Cloudflare Pages e crie uma
aplicação no painel Zero Trust com uma política liberando só o seu e-mail.
O plano gratuito cobre até 50 usuários.

### Instalar como app

Com a URL aberta no celular:

- **iPhone**: botão compartilhar → *Adicionar à Tela de Início*
- **Android**: menu ⋮ → *Adicionar à tela inicial*

Vai virar ícone na tela, abrir em tela cheia e funcionar offline.

---

## Subir para o GitHub

Na pasta do projeto:

```bash
git init
git add .
git commit -m "Primeira versão da roleta"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/girou-fez.git
git push -u origin main
```

Crie o repositório vazio no GitHub antes (sem README, sem .gitignore — eles já estão aqui)
e troque `SEU-USUARIO` pelo seu nome de usuário.

Depois, a cada mudança:

```bash
git add .
git commit -m "descrição do que mudou"
git push
```

---

## Estrutura

```
index.html    # o app inteiro: HTML, CSS e JS num arquivo só
README.md
.gitignore
```

---

## Mexer no código

Tudo está dentro do `index.html`.

- **Cores da roleta** — array `SEGS`, perto do topo do `<script>`.
- **Tarefas de exemplo** — array `SEED`. Só valem no primeiro acesso, quando ainda não há nada salvo.
- **Tempos disponíveis** — array `TIMES`.
- **Emojis do cadastro** — array `FACES`.
- **Frases de comemoração** — array `CHEERS`.
- **Duração do giro** — `transition` do `#spinner` no CSS e o `setTimeout` no fim da função `spin()`. Os dois precisam bater.

Se mudar o formato dos dados salvos, troque também a constante `KEY`
(`roleta:v2` → `roleta:v3`) para não conflitar com o que já está no aparelho.

---

## Acessibilidade

Respeita `prefers-reduced-motion`: com a opção de reduzir animações ligada no sistema,
o giro fica curto e o confete não aparece.
