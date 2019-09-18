# Reminder 

# Table of Contents
1. [Bash shell](#Bash)
2. [Vim](#Vim)
3. [Kafka](#Kafka)
4. [Python](#Python)
5. [GIT](#GIT)
6. [API](#API)
7. [CheatSheet](#CHEATSHEET)
## Bash shell
### Reference
- [The programmer Stone](https://www.datapacrat.com/Opinion/Reciprocality/r0/index.html)
- https://catonmat.net/the-definitive-guide-to-bash-command-line-history
- http://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html
- https://linuxhint.com/30_bash_script_examples/
- https://dev.to/awwsmm/101-bash-commands-and-tips-for-beginners-to-experts-30je#click-click
- https://catonmat.net/bash-one-liners-explained-part-two

### Password generation
- openssl rand -base64 32
- tr -cd '[:alnum:]' < /dev/urandom | fold -w30 | head -n1
- < /dev/urandom tr -dc _A-Z-a-z-0-9 | head -c${1:-32};echo;

### bash history manipulation
- !!:gs/search/replace/
- ^x^y

### Check port open
(timeout 2 bash -c '</dev/tcp/127.0.0.1/17500 && echo PORT OPEN || echo PORT CLOSED') 2>/dev/null
nc -zv kafka02 6667
-z = sets nc to simply scan for listening daemons, without actually sending any data to them
-v = enables verbose mode

## Bash scripting
### default argument
- somecommand ${1:-foo}
- ternaire operator [[ $vartest = "data" ]] && var="iftrue" || var="iffalse"
### check
```
#!/bin/bash
set -eo pipefail
```
### Confirm manipulation
read -n 1 -p "Apply this ? (y/n) " answer
case ${answer:0:1} in
    y|Y )
        do_works
    ;;
    * )
        echo "Cancel"
    ;;
esac

### Color manipulation
```
red=`tput setaf 1`
green=`tput setaf 2`
yellow=`tput setaf 3`
bold=`tput bold`
underline=`tput smul`
reset=`tput sgr0`
echo "${underline}${bold}${red}Start Script ...${reset}"
```
## sed 
### Replace dos to unix
sed -i -e 's/\r$//' myscript.sh

## Certificat
openssl req -new -newkey rsa:2048 -nodes -keyout mydomain.key -out mydomain.csr

## Vim

- :w !sudo tee %
```
 :w = Write a file.
 !sudo = Call shell sudo command.
 tee = The output of the vi/vim write command is redirected using tee.
 % = Triggers the use of the current filename.
 Simply put, the ‘tee’ command is run as sudo and follows the vi/vim command on the current filename given.
 ```
- :s/foo/bar/G
- :r myfile
insert the content of myfile in the open buffer

 ## Kafka
 ### References
 - https://riptutorial.com/fr/apache-kafka/example/27964/kafka-topics
 
 ### Command
 - Topics list:
 ```
 kafka-topics  --zookeeper localhost:2181 --list
 ```
 - Topics list:
 ```
 kafka-topics  --bootstrap-server localhost:9092 --list
 ```
 - Create topics:
 ```
 kafka-topics  --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
 ```
 - Describe topics: 
 ```
 kafka-topics  --zookeeper localhost:2181 --describe --topic test
 ```
 - Change topics: 
 ```
 change configuration
kafka-topics  --zookeeper localhost:2181 --alter --topic test --config max.message.bytes=128000
# add a partition
kafka-topics  --zookeeper localhost:2181 --alter --topic test --partitions 2
```

## Python
### python oneliner 
- urllib.request.urlopen('http://www.python.org/')
- python2 : python -m SimpleHTTPServer 8000
- python3 : python -m http.server 8000 [--bind 127.0.0.1 --directory /tmp/ --cgi 8000]
- debug with breakpoint()


## GIT
- git config --list
- git config --global user.name "John Doe"
- git config --global user.email [jd@polop]


 ## API
 ### https://www.ipify.org/
 Exemple : 
 ```bash
 curl 'https://api.ipify.org?format=json' 
{"ip":"164.128.235.36"}
```
## CheatSheet
- http://overapi.com/javascript
- https://www.debuggex.com/cheatsheet/regex/
- https://marozed.ma/vue-cheatsheet/
- https://vuejs-tips.github.io/vuex-cheatsheet/
- https://yoksel.github.io/flex-cheatsheet/
- https://devhints.io/
- https://raw.githubusercontent.com/sogko/graphql-shorthand-notation-cheat-sheet/master/graphql-shorthand-notation-cheat-sheet.png

## Coding Interview
- https://realpython.com/python-coding-interview-tips/
- https://github.com/lydiahallie/javascript-questions

