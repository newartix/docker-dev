# docker-dev
Docker files and compose to simple run in dev with PhpStorm and on prod. Include mysql, php and nginx, redis and centrifugo.

Expected that you create directories tree as like:
 - your-dev-path
   - docker-dev
     - nginx
       - (common nginx configs)
     - php
       - (php configs)
     - mysql
       - (mysql configs and all your mysql-data)
   - data
     - mysql
       - (mysql presist data)
     - redis
       - (redis persist data)
   - logs
   - projects
     - project1
        - project1.nginx.conf
     - project2
        - project2.nginx.conf

Don't forget add records to C:\Windows\System32\driver\etc\hosts like:
127.0.0.1 yourproject.local

DO NOT USE ZONE .dev, it has issues with HSTS.

Install Docker Desktop, open powershell and type:
cd C:\your-dev-path\docker-dev\ && docker-compose up
