> 启动elasticsearch，调账内存大小

https://hub.docker.com/_/elasticsearch

```shell
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -e ES_JAVA_OPTS="-Xms64m -Xmx512m" elasticsearch:7.6.2
```



> 启动portainer

https://portainer.readthedocs.io/en/latest/deployment.html

```shell
docker run -d -p 9000:9000 -p 8000:8000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer
```

