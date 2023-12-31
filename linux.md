# LINUX

## NETWORKING
* TCP DUMP: ```tcpdump -nqt -s0 -A -i any port 5060 |grep "computer networking" -A 10 -B 10```
* TCP DUMP with portrange: ```tcpdump -nqt -s0 -A -i any -an portrange 1-25```
* Ping with MTU size: ```ping 122.152.145.101 -s 1500```


## ADVANDCE
* Find & Replace: ```find ./hoiio/ -type f -exec sed -i "s/<origin_string>/<new_string>/g" {} +```
* Repeat Command n times: ```for i in {1..10}; do <command>; done```
* curl with digest auth ```curl --digest --user minh:secret https://minh.com/```
* trace: ```last -x```
* investigate: ```grep -iv ': starting\|kernel: .*: Power Button\|watching system buttons\|Stopped Cleaning Up\|Started Crash recovery kernel' /var/log/messages /var/log/syslog /var/log/apcupsd* \| grep -iw 'recover[a-z]*\|power[a-z]*\|shut[a-z ]*down\|rsyslogd\|ups'```
* 10 bigest file: ```du -a /var/log | sort -n -r | head -n 10```

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
* SSH Tunnel


* ```ssh -L local-port:target-host-address:target-host-port remote-host-address```
* ```ssh -L 80 172.16.1.2:8080 minh@1.1.1.1```


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

## IPTABLES
### FLUSH
```
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT

iptables -t nat -F
iptables -t mangle -F
iptables -F
iptables -X
```

```
nft flush ruleset
```

### RESET COUNTER
```
iptables -Z -L -v
```


## OPENSSL
* generate ssl key & cert ```openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout selfsigned.key -out selfsigned.crt```
* print out certificate x509 in text form: ```openssl x509 -text -noout -in github_com.csr```


## OPENVPN3
```
wget https://swupdate.openvpn.net/repos/openvpn-repo-pkg-key.pub
apt-key add openvpn-repo-pkg-key.pub
wget -O /etc/apt/sources.list.d/openvpn3.list https://swupdate.openvpn.net/community/openvpn3/repos/openvpn3-buster.list
apt update
apt install openvpn3
mkdir /etc/openvpn3/client
openvpn3 session-start --config /etc/openvpn3/client/mind.ovpn
openvpn3 sessions-list
openvpn3 session-manage --disconnect  --config /etc/openvpn3/client/mind.ovpn

```

## MACOS X

* Dock Hide Time
```
defaults write com.apple.dock autohide-time-modifier -int 0
killall Dock

defaults delete com.apple.Dock autohide-delay
```
* Startup Volume ```sudo nvram StartupMute=%01```
* Disable Power Button ```defaults write com.apple.loginwindow PowerButtonSleepsSystem -bool yes```

* Mac Name
```
sudo scutil --set HostName <new host name>
sudo scutil --set LocalHostName <new host name>
sudo scutil --set ComputerName <new name>
dscacheutil -flushcache
```

## GIT
```
# track:
git remote add upstream git@github.com:signalwire/freeswitch.git

# Update:
git fetch upstream
git rebase upstream/master
git push
git push --tags

# new branch from tag
git checkout tags/v1.10.11 -b v1.10.11-libre-a

```


