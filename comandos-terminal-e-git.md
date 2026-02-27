# Comandos de terminal: navegar e Git

*Comandos básicos para te mexeres no computador pelo terminal e para usares Git. Estás a aprender — vai ao teu ritmo.*

---

## Parte 1 — Navegar no computador

O terminal trabalha com **pastas** (diretórios). Estás sempre “dentro” de uma. Estes comandos servem para ver onde estás e mudar de sítio.

### `pwd` — Onde estou?
- Mostra o **caminho completo** da pasta onde estás.
- *Exemplo:* se aparecer `.../self_improvement`, é essa a tua pasta atual.

### `ls` — O que há aqui?
- Lista ficheiros e pastas dentro da pasta atual.
- **`ls -l`** — mais detalhes (tamanho, datas).
- **`ls -a`** — inclui ficheiros ocultos (ex.: `.git`).

### `cd` — Mudar de pasta
| Comando | O que faz |
|---------|-----------|
| `cd nome_da_pasta` | Entra nessa pasta (tem de existir) |
| `cd ..` | Sobe um nível (pasta “pai”) |
| `cd` | Vai à tua pasta de utilizador (home) |
| `cd /caminho/completo` | Vai diretamente para esse caminho |

> **Dica:** no macOS/Linux escreve as primeiras letras do nome e carrega **Tab** — o terminal completa.

### `mkdir` — Criar uma pasta
- **`mkdir nome_nova_pasta`** — cria uma pasta com esse nome na pasta atual.

### `clear` — Limpar o ecrã
- Apaga o texto do terminal. Não apaga ficheiros; só deixa o ecrã mais limpo.

---

## Parte 2 — Git (versões do teu projeto)

O Git guarda **versões** do teu projeto. Assim podes voltar atrás se algo correr mal ou ver o que mudou.

### `git status` — O que mudou?
- Mostra em que ramo estás e que ficheiros foram alterados, adicionados ou não estão a ser seguidos.
- *Usa sempre que quiseres saber o estado do projeto.*

### `git init` — Começar a usar Git
- Faz **uma vez** por projeto. Cria a pasta oculta `.git` e o projeto passa a ser um “projeto Git”.

### `git add` — Preparar ficheiros
- **`git add nome_do_ficheiro`** — prepara esse ficheiro.
- **`git add .`** — prepara todos os ficheiros alterados.
- “Preparar” = marcar para entrar na próxima “fotografia” (commit).

### `git commit` — Guardar uma versão
- **`git commit -m "Descrição do que fizeste"`** — guarda as alterações que preparaste, com uma mensagem curta.
- *Exemplo:* `git commit -m "Adicionei ficheiro de prompts"`.

### `git log` — Ver o histórico
- Lista os commits (versões guardadas), do mais recente ao mais antigo.
- *Sai com a tecla **q**.*

### `git diff` — Ver as diferenças
- Mostra linha a linha o que mudou nos ficheiros ainda não adicionados. Útil antes de fazer commit.

### `git branch` — Ramos (branches)
- **`git branch`** — lista os ramos (o atual tem `*`).
- **`git branch nome_do_ramo`** — cria um novo ramo. Útil para experimentar sem estragar o código principal.

### `git checkout` — Mudar de ramo ou restaurar ficheiro
- **`git checkout nome_do_ramo`** — muda para esse ramo.
- **`git checkout -- nome_do_ficheiro`** — descarta alterações nesse ficheiro. *Cuidado: perdes o que não guardaste.*

### `git pull` — Trazer alterações do remoto
- Traz as alterações que estão no GitHub (ou noutro sítio) e junta-as ao teu projeto local.
- *Faz isto antes de começares a trabalhar se alguém mais puder ter alterado o repo.*

### `git push` — Enviar para o remoto
- Depois do commit, **`git push`** envia os teus commits para o GitHub. Fica guardado na nuvem.

---

## Resumo rápido

**Navegação:** `pwd` = onde estou · `ls` = o que há aqui · `cd` = mudar de pasta · `mkdir` = criar pasta

**Git:** `git status` = o que mudou · `git add` = preparar · `git commit` = guardar versão · `git pull` = trazer · `git push` = enviar

---

*Quando tiveres dúvida, experimenta numa pasta de teste. Com o tempo estes comandos ficam naturais.*
