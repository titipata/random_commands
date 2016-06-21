[back to home](../README.md)

# Homebrew

Homebrew is a nice package management system for OS X. This is also the
one that I'm currently using. Homebrew installation is very easy,
you can see it on Homebrew [web page](http://brew.sh/). It is also open-source which
you can find it on [Github](https://github.com/Homebrew/homebrew).

To install brew, simply do as following

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

There are a tons of good packages that you can install e.g.
`youtube-dl`, `vim`, `emacs`, `git` and so on

Some useful `brew` commands includes

```bash
brew update # update to newest version of Homebrew
brew upgrade # upgrade installed packages
brew list # list installed packages
brew uninstall <package_name>
brew cleanup # remove outdated
```
