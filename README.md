# Test Dockerfile by Serverspec

## Docker

- base image, [dhrp/sshd](http://docs.docker.io/en/latest/examples/running_ssh_service/)

## ssh

#### ssh from vagrant VM


```
# Dockerfile
# ssh login from vagrant without no password
RUN useradd vagrant
RUN mkdir -p /home/vagrant/.ssh
RUN chown vagrant /home/vagrant/.ssh
RUN chmod 700 /home/vagrant/.ssh

# ADD /home/vagrant/.ssh/id_rsa.pub /home/vagrant/.ssh/authorized_keys
# -> Not found
ADD ./id_rsa.pub /home/vagrant/.ssh/authorized_keys
RUN chown vagrant /home/vagrant/.ssh/authorized_keys
RUN chmod 700 /home/vagrant/.ssh/authorized_keys
```

Run container with portforward setting, 0.0.0.0:7654->22/tcp

```
docker run -p 7654:22 -d serverspec /usr/sbin/
```

Login with ssh

```
ssh vagrant@localhost -p 7654
```
