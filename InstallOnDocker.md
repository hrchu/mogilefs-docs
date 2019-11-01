
Install on Docker 
==============================
In this instruction, we will setup a mogilefs cluster for test.

Fetch images
```
docker pull jeffutter/mogile-node
docker pull jeffutter/hrchu/mogile-moji
```

Run images
```
docker run -d -p 7500:7500 --name mogile-node jeffutter/mogile-node
docker run -t -d -p 7001:7001 --name mogile-tracker --link mogile-node:mogile-node hrchu/mogile-moji
sudo echo 172.17.0.2 mogile-node | sudo tee -a /etc/hosts
```

Test
```
telnet localhost 7001, 7500
```

Note that we have following configuration by default:
* domain: testdomain
* class: testclass1, testclass2
