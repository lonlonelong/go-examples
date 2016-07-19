Example code: https://github.com/ibmendoza/go-examples/blob/master/docker/helloworld.go

**Run on bare metal**

http://localhost:8080/sdf

Output:

```
Hi there, I love sdf! From: 192.168.0.121 fe80::4c99:7e59:9085:6f87 
fe80::989d:fb29:9977:774c 
fe80::b4ed:4d9b:91e4:d9cd 
192.168.56.1 
192.168.99.1 
192.168.0.121 
```

**With docker run**

First, build the Docker image using the Dockerfile below

```
FROM scratch

COPY helloworld /helloworld

EXPOSE 8080

CMD ["/helloworld"]
```

- upload helloworld Linux binary to Turnkey Linux VM at /home/docker/ipaddr
- chmod +x helloworld
- docker build -t helloworld
- docker images
- docker -p 8080:8080 run helloworld

Output:

```
Hi there, I love sdf! From: 172.17.0.2 172.17.0.2 
```

docker network inspect bridge

```
[
    {
        "Name": "bridge",
        "Id": "74e8a07f9cd363b9a5896b7007062bb9c7dffe611724a98aa0040e56738e3fbc",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.0/16"
                }
            ]
        },
        "Internal": false,
        "Containers": {
            "ec3ba4c654a94529c15ec192f4bee018fa6c108f9bbc0b154c752701196bfb32": {
                "Name": "adoring_babbage",
                "EndpointID": "b75edb592858c44500c2013a29aaf567894558ded02b2244c7edc54763ffc3dc",
                "MacAddress": "02:42:ac:11:00:02",
                "IPv4Address": "172.17.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]
```

