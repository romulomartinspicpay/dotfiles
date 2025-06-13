# README - Gerenciamento de dotfiles do ASDF com GNU Stow

Este documento descreve o fluxo de trabalho para preparar, executar e finalizar a gestão das suas configurações do ASDF usando GNU Stow. Siga os passos abaixo para garantir que seu ambiente seja reproduzível em qualquer máquina.

---

## Pré-requisitos

- **Git**: para clonar seu repositório de dotfiles.
- **asdf**: instalado e configurado no seu sistema.
- **GNU Stow**: instalado via Homebrew ou outro gerenciador (`brew install stow`).

## 1. Antes de rodar o `stow`

1. **Clone o repositório de dotfiles** (caso ainda não tenha feito):

   ```bash
   git clone git@github.com:romulomartinspicpay/dotfiles.git ~/dotfiles
   ```

2. **Verifique os arquivos do ASDF** dentro de `~/dotfiles/asdf`:

   - \`\`: lista de plugins e versões (ex.: `nodejs 18.17.1`, `python 3.11.4`, etc.)
   - \`\` *(opcional)*: configurações do asdf (paths, cache, legacy\_version\_file, etc.)
   - \`\` *(opcional)*: URLs dos plugins a instalar (gerado via `asdf plugin list --urls > plugins.txt`).

3. **Configurar ignorados do Stow** (para pular arquivos `.md`):

   - Crie um arquivo chamado \`\` em `~/dotfiles/asdf/` com o conteúdo:
     ```text
     .*\.md$
     ```

   Isso faz com que quaisquer arquivos Markdown sejam ignorados pelo Stow.

## 2. Executando o `stow`

No diretório raiz do repositório de dotfiles, rode o comando:

```bash
cd ~/dotfiles
stow asdf
```

> Se você não usou `.stow-local-ignore`, pode rodar:
>
> ```bash
> stow --ignore='\.md$' asdf
> ```

Esse comando criará links simbólicos de:

- `~/dotfiles/asdf/.tool-versions` → `~/.tool-versions`
- `~/dotfiles/asdf/.asdfrc`        → `~/.asdfrc`
- e outros arquivos/pastas contidos em `asdf/`.

## 3. Depois de rodar o `stow`

1. **Recarregue as definições do ASDF** no seu shell (caso não esteja no profile):

   ```bash
   source ~/.asdf/asdf.sh
   source ~/.asdf/completions/asdf.bash
   ```

2. **Instale todas as versões definidas** em `.tool-versions`:

   ```bash
   asdf install
   ```

3. **Verifique as versões instaladas**:

   ```bash
   asdf list
   ```

4. **Atualize os shims** (caso adicione novos binários ou atualize versões):

   ```bash
   asdf reshim
   ```

5. **Abra um novo terminal** ou recarregue seu `~/.zshrc` / `~/.bashrc`:

   ```bash
   source ~/.zshrc
   ```

---

## Contribuições e ajustes

- Para adicionar novos plugins, edite `plugins.txt` e execute:

  ```bash
  xargs -L1 asdf plugin add < ~/dotfiles/asdf/plugins.txt
  asdf install
  ```

- Se precisar ajustar configurações do ASDF, edite `~/.asdfrc` dentro do repositório e reaplique o `stow`.

---

> **Dica**: mantenha sempre seu `plugins.txt` e `.tool-versions` sincronizados para que qualquer clone do repositório reproduza fielmente seu ambiente.



