1: Build the image executor

    docker build --rm -t azkaban-exec:0.1.0-SNAPSHOT -t azkaban-exec:latest .

2: Build the image webserver

    docker build --rm -t azkaban-web:0.1.0-SNAPSHOT -t azkaban-web:latest .

3: Start containers

    docker-compose up -d

![](https://raw.githubusercontent.com/parisgo/docker-azkaban/master/docs/images/Capture00.JPG)

4: Copy and initialize database (azkaban-db / create.all.sql)

    docker cp create.all.sql azkaban-mysql:/
    mysql -uroot -ptest azkaban < create.all.sql

5: Access the web UI :
[https://127.0.0.1:8443](https://127.0.0.1:8443)  
username: azkaban  
password: azkaban

![](https://raw.githubusercontent.com/parisgo/docker-azkaban/master/docs/images/Capture01.JPG)

6: Create project for test

    #command.job
    type=command
    command=echo 'hello azk'

![](https://raw.githubusercontent.com/parisgo/docker-azkaban/master/docs/images/Capture02.JPG)

![](https://raw.githubusercontent.com/parisgo/docker-azkaban/master/docs/images/Capture03.JPG)