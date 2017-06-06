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
https://github.com/bratchenko/docker-iqfeed and 
https://github.com/jaikumarm/docker-iqfeed

However, my image turned out quite a bit smaller, 1.3GB vs 1.8GB

### Python example ###
```
""
Created on Sun Apr  9 16:16:04 2017
@author: github.com/Quantmatic
"""
import json
import docker
import time

client = docker.APIClient(base_url='unix://var/run/docker.sock', version='auto')

for line in client.pull('quantomatic/iqfeed-latest', stream=True):
    print(json.dumps(json.loads(line), indent=4))

port_bindings = {9101: 9100}
host_config = client.create_host_config(
    port_bindings=port_bindings,
)
ports = [9101]
container = client.create_container(
    image='quantomatic/iqfeed-latest',
    ports=ports,
    host_config=host_config,
    environment={'LOGIN': '12345','PASSWORD': '12345'},
    name='iqfeed_docker',
)
print(container)
client.start(container)
print 'Starting docker container....'
time.sleep(8)
```

