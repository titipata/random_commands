[back to home](../README.md)

# Cowsay on Mac terminal

See blog post in Thai [here](http://tupleblog.github.io/cowthink-vader/).
First, you have to download Homebrew, in case you use OSX

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Then, you can use `brew` to install as follows

```bash
brew install cowsay
brew install fortune
```

Now, you can put this line in `.bash_profile` or just run it on terminal.

```bash
fortune | cowthink -f vader
```

(**note**, you can list version of cowsay by using `cowsay -l`)
