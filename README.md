# Docker XAMPP
This Docker image provides an up-and-running PHP development environment based on the [XAMPP stack](https://www.apachefriends.org/index.html). For convenient access to the conatiner, an additional SSH server is available . __Please note that both mySQL and phpMyAdmin use the default XAMPP password settings__.

## Running the image
This image uses the `/www` directory for your project's web content, so you need to mount your working directory from the host into the container:
```
$ docker run --name xampp -p 2222:22 -p 8080:80 -d -v <project-directory>:/www iggyblob/docker-xampp
```

The command above will expose an Apache HTTP server on port `8080` as well as an SSH server on port `2222` .    
Feel free to adapt the ports and/or container name according to your needs.

URL to your project: [http://localhost:8080/www](http://localhost:8080/www)    
XAMPP management interface: [http://localhost:8080/](http://localhost:8080/)

## Additional services

### SSH connection
Please use the default SSH password `root` when connecting to the container.
```
$ ssh root@localhost -p 2222
```

### Mount a bash shell to your container
```
$ docker exec -ti xampp bash
```

### Use XAMPP binaries inside the container
If you need to use the `mysql` client or other binaries provided by the XAMPP package, extend the `PATH` variable inside your container to include the `/opt/lampp/bin` directory.
```
$ export PATH=/opt/lampp/bin:$PATH
```

### Use a custom Apache configuration
In your home directory, create a `my_apache_conf` directory in which you put your custom Apache `.conf` files. They will come into effect upon restarting Apache (see the next section for further information).
```
$ docker run --name xampp -p 2222:22 -p 8080:80 -d -v <project-directory>:/www  -v <project-directory>/my_apache_conf:/opt/lampp/apache2/conf.d iggyblob/docker-xampp
```

### Restarting Apache
If you modify configuration files you'll have to restart Apache:
```
$ docker exec xampp /opt/lampp/lampp restart
```

## Issues
Please report an issue if you run into any problems while using this Docker image.
