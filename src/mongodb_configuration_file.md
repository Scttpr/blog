# MongoDB configuration file

> [Command line options](https://docs.mongodb.com/manual/reference/program/mongod/#options) documentation and [configuration file](https://docs.mongodb.com/manual/reference/configuration-options/) options

## Use

```shell
mongod --config "/etc/mongod,conf"
mongod -f "/etc/mongod.conf"
```

## Template

```yml
storage:
    dbPath: "/data/db"

systemLog:
    path: "/data/log/mongod.log"
    destination: "file"

net:
    bindIp: "127.0.0.1, 192.168.0.10"
    ssl:
        mode: "requireSSL"
        PEMKeyFile: "/etc/ssl/ssl.pem"
        CAFile: "/etc/ssl/SSLCA.pem"

security:
    keyFile: "/data/keyfile"
    authorization: "enabled"

processManagement:
    fork: true

replication:
    # Replica set options
    replSetName: "my_super_replica_set"
```
