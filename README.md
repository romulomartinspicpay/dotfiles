# dotfiles

Repositório com meus dotfiles para configurar rapidamente um novo ambiente de desenvolvimento.

## Estrutura do repositório

```text
dotfiles/
├── alacritty/
│   └── .config/alacritty/
├── asdf/
│   ├── .tool-versions
│   ├── .asdfrc
│   └── plugins.txt
├── lvim/
│   └── .config/lvim/
├── p10k/
│   └── .p10k.zsh
├── tmux/
│   └── .tmux.conf
├── zsh/
│   ├── .zshrc
│   └── .zshenv
└── README.md
```

## Pré-requisitos

Antes de aplicar os dotfiles, certifique-se de ter instalado em sua máquina:

- **Git**
- **GNU Stow** (`brew install stow`)
- **Alacritty**
- **asdf** (gerenciador de versões)
- **LunarVim**
- **Powerlevel10k**
- **tmux**
- **Zsh**

## Instalação e configuração

1. **Clone o repositório**:

   ```bash
   git clone https://github.com/romulomartinspicpay/dotfiles.git ~/dotfiles
   cd ~/dotfiles
   ```

2. **Gerencie links simbólicos com Stow**:

   - Para aplicar todos os pacotes:
     ```bash
     stow alacritty asdf lvim p10k tmux zsh
     ```
   - Se desejar ignorar arquivos Markdown:
     ```bash
     stow --ignore='\.md$' alacritty asdf lvim p10k tmux zsh
     ```

3. **Instale plugins e versões do asdf**:

   ```bash
   asdf plugin add $(awk '{print $1}' asdf/plugins.txt)
   asdf install
   ```

4. **Recarregue o shell**:

   ```bash
   exec $SHELL
   ```

## Descrição dos pacotes

- **alacritty/**: customizações do terminal Alacritty (`.config/alacritty/alacritty.yml`).
- **asdf/**: arquivo `.tool-versions` com versões fixas e `plugins.txt` para repositório de plugins.
- **lvim/**: configurações do LunarVim (`.config/lvim/config.lua`).
- **p10k/**: tema Powerlevel10k (`.p10k.zsh`).
- **tmux/**: configuração do tmux (`.tmux.conf`).
- **zsh/**: inicialização e ambiente Zsh (`.zshrc`, `.zshenv`).

## Contribuições

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues e pull requests.

## Licença

Este projeto está licenciado sob [MIT License](LICENSE).

