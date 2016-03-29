[back to home](README.md)

# Show Github Branch in Terminal (Mac OSX)

First is to load `git-completion.bash`:

```bash
curl https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh -o ~/.git-prompt.sh
curl -OL http://github.com/git/git/raw/master/contrib/completion/git-completion.bash
```

Then change the name of `git-completion` to `.git-completion`:

```bash
mv ~/git-completion.bash ~/.git-completion.bash
```

Then add these lines to `.bash_profile` in order to add color to your bash.

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
