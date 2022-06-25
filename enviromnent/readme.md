
#### test env

```
docker run --rm -d  --name ubuntu ubuntu sh -c "while true ; do sleep 100 ; done"

docker build . -t pramodepandit/ubuntu:latest --no-cache --progress plain

docker run -d -p 2022:22 --rm --name webserver pramodepandit/ubuntu 

ssh applmgr@localhost -p 2022

docker run -d -p 2024:22 --rm --name applserver pramodepandit/ubuntu 

ssh applmgr@localhost -p 2024

docker run -d -p 2026:22 --rm --name dbserver pramodepandit/ubuntu 

ssh applmgr@localhost -p 2026

```