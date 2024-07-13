# ~/.dotfiles

## 🏡 powered by [chezmoi](https://chezmoi.io)

Welcome home! This repository contains my personal configuration files and scripts for setting up a customized development environment. The setup is designed to work on both macOS and Linux systems.

## What it does

This repo is a way for me to quickly configure a new machine with the tools I use daily.

Here are the tools it installs and configures:

- 🍏 Compatible with macOS and Ubuntu
- 📁 Dotfile Framework: [🏡 Chezmoi](https://chezmoi.io)
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

```sh
dotfile save
```

Saves and applies any updates made to the local dotfiles.

```sh
dotfile update
```

Pulls the latest changes from github and applies them to the local environment.

```sh
dotfile edit
```

Opens the source code of this repo so that you can customize it.

```sh
dotfile run
```

You can run any executable file located within ~/.dotfiles like so:

```sh
dotfile run <script_name>
```

At the moment, only two scripts are available by default:

- `install`: Idempotent install script used to setup a new machine
- `uninstall`: Script that uninstalls `chezmoi`, its files, and all the dotfiles added by this repository. **Note:** it won't uninstall brew or other brew installed packages.

## Making it your own

The organization is fairly straightforward and I'm trying to keep it as minimalistic and catered to my needs as possible. If you plan on using it, I would highly recommend you fork this repo and adjust it to your own liking.

I have organized the repo like so:

- `./dot_dotfiles/*` will be copied on your machine to `~/.dotfiles/*` on your system
- `./dot_dotfile` will be copied to `~/.dotfile` on your machine
- Upon installation, a single line is being added to your `~/.zshrc` file: `source "${HOME}/.dotfile"` which will load all the stuff that's needed (more explanations below)
- Whenever you open your terminal, your `~/.zshrc` file gets automatically loaded; in turn, the `~/.dotfile` gets loaded as well. In it, we load the `aliases`, `exports`, `functions`, `plugins` and `styles` located under `~/.dotfiles`.
- Additionally, all files within `~/.dotfiles/modules/*` get sourced recursively. It makes it very convenient to add vendor/tool-specific aliases and functions and much more scalable and easy to maintain.

You can declare `dotfile_*` functions which will become automatically available to the `dotfile <function_suffix>` cli tool.

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

## Contributing

If you find any issues or have suggestions for improvements, feel free to open an issue or submit a pull request. Contributions are welcome!

## License

This repository is licensed under the MIT License. See the [LICENSE](./LICENSE) file for more details.
