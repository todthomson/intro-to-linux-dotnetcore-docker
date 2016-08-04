# Building applications with Docker

## Intro to problem

### Linking

```bash
    docker build . -t rethinklogs:latest
```

```bash
    docker run -itd -p 5000:5000 --link rethinkdb --name=rethinklogs rethinklogs
```

### Networking

Create backend network:

```docker network create backend```

Run Rethinklogs app (and RethinkDb) --todo add volume

```docker run -itd -p 8080:8080 -p 28015:28015 -p 29015:29015 --net=backend -v ~/rethinkdb_data --name=rethinkdb rethinkdb```

```docker run -itd -p 80:5000 --net=backend --name=rethinklogs rethinklogs
```



## Compose

## Distrubuted

## swarm 


## Reference to Wolfy's repo
