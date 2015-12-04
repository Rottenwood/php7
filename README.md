## Docker container with Ubuntu and PHP7-fpm

First, build docker image:
`sudo docker build -t rottenwood/php7 .`

Then run it:
`sudo docker run -d --name="php7" rottenwood/php7`

Container with php-fpm will be started and you can then connect to it with nginx like this:

server {
	listen 80;
    server_name your-server-name.net;
    
    location / {
        fastcgi_pass   YOUR_IP:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }

    error_log /var/log/nginx/error.log;
    access_log /var/log/nginx/access.log;
}
