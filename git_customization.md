[back to home](README.md)

# Set up Git

Once you have package management system e.g. Homebrew on MacOSX.
You can do `brew install git` in order to install `git`.
Follow this [link](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control)
for more information. You can set up few information using `git config`

```bash
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

# Git completion

This is a short documentation how to download git completion bash.
It makes life a lot easier when you tab and it auto-fills your commands.

First is to load `git-completion.bash`:

```bash
curl https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh -o ~/.git-prompt.sh
curl -OL http://github.com/git/git/raw/master/contrib/completion/git-completion.bash
```

Then change the name of `git-completion` to `.git-completion` as follows

```bash
mv ~/git-completion.bash ~/.git-completion.bash
```

# Show Git Branch in Terminal (Mac OSX)

To show Git branch in Terminal, add these lines to `.bash_profile`
in order to add color to your bash.

```bash

# color constant
GREEN=$(tput setaf 2)
YELLOW=$(tput setaf 3)
LIME_YELLOW=$(tput setaf 190)
POWDER_BLUE=$(tput setaf 153)
CYAN=$(tput setaf 6)
WHITE=$(tput setaf 7)
BOLD=$(tput bold)
NORMAL=$(tput sgr0)

source ~/.git-prompt.sh

if [ -f ~/.git-completion.bash ]; then
    source ~/.git-completion.bash
    export PS1='\W\[${LIME_YELLOW}\]$(__git_ps1 "(%s)")\[${NORMAL}\] > '
fi
```


For those who has no color `tput colors` give you `8`, use this instead

```bash
if [ -f ~/.git-completion.bash ]; then
    source ~/.git-completion.bash
    export PS1='\W$(__git_ps1 "(%s)") > '
fi
```

# Git Alias

This is the way that we can use some `alias` for Git.

```bash
git config --global alias.logg "log --graph --decorate --oneline --abbrev-commit --all"
```
