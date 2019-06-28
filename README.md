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
 
 ##Kafka
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

 ## API
 ### https://www.ipify.org/
 Exemple : 
 ```curl 'https://api.ipify.org?format=json' 
{"ip":"164.128.235.36"}
```
