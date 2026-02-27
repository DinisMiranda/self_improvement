# Prompts que deste (explicação simples)

*Isto é um resumo do que pediste noutro repositório. Como foi noutro projeto, não tens os ficheiros à frente — está descrito de forma geral: o tipo de coisas que pediste.*

---

## Nesta sessão

Pediste duas coisas:

1. Como tornar um repositório **"profissional"**.
2. Uma lista de todos os prompts que tinhas feito, num ficheiro.

---

## O que foi feito noutro repo

### Organização
- Estrutura clara: pastas para código, configuração e scripts bem separadas.
- Ficheiro **.gitignore** para o Git não guardar ficheiros desnecessários ou com dados sensíveis (ex.: palavras-passe).

### Configuração
- A aplicação a ler definições de um ficheiro de config (ex.: .toml).
- Um ficheiro **de exemplo** para outros copiarem.
- O ficheiro verdadeiro com segredos **fora do Git**.
- Tudo isto documentado no README.

### Base de dados e dependências
- Ligação à base de dados (MySQL) num sítio só, reutilizável.
- Projeto a usar **Poetry** para instalar dependências e correr scripts (em vez de truques manuais).
- Instruções para instalar o Poetry quando não estava instalado.

### Testes
- Testes automáticos (**Pytest**) para funções importantes: carregar a config (casos bons e maus) e funções que criam dados de exemplo.
- Tipos no código consistentes (ex.: `list` em vez de `List` em versões antigas).

### Aspecto profissional do projeto
- **pyproject.toml** completo (autores, licença, etc.).
- Documentação e comentários em inglês.
- Cada função com uma descrição clara (**docstrings**): o que faz, o que recebe, o que devolve.

### CI e cobertura
- Testes a correr sozinhos no **GitHub Actions**.
- Medir a **cobertura** dos testes (que percentagem do código está testada); em alguns módulos o objetivo era 100%.

### GitHub
- Ficheiros como **CODEOWNERS** e **Dependabot** para manter dependências atualizadas.
- Comandos para definir a descrição e os tópicos do repositório no GitHub.

### “Realmente profissional”
No fim pediste ficheiros que projetos sérios costumam ter:

| Ficheiro / coisa | Para quê |
|------------------|----------|
| SECURITY.md | Como reportar falhas de segurança |
| CONTRIBUTING.md | Como contribuir para o projeto |
| CHANGELOG | Alterações por versão |
| Badges no README | Testes, licença, etc. |
| Ruff (linter) | Formatação e qualidade do código |
| Templates no GitHub | Abrir bugs e pedidos de funcionalidades |

---

## Em resumo

No outro repo pediste: **organização**, **config segura**, **testes**, **documentação**, **automação no GitHub** e ficheiros que tornam o projeto mais fácil de manter e de partilhar.

Podes usar estas ideias em qualquer projeto parecido.
