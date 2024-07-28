# ~/.dotfiles

## 🏡 powered by [chezmoi](https://chezmoi.io)

Welcome home! This repository contains my personal configuration files and scripts for setting up a customized development environment. The setup is designed to work on both macOS and Linux systems.

## What it does

This repo is a way for me to quickly configure a new machine with the tools I use daily.

Here are the tools it installs and configures:

- 🍏 Compatible with macOS and Ubuntu
- 📁 Dotfile Manager: [🏡 Chezmoi](https://chezmoi.io)
- 📦 Package Manager: [🍺 Homebrew](https://brew.sh)
- 💲 Terminal: [⚡️ Hyper](https://hyper.is/)
- 💅 Theme: [powerlevel10k](https://github.com/romkatv/powerlevel10k), [glow](https://github.com/charmbracelet/glow)
- 🔌 Plugins: [zsh-autocomplete](https://github.com/marlonrichert/zsh-autocomplete)
- 🧠 Local Generative AI: [Ollama](https://ollama.com/) (adds `ask` and `chat` aliases)
- 🐍 Python: [Poetry](https://python-poetry.org/)
- 🌐 Node: [nvm](https://github.com/nvm-sh/nvm), [bun](https://bun.sh/)

There's actually a lot more stuff that you can find listed in the [Brewfile](./dot_dotfiles/brew/Brewfile). You should consider forking this repo and make it your own before installing, as you may not want to use all the stuff I'm using.

## Installation

To set up my dotfiles on your system, run the following command:

```sh
sh -c "$(curl -fsLS https://raw.githubusercontent.com/benvilliere/dotfiles/HEAD/dot_dotfiles/install)"
```

**Note:** You may want to fork this repo and make it your own. Simply replace `benvilliere` with your own username to make it work the same way.

## Commands

This dotfile setup comes with a minimalist yet powerful `dotfile` commandlet written in bash. You can browse the underlying [functions here](./dot_dotfiles/functions).

- Save and apply any updates made to the local dotfiles:

```sh
dotfile save
```

- Pull the latest changes from github and apply them to the local environment:

```sh
dotfile update
```

- Open the source code of this repo to customize it:

```sh
dotfile edit
```

- Run any executable (`chmod +x`) file located within ~/.dotfiles like so:

```sh
dotfile run <script_name>
```

At the moment, only two scripts are available:

- `install`: Idempotent install script used to setup a new machine
- `uninstall`: Script that uninstalls `chezmoi`, its files, and all the dotfiles added by this repository. **Note:** it won't uninstall brew or other brew installed packages.

You can easily add more scripts as you see fit.

## Making it your own

The organization is fairly straightforward and I'm trying to keep it as minimalistic and catered to my needs as possible. If you plan on using it, I would highly recommend you fork this repo and adjust it to your own liking.

First, make sure you're familiar with the core [🏡 Chezmoi](https://chezmoi.io) concepts.

The _TLDR;_ is that it checks out the desired dotfiles repo in `~/.local/share/chezmoi` (that's the standard location). That's the standard location where the source of the dotfiles setup lies on your system.

From there, as soon as you run `chezmoi apply`, it will copy the contents to your home folder `~/` (`$HOME`). It can apply all sorts of transformations for you (the most obvious one is renaming `dot_file` to `.file`), it also comes with a templating system and utilities to leverage password managers and much much more. I'm not leveraging many of its features yet.

I have organized the repo like so:

- `./dot_dotfiles/*` will be copied on your machine to `~/.dotfiles/*` on your system
- `./dot_dotfile` will be copied to `~/.dotfile` on your machine
- Upon installation, a single line is being added to your `~/.zshrc` file: `source "${HOME}/.dotfile"` which will load all the stuff that's needed (more explanations below)
- Whenever you open your terminal, your `~/.zshrc` file gets automatically loaded; in turn, the `~/.dotfile` gets loaded as well. In it, we load the `aliases`, `exports`, `functions`, `plugins` and `styles` located under `~/.dotfiles`.
- Additionally, all files within `~/.dotfiles/modules/*` get sourced recursively. It makes it very convenient to add vendor/tool-specific aliases and functions and much more scalable and easy to maintain.

You can declare `dotfile_*` functions which will become automatically available to the `dotfile <function_suffix>` CLI tool.

Example:

```sh
# -- modules/your-module/functions (or any other name for that matter)
#!/bin/zsh

function dotfile_example() {
  echo "Do something useful"
}
```

Allows you to run:

```sh
dotfile example # > Do something useful
```

Likewise, add and `chmod +x` any script within `~/.dotfiles` to make it callable via `dotfile run xxx`.

That's pretty much all there is to it!

## (Incomplete) list of everything that's installed

Because I'm strictly using Homebrew as my package manager, the comprehensive list of things that are installed on the machine is easily available in the [Brewfile](./dot_dotfiles/brew/Brewfile), but I thought it'd be great to list them out for future reference:

- [gitleaks](https://github.com/gitleaks/gitleaks): Protect and discover secrets using Gitleaks 🔑

- [pre-commit](https://pre-commit.com/#install): A framework for managing and maintaining multi-language pre-commit hooks.

Bear with me, I'll add more as I go.

## Roadmap

Features I'm looking to add in the near future:
[ ] Move all contents to a sub directory
[ ] Add tests suite using bats-core
[ ] Run tests run within a Docker image
[ ] Add linting script
[ ] Add secrets leaking check
[ ] Add a Github workflow with code checks

## Contributing

If you find any issues or have suggestions for improvements, feel free to open an issue or submit a pull request. Contributions are welcome!

## License

This repository is licensed under the MIT License. See the [LICENSE](./LICENSE) file for more details.
