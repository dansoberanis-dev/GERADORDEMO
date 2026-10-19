# Gerador de Proposta Comercial — VDEMETRIO

Site privado (ferramenta interna) para gerar propostas comerciais em PDF para locação e produção de eventos — VDEMETRIO Locação e Produção para Eventos.

## Marca
- Logo: `logo.png` (azul `#0c5ba3` + verde `#85b53a`) — fixa no canto superior esquerdo da capa.
- Tema do formulário: escuro. Tema da proposta/PDF: **claro** (4 páginas: capa, quem somos, evento, proposta).
- Slogan: "Seu evento, nosso compromisso."
- Dados da empresa (nome, quem somos, localização, contato) são **fixos no código** (`const COMPANY` no `index.html`).

## Como usar
1. Abra o site (`http://localhost:5432` localmente).
2. Preencha **Cliente** (nome da empresa — aparece na capa ao lado direito), **Evento** e **Orçamento**.
3. Clique em **Gerar proposta** e depois **⬇ Baixar proposta (PDF)** → "Salvar como PDF" (margens: nenhuma; marque "Gráficos de plano de fundo"). As 4 páginas saem no mesmo PDF.

## Mini-CRM (histórico de propostas)
- **💾 Salvar proposta** — grava a proposta no histórico (fica no navegador / localStorage).
- **Carregar** — reabre uma proposta salva no formulário para editar (ao salvar de novo, atualiza o mesmo registro).
- **Status** — Rascunho / Enviada / Aprovada / Não fechada (em cada registro).
- **⬇ Relatório CSV** — exporta todas as propostas (abre no Excel; separador `;`).
- **⬇ Backup JSON** — exporta o histórico completo em arquivo.
- **⬆ Importar backup** — restaura/combina histórico em outro computador.
- **Nova proposta** — limpa o formulário.

Obs.: os dados ficam no navegador (localStorage) — por isso o backup JSON é recomendado ao trocar de PC ou limpar o navegador.

## Projeto local (Windows)
A pasta do projeto no seu computador é: `E:\sites\vdemetrio\gerador`

### Atualizar o projeto a partir do ZIP baixado (PowerShell)
```powershell
Expand-Archive -Force "$env:USERPROFILE\Downloads\gerador-vdemetrio.zip" "$env:USERPROFILE\Downloads\gerador-vdemetrio-tmp"
Copy-Item -Recurse -Force "$env:USERPROFILE\Downloads\gerador-vdemetrio-tmp\*" "E:\sites\vdemetrio\gerador\"
Remove-Item -Recurse -Force "$env:USERPROFILE\Downloads\gerador-vdemetrio-tmp"
```

### Rodar em localhost na porta 5432 (PowerShell)
```powershell
cd E:\sites\vdemetrio\gerador
py -m http.server 5432
# ou: npx serve -l 5432
```
Abra `http://localhost:5432`.

## Deploy na Vercel (somente após o OK final)
```powershell
cd E:\sites\vdemetrio\gerador
npx vercel
npx vercel --prod
```
- Site estático (`index.html` + imagens), sem build.
- Para privacidade, use a "Deployment Protection" da Vercel (senha) ou um subdomínio não divulgado.
- `vercel.json` já envia `X-Robots-Tag: noindex, nofollow`.

## Estrutura
- `index.html` — aplicação completa (formulário + prévia + PDF + mini-CRM).
- `logo.png` — logo oficial VDEMETRIO.
- `capa-bg.png` — imagem de fundo da capa (faixa verde + ícones).
- `quem-somos.jpg` — página "Quem somos" pronta (arte feita no Canva).
- `hex-bg.png` — fundo hexagonal das páginas de evento e proposta.
- `vercel.json` — headers de deploy.

## Acesso (senha)

- Tela de login ao abrir o sistema. Padrão: usuário **admin** / senha **vdemetrio2026**.
- Para trocar ou adicionar usuários, edite a lista `USERS` no `index.html`.
- Para gerar o hash de uma senha nova, abra o console do navegador (F12) e digite: `hashPw('senhaNova')`.
- Botão "Sair" no topo do formulário encerra a sessão.
- IMPORTANTE: é uma trava de acesso por obscuridade (roda no navegador). Mantenha o repositório PRIVADO no GitHub. Para proteção de verdade, use a proteção de senha da Vercel (plano Pro) ou Cloudflare Access.

## PDF no celular

- Android (Chrome): Imprimir → "Salvar como PDF" → vai para Downloads, com o nome "Proposta CLIENTE - VDEMETRIO".
- iPhone/iPad (Safari): na prévia de impressão, use Compartilhar → "Salvar nos Arquivos" (escolha Downloads).
- O nome do arquivo segue o cliente, mas o navegador sempre mostra a caixa de diálogo para confirmar/renomear.
- Nada é enviado a servidores: tudo roda no navegador.
