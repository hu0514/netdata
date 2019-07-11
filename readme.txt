docker run -d \
    --network host \
    -v /data/netdata/:/etc/netdata/python.d/ \
    -v /proc:/host/proc:ro \
    -v /var/run/docker.sock:/var/run/docker.sock:rw \
    --cap-add SYS_PTRACE \
    --security-opt apparmor=unconfined \

    netdata/netdata

要点：
/etc/netdata/python.d 存放外部插件配置 比如mysql redis nginx等官网有相关配置
    