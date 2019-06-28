# Reminder 

## Bash shell
### Reference
- https://catonmat.net/the-definitive-guide-to-bash-command-line-history
- http://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html
- https://linuxhint.com/30_bash_script_examples/
- https://dev.to/awwsmm/101-bash-commands-and-tips-for-beginners-to-experts-30je#click-click
- https://catonmat.net/bash-one-liners-explained-part-two

### Password generation
- openssl rand -base64 32
- tr -cd '[:alnum:]' < /dev/urandom | fold -w30 | head -n1
### bash history manipulation
- !!:gs/search/replace/
- ^x^y

## Bash scripting
### default argument
- somecommand ${1:-foo}

## Vim

- :w !sudo tee %
```
 :w = Write a file.
 !sudo = Call shell sudo command.
 tee = The output of the vi/vim write command is redirected using tee.
 % = Triggers the use of the current filename.
 Simply put, the ‘tee’ command is run as sudo and follows the vi/vim command on the current filename given.
 ```
 
 ## API
 ### https://www.ipify.org/
 Exemple : 
 ```curl 'https://api.ipify.org?format=json' 
{"ip":"164.128.235.36"}
```
