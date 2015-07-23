# redis-work


ilk çıktı 
redis$  redis-cli -h localhost -p 26379 info                                                
# Server
redis_version:2.8.17
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:447fbed5d78be577
redis_mode:sentinel
os:Darwin 14.4.0 x86_64
arch_bits:64
multiplexing_api:kqueue
gcc_version:4.2.1
process_id:21338
run_id:633903e096583d8846dea970ae8808b951b0ffa7
tcp_port:26379
uptime_in_seconds:24
uptime_in_days:0
hz:11
lru_clock:11623026
config_file:/Users/volkan/project/redis/redis-sentinel.conf

# Sentinel
sentinel_masters:0
sentinel_tilt:0
sentinel_running_scripts:0
sentinel_scripts_queue_length:0

ilk master eklemesini yapıyoruz
redis-cli -h localhost -p 26379 SENTINEL monitor mymaster 127.0.0.1 6381 2

log:
[21534] 24 Jul 00:22:07.005 # Sentinel runid is 5d0ff4c16b809ea969ac60c254b8efc88d7157ac
[21534] 24 Jul 00:26:13.519 # +monitor master mymaster 127.0.0.1 6381 quorum 2
[21534] 24 Jul 00:26:13.543 * +slave slave 127.0.0.1:6380 127.0.0.1 6380 @ mymaster 127.0.0.1 6381
[21534] 24 Jul 00:26:13.543 * +slave slave 127.0.0.1:6379 127.0.0.1 6379 @ mymaster 127.0.0.1 6381


➜  redis$  redis-cli -h localhost -p 26379 info                                      
# Server
redis_version:2.8.17
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:447fbed5d78be577
redis_mode:sentinel
os:Darwin 14.4.0 x86_64
arch_bits:64
multiplexing_api:kqueue
gcc_version:4.2.1
process_id:21534
run_id:5d0ff4c16b809ea969ac60c254b8efc88d7157ac
tcp_port:26379
uptime_in_seconds:436
uptime_in_days:0
hz:14
lru_clock:11623603
config_file:/Users/volkan/project/redis/redis-sentinel_26379.conf

# Sentinel
sentinel_masters:1
sentinel_tilt:0
sentinel_running_scripts:0
sentinel_scripts_queue_length:0
master0:name=mymaster,status=ok,address=127.0.0.1:6381,slaves=2,sentinels=1

➜  redis$  redis-cli -h localhost -p 26379 info                                      
# Server
redis_version:2.8.17
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:447fbed5d78be577
redis_mode:sentinel
os:Darwin 14.4.0 x86_64
arch_bits:64
multiplexing_api:kqueue
gcc_version:4.2.1
process_id:21534
run_id:5d0ff4c16b809ea969ac60c254b8efc88d7157ac
tcp_port:26379
uptime_in_seconds:537
uptime_in_days:0
hz:11
lru_clock:11623704
config_file:/Users/volkan/project/redis/redis-sentinel_26379.conf

# Sentinel
sentinel_masters:1
sentinel_tilt:0
sentinel_running_scripts:0
sentinel_scripts_queue_length:0
master0:name=mymaster,status=ok,address=127.0.0.1:6381,slaves=2,sentinels=2


Master redis 6381 Bağlantıyı koparınca ;
➜  redis  redis-cli -h localhost -p 26379 info
# Server
redis_version:2.8.17
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:447fbed5d78be577
redis_mode:sentinel
os:Darwin 14.4.0 x86_64
arch_bits:64
multiplexing_api:kqueue
gcc_version:4.2.1
process_id:21534
run_id:5d0ff4c16b809ea969ac60c254b8efc88d7157ac
tcp_port:26379
uptime_in_seconds:648
uptime_in_days:0
hz:12
lru_clock:11623815
config_file:/Users/volkan/project/redis/redis-sentinel_26379.conf

# Sentinel
sentinel_masters:1
sentinel_tilt:0
sentinel_running_scripts:0
sentinel_scripts_queue_length:0
master0:name=mymaster,status=ok,address=127.0.0.1:6380,slaves=2,sentinels=2

