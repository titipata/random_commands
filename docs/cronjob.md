# Running Cronjob

In order to run Cronjob, I have to first edit default editor on my Mac
by adding `export EDITOR="emacs"` to `~/.bash_profile`. In this case, I won't
have to deal with `vi`. I can also use `nano` text editor. However, I got some error
running `nano` recently and it's solved by running [this solution](http://askubuntu.com/questions/90013/how-do-i-enable-syntax-highlighting-in-nano).

```bash
git clone https://github.com/nanorc/nanorc.git
cd nanorc
make install
```

First, start using `Cronjob` by typing

```bash
crontab -e
```

Try adding this lines to the script.

```bash
#!/bin/bash

# add path to cron
PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Users/titipat/anaconda/bin
# running example cron job
30 13 * * * echo "hello, world on $(date)" >> backup.log
```
