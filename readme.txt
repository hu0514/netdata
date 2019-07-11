docker run -d \
    --network host \
    -v /data/netdata/python.d/:/etc/netdata/python.d/ \
    -v /proc:/host/proc:ro \
    -v /var/run/docker.sock:/var/run/docker.sock:rw \
    --cap-add SYS_PTRACE \
    --security-opt apparmor=unconfined \
    netdata/netdata

要点：
/etc/netdata/python.d 存放外部插件配置 比如mysql redis nginx等官网有相关配置

mysql:
    不使用配置文件
    create user 'netdata'@'localhost';
    grant usage on *.* to 'netdata'@'localhost';
    flush privileges;
    使用配置文件 
    /etc/netdata/python.d目录下添加mysql.conf文件    

nginx:
    nginx.conf添加
        location /stub_status {
                stub_status on;
                access_log off;
                #allow 127.0.0.1;
                #deny all;
        } 


php:
    nginx.conf添加
        location /status {
                include fastcgi_params;
                fastcgi_pass 127.0.0.1:9000;
                fastcgi_param SCRIPT_FILENAME $fastcgi_script_name;
        }               