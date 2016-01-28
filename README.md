# nginxPhp
imac下nginx和php
1.安装nginx
brew install nginx
2.启动php-fpm
sudo php-fpm
一般情况下会报错
复制php-fpm.conf.default改为php-fpm.conf
;error_log = log/php-fpm.log
找到这一行
分号去掉
修改路径为一个可写文件，文件名为php-fpm.log
我这里改为error_log = /Users/bruce.wang/Desktop/g-工具/php-fpm.log

3.打开nginx.conf
nginx.conf ：/usr/local/etc/nginx/nginx.conf
开启php的注释，配置好自己的root

location / {
    root   /Users/bruce.wang/Desktop/q-轻app生成器;
    index  index.html index.htm;
 }
location ~ \.php$ {
    fastcgi_pass   127.0.0.1:9000;
    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
    include        fastcgi_params;
}
注意
SCRIPT_FILENAME  /script$fastcgi_script_name;
改为
SCRIPT_FILENAME  $document_root$fastcgi_script_name;

4.开启nginx
sudo nginx
