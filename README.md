# pony

Local File-Based Password, API Key, Secret, Recovery Code Store Backed By GPG

```console
$ pony -h
NAME:
   pony - Local File-Based Password, API Key, Secret, Recovery Code Store Backed By GPG

USAGE:
   pony [global options] command [command options] [arguments...]
   
VERSION:
   v0.1.0
   
AUTHOR(S):
   @jfrazelle <no-reply@butts.com> 
   
COMMANDS:
   add, save    Add a new secret
   delete       Delete a secret or a specific recovery code
   get          Get the value of a secret
   list, ls     List all secrets
   update       Update a secret
   help, h      Shows a list of commands or help for one command
   
GLOBAL OPTIONS:
   --debug, -d              run in debug mode
   --file, -f "~/.pony"     file to use for saving encrypted secrets
   --gpgpath "~/.gnupg"     filepath used for gpg keys
   --help, -h               show help
   --generate-bash-completion   
   --version, -v            print the version

```

### Best Practices

You should namespace the keys for your secrets like the following:

```console
$ pony add com.twitter.frazelledazzell.token KJDHJKFHDSBJDF
# GPG Passphrase for key "Jess Frazelle <butts@systemd.lol>": 

$ pony add com.github.jfrazelle.token LKJHSDLFKJDHF
# GPG Passphrase for key "Jess Frazelle <butts@systemd.lol>": 

# if a key ends with `.recovery`
# we assume it is a list of comma seperated 
# strings that are recovery codes
$ pony add com.github.devnull@butts.com.recovery we0wk4,osdknew,4fd9kw,03jfn23,sduj39s
# GPG Passphrase for key "Jess Frazelle <butts@systemd.lol>": 

$ pony ls
# GPG Passphrase for key "Jess Frazelle <butts@systemd.lol>": 

KEY                                     VALUE
com.aws.amazon.prod.key                 KSUIIUEJDMSDBSDJFOFR
com.aws.amazon.prod.secret              skljdUYGjsndhfjjiosjdfgr/HKKSU
com.github.devnull@butts.com.recovery   we0wk4,osdknew,4fd9kw,03jfn23,sduj39s
com.github.jfrazelle.token              LKJHSDLFKJDHF
com.twitter.frazelledazzell.token       KJDHJKFHDSBJDF
```