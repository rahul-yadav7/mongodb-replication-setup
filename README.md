
## Mongodb Replication



## How to create and setup mongo-replica locally ?

```javascript
$ mongod --port 27018 --dbpath /var/lib/tempmongodb1 --bind_ip localhost,192.168.0.109,192.168.0.117 --replSet rs0
$ mongod --port 27018 --dbpath /var/lib/psreadtestdb --bind_ip 0.0.0.0 --replSet rs0
$ 
$ mongod --port 28001 --dbpath /var/lib/tempmongodb2 --replSet rs0
$ mongod --port 28004 --dbpath /var/lib/tempmongodb5 --replSet rs0

```

## Local Setup (Change Stream)


```javascript
1. mongod --port 28001 --dbpath /home/ongraph/Projects/purespectrum/mongodb/tempmongodb1 --replSet rs0
2. mongod --port 28002 --dbpath /home/ongraph/Projects/purespectrum/mongodb/tempmongodb2 --replSet rs0 
3. mongod --port 28003 --dbpath /home/ongraph/Projects/purespectrum/mongodb/tempmongodb3 --replSet rs0
```

## ON Master


```javascript
config = { _id: "rs0", members:[
        {_id: 0, host: 'localhost:28001'},
        {_id: 1, host: 'localhost:28002'},
        {_id: 2, host: 'localhost:28003'}
    ]
}

config = rs.initiate(config);

```


## On Slave 


```javascript
rs.slaveOk();

config = { _id: "purescore-service", members:[
        {_id: 0, host: 'ip-172-31-16-138.ec2.internal:28000'},
        {_id: 1, host: 'ip-172-31-17-105.ec2.internal:28000'}
    ]
}


```
