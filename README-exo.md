# Running ELK on exoscale with the docker toolbox
by twitter://MBuffenoir

## Create instance

    docker-machine create --driver exoscale \
        --exoscale-api-key $CLOUDSTACK_KEY \
        --exoscale-api-secret-key $CLOUDSTACK_SECRET_KEY \
        --exoscale-instance-profile small \
        --exoscale-disk-size 10 \
        --exoscale-security-group elk \
        elk

## Add security rules with Exoscale API

    cs authorizeSecurityGroupIngress protocol=TCP startPort=5600 endPort=5600 securityGroupName=elk cidrList=0.0.0.0/0
    cs authorizeSecurityGroupIngress protocol=UDP startPort=5000 endPort=5000 securityGroupName=elk 'usersecuritygrouplist[0].account'=$EXOSCALE_ACCOUNT_EMAIL 'usersecuritygrouplist[0].group'=swarm

## Launch ELK

    docker-machine scp -r conf-files/ elk:
    eval $(docker-machine env elk)
    docker-compose -f docker-compose-ubuntu.yml up -d

## Test it with a web server:

    eval $(docker-machine env --swarm swarm-queen)
    docker run -d --name nginx-with-syslog --log-driver=syslog --log-opt syslog-address=udp://$(docker-machine ip elk):5000 -p 80:80 nginx:alpine
