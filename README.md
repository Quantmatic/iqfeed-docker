=======================

Usage
-----

```
docker run -e LOGIN=<your iqfeed login> -e PASSWORD=<your iqfeed password>  -p 9100:9101  quantomatic/iqfeed-latest
```

If you want to build your own copy via the Dockerfile:

1. docker build Dockerfile
2. docker run -e LOGIN=<your iqfeed login> -e PASSWORD=<your iqfeed password> -p 5900:5900 -p 9100:9101 yourNEWimage/name
3. docker exec -it container_name bash
4. run x11vnc and exit container bash
5. on the host run $ vncviewer localhost:5900
6. complete the iqfeed install over vnc
7. docker stop container_name
8. docker committ container_name to yourNEWimage/name

Based on
https://github.com/bratchenko/docker-iqfeed
https://github.com/jaikumarm/docker-iqfeed

However, my image turned out quite a bit smaller, 1.3GB vs 1.8GB

