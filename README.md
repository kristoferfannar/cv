

# CV

Welcome to my CV repo. In attempt to move away from overleaf, I've decided to move my cv to my file system, while version controlling it on GitHub.

This allows for keeping track of incremental changes, autocompiling it and having a workflow continuously deploy it once I have somewhere to continuously deploy.

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

