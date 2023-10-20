# Reminder 

# Table of Contents
1. [Bash shell](#Bash)
2. [Vim](#Vim)
3. [Kafka](#Kafka)
4. [Python](#Python)
5. [GIT](#GIT)
6. [API](#API)
7. [CheatSheet](#CHEATSHEET)
8. [ffmeg](#FFMEG)
## Bash shell
# Bash string manipulation cheatsheet

<table>
	<tr>
		<th colspan="2">Assignment</th>
	</tr>
	<tr>
		<td>Assign <code>value</code> to <code>variable</code> if <code>variable</code> is not already set, <code>value</code> is returned.<br /><br />Combine with a <code>:</code> no-op to discard/ignore return <code>value</code>.</td>
		<td><code>${variable="value"}</code><br /><code>: ${variable="value"}</code></td>
	</tr>
	<tr>
		<th colspan="2">Removal</th>
	</tr>
	<tr>
		<td>Delete shortest match of <code>needle</code> from front of <code>haystack</code></td>
		<td><code>${haystack#needle}</code></td>
	</tr>
	<tr>
		<td>Delete longest match of <code>needle</code> from front of <code>haystack</code></td>
		<td><code>${haystack##needle}</code></td>
	</tr>
	<tr>
		<td>Delete shortest match of <code>needle</code> from back of <code>haystack</code></td>
		<td><code>${haystack%needle}</code></td>
	</tr>
	<tr>
		<td>Delete longest match of <code>needle</code> from back of <code>haystack</code></td>
		<td><code>${haystack%%needle}</code></td>
	</tr>
	<tr>
		<th colspan="2">Replacement</th>
	</tr>
	<tr>
		<td>Replace first match of <code>needle</code> with <code>replacement</code> from <code>haystack</code></td>
		<td><code>${haystack/needle/replacement}</code></td>
	</tr>
	<tr>
		<td>Replace all matches of <code>needle</code> with <code>replacement</code> from <code>haystack</code></td>
		<td><code>${haystack//needle/replacement}</code></td>
	</tr>
	<tr>
		<td>If <code>needle</code> matches front of <code>haystack</code> replace with <code>replacement</code></td>
		<td><code>${haystack/#needle/replacement}</code></td>
	</tr>
	<tr>
		<td>If <code>needle</code> matches back of <code>haystack</code> replace with <code>replacement</code></td>
		<td><code>${haystack/%needle/replacement}</code></td>
	</tr>
	<tr>
		<th colspan="2">Substitution</th>
	</tr>
	<tr>
		<td>If <code>variable</code> not set, return <code>value</code>, else <code>variable</code></td>
		<td><code>${variable-value}</code></td>
	</tr>
	<tr>
		<td>If <code>variable</code> not set <em>or</em> empty, return <code>value</code>, else <code>variable</code></td>
		<td><code>${variable:-value}</code></td>
	</tr>
	<tr>
		<td>If <code>variable</code> set, return <code>value</code>, else null string</td>
		<td><code>${variable+value}</code></td>
	</tr>
	<tr>
		<td>If <code>variable</code> set <em>and</em> not empty, return <code>value</code>, else null string</td>
		<td><code>${variable:+value}</code></td>
	</tr>
	<tr>
		<th colspan="2">Extraction</th>
	</tr>
	<tr>
		<td>Extract <code>length</code> characters from <code>variable</code> starting at <code>position</code></td>
		<td><code>${variable:position:length}</code></td>
	</tr>
	<tr>
		<td>Return string length of <code>variable</code></td>
		<td><code>${#variable}</code></td>
	</tr>
	<tr>
		<th colspan="2">Escaping</th>
	</tr>
	<tr>
		<td>Single quotes inside a single quoted string</td>
		<td><code>echo 'Don'\''t break my escape!'</code></td>
	</tr>
	<tr>
		<th colspan="2">Indirection</th>
	</tr>
	<tr>
		<td>Return value of variable name held in <code>indirect</code>, else <code>value</code></td>
		<td><code>indirect="apple"</code><br /><code>apple="fruit"</code><br /><code>${!indirect-value}</code></td>
	</tr>
</table>

## Reference

- https://tldp.org/LDP/abs/html/string-manipulation.html
- https://tldp.org/LDP/abs/html/parameter-substitution.html
- https://tldp.org/LDP/abs/html/ivr.html
- Special characters:
	- `*`: https://www.tldp.org/LDP/abs/html/special-chars.html#ASTERISKREF
	- `?`: https://www.tldp.org/LDP/abs/html/special-chars.html#WILDCARDQU
- https://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#tag_18_06_02
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

### Retrieve my IP
- ip=$(hostname --ip-address)
- ip=$(ip route get 1 | awk '{print $NF;exit}')
- curl https://ipinfo.io/ip
- wget -qO- https://ipecho.net/plain ; echo
- dig +short myip.opendns.com @resolver1.opendns.com
- LANG=c ifconfig | grep -B1 "inet addr" |awk '{ if ( $1 == "inet" ) { print $2 } else if ( $2 == "Link" ) { printf "%s:" ,$1 } }' |awk -F: '{ print $1 ": " $3 }'
- http://checkip.amazonaws.com
- ifconfig.me
- stunclient stun.services.mozilla.com
- ip addr show

### AWK tips
- Extract Value beetween tags : echo "asdf \<ip\>test\</ip\> dsaf" | awk -v RS='</?ip>' '!(NR%2)'
  - Result : test

### Check port open
- (timeout 2 bash -c '</dev/tcp/127.0.0.1/17500 && echo PORT OPEN || echo PORT CLOSED') 2>/dev/null
- nc -zv kafka02 6667
   -z = sets nc to simply scan for listening daemons, without actually sending any data to them
   -v = enables verbose mode

### Ping without ping (Test port with no tools)
- timeout 10 true >/dev/tcp/8.8.8.8/53
- timeout 10 true >/dev/tcp/142.250.201.163/80
- timeout 10 true >/dev/tcp/142.250.201.163/809

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

## TLS / Certificats
### CSR : Certificat Server Request
- openssl req -new -newkey rsa:2048 -nodes -keyout mydomain.key -out mydomain.csr
- openssl req -new -newkey rsa:2048 -nodes -keyout server.key -out server.csr -subj "/C=*Country*/ST=*State or Province*/L=*Locality or City*/O=*Company*/OU=*Organizational unit*/CN=*Common Name*"

### Check certificat / private key / csr
- openssl rsa -noout -modulus -in mykey.key | openssl md5 > key.mod
- openssl req -noout -modulus -in mycsr.csr | openssl md5 > csr.mod
- openssl x509 -noout -modulus -in mycert.crt | openssl md5 > cert.mod
- diff3 key.mod cert.mod csr.mod
Result must be the same.

- https://www.sysnove.fr/blog/2016/03/utilisation-pratique-letsencrypt-acme-tiny.html

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
### python pip
- pip install --download mypackage
- pip install --no-index --find-links `pwd` mypackage
- python pip-10.0.1-py2.py3-none-any.whl/pip install --no-index pip-10.0.1-py2.py3-none-any.whl

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
- https://kubernetes.io/fr/docs/reference/kubectl/cheatsheet/

## Coding Interview
- https://realpython.com/python-coding-interview-tips/
- https://github.com/lydiahallie/javascript-questions

## FFMEG
- Convertion en mp3 d'une autre source : ffmpeg -i audio.aac -acodec libmp3lame audio.mp3
