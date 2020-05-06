# telegraf_ipmi
Telegraf with built in IPMItool


Sample Compose file:
```
version: '2'
services:
  telegraf:
    environment:
      INFLUXDB_HOST: <influxdb_host>
      INFLUXDB_NAME: <influxdb_name>
      INFLUXDB_USER: <influx_user_with_write_access>
      INFLUXDB_PASSWORD: <influx_password>
      HOST_MOUNT_PREFIX: /hostfs
      HOST_ETC: /hostfs/etc
    image: <name_of_your_telegraf_image>
    stdin_open: true
    tty: true
    volumes:
    - /var/run/docker.sock:/var/run/docker.sock:ro
    - /sys:/rootfs/sys:ro
    - /proc:/rootfs/proc:ro
    - /etc:/rootfs/etc:ro
    - /:/hostfs:ro
    stdin_open: true
```
another
```
version: '2'
services:
  telegraf:
    mem_limit: 16777216
    image: pockost/telegraf-rancher
    environment:
      HOST_ETC: /hostfs/etc
      HOST_MOUNT_PREFIX: /hostfs
      INFLUXDB_HOST: http://influxdb:8086
      INFLUXDB_NAME: my_infuxdb_dbname
      INFLUXDB_PASSWORD: my_infuxdb_password
      INFLUXDB_USER: my_infuxdb_username
      HOST_SYS: /hostfs/sys
      HOST_PROC: /hostfs/proc
    stdin_open: true
    volumes:
    - /var/run/docker.sock:/var/run/docker.sock:ro
    - /sys:/rootfs/sys:ro
    - /proc:/rootfs/proc:ro
    - /etc:/rootfs/etc:ro
    - /:/hostfs:ro
    tty: true
```      
