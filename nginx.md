# nginx配置

#### HTTP配置

```
# Virtual Host configuration for example.com
#
# You can move that to a different file under sites-available/ and symlink that
# to sites-enabled/ to enable it.
#
server {
        listen 80;
        listen [::]:80;

        server_name www.xxx.cn xxx.cn;

        root /home/xxx/www/xxx/;
        index index.php index.html index.htm index.shtml;

        # 重定向
        return 301 https://www.xxx.cn$request_uri;

        location / {
                # try_files $uri $uri/ =404;
                ssi on;
                ssi_silent_errors on;
                ssi_types text/shtml;
                try_files $uri $uri/ /index.php?$args;
        }

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_connect_timeout 300;
                fastcgi_send_timeout 300;
                fastcgi_read_timeout 300;
                fastcgi_buffers 8 128k;

                # With php7.0-cgi alone:
                # fastcgi_pass 127.0.0.1:9000;
                # With php7.0-fpm:
                fastcgi_pass unix:/run/php/php7.0-fpm.sock;
                # fastcgi_index  index.php;
                # fastcgi_param  SCRIPT_FILENAME  $document_root/$fastcgi_script_name;
                # include        fastcgi_params;
        }
}
```

#### HTTPS配置

```
# Virtual Host configuration for example.com
#
# You can move that to a different file under sites-available/ and symlink that
# to sites-enabled/ to enable it.
#
server {
        listen 443;

        server_name xxx.com;

        root /home/xxx/www/xxx/;
        index index.php index.html index.htm index.shtml;

        ssl on;
        ssl_certificate   /etc/nginx/cert/xx.cn.pem;
        ssl_certificate_key  /etc/nginx/cert/xx.cn.key;
        ssl_session_timeout 5m;
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers on;

        location / {
                # try_files $uri $uri/ =404;
                ssi on;
                ssi_silent_errors on;
                ssi_types text/shtml;
                try_files $uri $uri/ /index.php?$args;
        }

        # 站内站从定向
        location /school/ {
                index index.php;
                try_files $uri $uri/ /school/index.php?$args;
        }

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_connect_timeout 300;
                fastcgi_send_timeout 300;
                fastcgi_read_timeout 300;
                fastcgi_buffers 8 128k;

                # With php7.0-cgi alone:
                # fastcgi_pass 127.0.0.1:9000;
                # With php7.0-fpm:
                fastcgi_pass unix:/run/php/php7.0-fpm.sock;
                # fastcgi_index  index.php;
                # fastcgi_param  SCRIPT_FILENAME  $document_root/$fastcgi_script_name;
                # include        fastcgi_params;
        }
}
```

#### 站内站

```
location /school/ {
        index index.php;
        try_files $uri $uri/ /school/index.php?$args;
}
```

#### PC端自动重定向到移动端，静态文件不重定向

```
if ($document_uri ~* .(jpg|png|gif|css|js)) {
        set $isStatic static;
}

if ($http_user_agent ~* "(Android|iPhone|Windows Phone|UC|Kindle)") {
        set $isPC "$isStatic,mobile";
}

if ($isPC = ,mobile) {
        return 302 https://m.xxx.cn$request_uri;
}
```

#### 站内站重定向

```
location /info/ {
    if ($request_uri ~ (/info([\S\s]*))) {
            set $results_uri $2;
    }
    return 301 https://www.xxx.cn/news$results_uri;
    index index.php;
    try_files $uri $uri/ /info/index.php?$args;
}
```