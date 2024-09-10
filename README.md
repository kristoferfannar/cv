# CV

Welcome to my CV repo!

My current CV can be found on [kristoferfannar.github.io/cv](https://kristoferfannar.github.io/cv)

In attempt to move away from overleaf, I've decided to move my cv to my file system, while version controlling it on GitHub.
This allows for keeping track of incremental changes, autocompiling it and having a workflow continuously deploy it on GitHub Pages.

## Setup

There are quite a few steps needed to fully migrate from overleaf to local compilation.

To begin with, you'll need a TeX compiler. I'm using [MacTeX](https://www.tug.org/mactex/), specifically [BasicTeX](https://www.tug.org/mactex/morepackages.html), as its 90MB bundle is quite a lot more appealing than the 5.7GB [real thing](https://www.tug.org/mactex/mactex-download.html).

Really, you only need this for the [latexmk compiler](https://ctan.org/pkg/latexmk/). I didn't bother to find another way to install it, so just go with BasicTeX.

Note that latexmk didn't work for me at first, so I had to update it with [tlmgr](https://tug.org/texlive/tlmgr.html) (after updating tlmgr itself first) until it started working.

```
sudo tlmgr update --self
```

```
sudo tlmgr update latexmk
```

The reason why I use latexmk is that it's recommended by [VimTeX](https://github.com/lervag/vimtex), the vim and neovim latex plugin I'm using.

This plugin is really impressive. In a latex file, simply `:VimtexCompile` and the generated pdf document is opened in your preferred pdf viewer.

Regarding the pdf viewer, I'm using [Sioyek](https://sioyek.info/), and it's very impressive.
VimTeX recommends using zathura, but I had trouble installing it, and once it was installed it couldn't automatically open the pdf file due to some issues with synctex.
Nevermind that, just

```
brew install --cask sioyek
```

The auto-reload feature of Sioyek is super nice, and the setup (so far) more or less identically resembles overleaf.
Only in the comfort of my editor.

Here's a short video of me showcasing my setup:

https://github.com/user-attachments/assets/699affc5-fdc0-424e-8aa6-b1ef31a3ff1e

### External packages

External packages are stored as `.sty` files under `tex/latex/<package>/<package>.sty` in a specific package directory.
For _latexmk_, this package directory can be seen using `tlmgr conf` under `TEXMFHOME` for user specific directory (similar to `TEXMFLOCAL` for system directory or `TEXMFDIST` for distribution wide packages).

For this project, the package directory is [`./latex-packages/`](./latex-packages/), so you'll have to set the environment variable manually:

```bash
# for zsh
echo "export TEXMFHOME=$(pwd)/latex-packages" >> ~/.zshrc && source ~/.zshrc
```

Note that this only works while you're only locally compiling latex for this project. If you're locally compiling latex for other projects, you'll need to use the original `TEXMFHOME`, storing the external libraries used here in a separate file and using a script to ensure they're installed.

#### Installing external packages

Installing packages is often as easy as `sudo tlmgr install <package>`, found using `tlmgr search <package>`. However, sometimes these packages aren't available to the _tlmgr_ directory, meaning that we are required to find and build the `.sty` files on our own.

To do this, we require an `.ins` installer file and `.dtx` documented source file for the package - this can usually be found online. Then, to create the `.sty` file from these files, run:

```
latex <package>.ins
```

Ensuring that both the `.ins` and `.dtx` files are in the same directory, this will generate the `.sty` file required by latexmk.
