title: Fix systax error in Wordpress inside docker
date: 2016-04-30 10:55:11

---

1. Shutdown your droplet and make a snapshot. Always remember to make a snapshot before you make any big changes.

2. Execute your wordpress docker image again.

```
    $ docker ps
        CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                      NAMES
        2a646cb51226        wordpress           "/entrypoint.sh apach"   4 months ago        Up 2 minutes        0.0.0.0:80->80/tcp, 0.0.0.0:8080->80/tcp   wordpress_wordpress_1
        6057a85dc452        mariadb             "/docker-entrypoint.s"   4 months ago        Up 2 minutes        3306/tcp                                   wordpress_wordpress_db_1
```

<!--more-->

Remember the container ID to wordpress and execute

    $ docker exec -it <container ID> vi <full path to the file with syntax error>

If you see this error:

        exec: "vi": executable file not found in $PATH

execute

        $ docker exec -it <container ID> bash
        # apt-get update
        # apt-get install vim

After it finished without error, u can just edit the fill inside the container whatever you like.
