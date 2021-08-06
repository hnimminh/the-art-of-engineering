# LINUX

## NETWORKING
* TCP DUMP: ```tcpdump -nqt -s0 -A -i any port 5060 |grep "computer networking" -A 10 -B 10```
* Ping with MTU size: ```ping 122.152.145.101 -s 1500```


## ADVANDCE
* Find & Replace: ```find ./hoiio/ -type f -exec sed -i "s/<origin_string>/<new_string>/g" {} +```
* Repeat Command n times: ```for i in {1..10}; do <command>; done```
* curl with digest auth ```curl --digest --user minh:secret https://minh.com/```
* trace: ```last -x```
* investigate: ```grep -iv ': starting\|kernel: .*: Power Button\|watching system buttons\|Stopped Cleaning Up\|Started Crash recovery kernel' /var/log/messages /var/log/syslog /var/log/apcupsd* \| grep -iw 'recover[a-z]*\|power[a-z]*\|shut[a-z ]*down\|rsyslogd\|ups'```

## NTP _ CHRONY
```
/etc/chrony.conf - server 192.168.0.51 iburst prefer
chronyc tracking
chronyc source
chronyc sources -v

systemctl restart chronyd ; watch chronyc tracking
/sbin/hwclock --systohc
```

## SSH

# SSH Client Configuration

* Remote Access ```ssh -i ~/.ssh/private.key -p 9022 -oKexAlgorithms=+diffie-hellman-group1-sha1 -c aes256-cbc superadmin@10.10.10.10```

* Sample: ~/.ssh/config
```
Host PREFIX* 172.31.*.*
    Port 11922
    StrictHostKeyChecking no
    IdentitiesOnly yes
    UserKnownHostsFile=/dev/null
    KexAlgorithms +diffie-hellman-group1-sha1
    User minh
    IdentityFile ~/.ssh/minh.general.private
    ProxyJump SSHJUMPPOINT
 ```

## REDIS
* install redis-cli by 1 command ```wget http://download.redis.io/redis-stable.tar.gz && tar xvzf redis-stable.tar.gz && cd redis-stable && make & cp src/redis-cli /usr/bin/```

## SCREEN
* CISCO console connect example ```sudo screen /dev/ttyUSBO 9600```
* Start a new session with session name 	```screen -S <session_name>```
* List running sessions / screens 	```screen -ls```
* Attach to a running session 	```screen -x```
* Attach to a running session with name 	```screen -r <session_name>```
* Detach a running session 	`screen -d <session_name>`
* Kill session ```screen -X -S <session_name> quit


## OPENSSL
* generate ssl key & cert ```openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout selfsigned.key -out selfsigned.crt```
* print out certificate x509 in text form: ```openssl x509 -text -noout -in github_com.csr```

## MACOS X

* Dock Hide Time
```
defaults write com.apple.dock autohide-time-modifier -int 0
killall Dock

defaults delete com.apple.Dock autohide-delay
```
* Startup Volume ```sudo nvram StartupMute=%01```