sentinel logları:
[21534] 24 Jul 00:30:00.842 * +sentinel sentinel 127.0.0.1:26380 127.0.0.1 26380 @ mymaster 127.0.0.1 6381
[21534] 24 Jul 00:32:08.339 # +sdown master mymaster 127.0.0.1 6381
[21534] 24 Jul 00:32:08.399 # +odown master mymaster 127.0.0.1 6381 #quorum 2/2
[21534] 24 Jul 00:32:08.399 # +new-epoch 1
[21534] 24 Jul 00:32:08.399 # +try-failover master mymaster 127.0.0.1 6381
[21534] 24 Jul 00:32:08.400 # +vote-for-leader 5d0ff4c16b809ea969ac60c254b8efc88d7157ac 1
[21534] 24 Jul 00:32:08.402 # 127.0.0.1:26380 voted for 5d0ff4c16b809ea969ac60c254b8efc88d7157ac 1
[21534] 24 Jul 00:32:08.460 # +elected-leader master mymaster 127.0.0.1 6381
[21534] 24 Jul 00:32:08.460 # +failover-state-select-slave master mymaster 127.0.0.1 6381
[21534] 24 Jul 00:32:08.517 # +selected-slave slave 127.0.0.1:6380 127.0.0.1 6380 @ mymaster 127.0.0.1 6381
[21534] 24 Jul 00:32:08.517 * +failover-state-send-slaveof-noone slave 127.0.0.1:6380 127.0.0.1 6380 @ mymaster 127.0.0.1 6381
[21534] 24 Jul 00:32:08.584 * +failover-state-wait-promotion slave 127.0.0.1:6380 127.0.0.1 6380 @ mymaster 127.0.0.1 6381
[21534] 24 Jul 00:32:09.419 # +promoted-slave slave 127.0.0.1:6380 127.0.0.1 6380 @ mymaster 127.0.0.1 6381
[21534] 24 Jul 00:32:09.419 # +failover-state-reconf-slaves master mymaster 127.0.0.1 6381
[21534] 24 Jul 00:32:09.483 * +slave-reconf-sent slave 127.0.0.1:6379 127.0.0.1 6379 @ mymaster 127.0.0.1 6381
[21534] 24 Jul 00:32:10.469 * +slave-reconf-inprog slave 127.0.0.1:6379 127.0.0.1 6379 @ mymaster 127.0.0.1 6381
[21534] 24 Jul 00:32:10.546 # -odown master mymaster 127.0.0.1 6381
[21534] 24 Jul 00:32:11.552 * +slave-reconf-done slave 127.0.0.1:6379 127.0.0.1 6379 @ mymaster 127.0.0.1 6381
[21534] 24 Jul 00:32:11.608 # +failover-end master mymaster 127.0.0.1 6381
[21534] 24 Jul 00:32:11.608 # +switch-master mymaster 127.0.0.1 6381 127.0.0.1 6380
[21534] 24 Jul 00:32:11.608 * +slave slave 127.0.0.1:6379 127.0.0.1 6379 @ mymaster 127.0.0.1 6380
[21534] 24 Jul 00:32:11.609 * +slave slave 127.0.0.1:6381 127.0.0.1 6381 @ mymaster 127.0.0.1 6380
[21534] 24 Jul 00:32:41.634 # +sdown slave 127.0.0.1:6381 127.0.0.1 6381 @ mymaster 127.0.0.1 6380


6381 portlu redis ayağa kalkınca gidip master'a slave oluyor...
[21534] 24 Jul 00:34:17.836 * +convert-to-slave slave 127.0.0.1:6381 127.0.0.1 6381 @ mymaster 127.0.0.1 6380

Havuza yeni bir redis slave olarak ekledim (6382);
[21534] 24 Jul 00:36:02.714 * +slave slave 127.0.0.1:6382 127.0.0.1 6382 @ mymaster 127.0.0.1 6380

Son eklediğim hariç bütün redisleri kapattım. Son eklenen redis master yapıldı ve sistem çalışmaya devam ediyor.

En son olarak kapattığım bütün redisleri ayağa kaldırdım. Daha önce master olanlar otomatik slave yapıldı.

[21534] 24 Jul 00:38:35.634 * +slave slave 127.0.0.1:6380 127.0.0.1 6380 @ mymaster 127.0.0.1 6382
[21534] 24 Jul 00:38:35.635 * +slave slave 127.0.0.1:6381 127.0.0.1 6381 @ mymaster 127.0.0.1 6382
[21534] 24 Jul 00:38:35.635 * +slave slave 127.0.0.1:6379 127.0.0.1 6379 @ mymaster 127.0.0.1 6382
[21534] 24 Jul 00:39:05.664 # +sdown slave 127.0.0.1:6379 127.0.0.1 6379 @ mymaster 127.0.0.1 6382
[21534] 24 Jul 00:39:05.664 # +sdown slave 127.0.0.1:6380 127.0.0.1 6380 @ mymaster 127.0.0.1 6382
[21534] 24 Jul 00:39:05.664 # +sdown slave 127.0.0.1:6381 127.0.0.1 6381 @ mymaster 127.0.0.1 6382
[21534] 24 Jul 00:40:18.532 # -sdown slave 127.0.0.1:6379 127.0.0.1 6379 @ mymaster 127.0.0.1 6382
[21534] 24 Jul 00:40:20.241 # -sdown slave 127.0.0.1:6380 127.0.0.1 6380 @ mymaster 127.0.0.1 6382
[21534] 24 Jul 00:40:21.183 # -sdown slave 127.0.0.1:6381 127.0.0.1 6381 @ mymaster 127.0.0.1 6382
[21534] 24 Jul 00:40:28.437 * +convert-to-slave slave 127.0.0.1:6379 127.0.0.1 6379 @ mymaster 127.0.0.1 6382
[21534] 24 Jul 00:40:30.180 * +convert-to-slave slave 127.0.0.1:6380 127.0.0.1 6380 @ mymaster 127.0.0.1 6382




