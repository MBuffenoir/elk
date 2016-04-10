# elk
A compose file to quickly setup and ELK stack

Try it out with:

    $ docker-machine create -d virtualbox elk
    $ eval $(docker-machine env elk)
    $ git clone git@github.com:MBuffenoir/elk.git
    $ cd elk
    $ docker-compose up -d
    $ echo "Hi syslog" | nc -u $(docker-machine ip elk) 5000
