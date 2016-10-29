# lua_nginx

Инструкция по установке
Установим компилятор lua (версии 2.0 или 2.1)

Скачаем luaJit и соберем его
make && sudo make install


Для сборки nginx с nginx devel kit необходим http_rewrite_module, а тот с свою очередь требует библиотеку pcre. Поэтому установим ее
sudo apt-get update
sudo apt-get install libpcre3 libpcre3-dev


Скачаем зависимые модули и сам nginx
nginx devel kit 
nginx lua module 
nginx 

Сконфигурируем и установим nginx
export LUAJIT_LIB=/usr/local/lib // путь к библиотеке lua
export LUAJIT_INC=/usr/local/include/luajit-2.1 //путь к luaJit

./configure 
--prefix=/etc/nginx 
--sbin-path=/usr/sbin/nginx
--conf-path=/etc/nginx/nginx.conf 
--error-log-path=/var/log/nginx/error.log
--http-log-path=/var/log/nginx/access.log 
--pid-path=/var/run/nginx.pid 
--lock-path=/var/run/nginx.lock
--http-client-body-temp-path=/var/cache/nginx/client_temp 
--http-proxy-temp-path=/var/cache/nginx/proxy_temp 
--http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp 
--http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp
--http-scgi-temp-path=/var/cache/nginx/scgi_temp 
--user=nginx 
--group=nginx  
--with-ld-opt="-Wl,-rpath,/path/to/lua/lib" // путь к библиотеке Lua
--add-module=/path/to/ngx_devel_kit //путь к nginx devel kit
--add-module=/path/to/lua-nginx-module // путь к nginx lua module
--without-http_gzip_module

make -j2
sudo make install