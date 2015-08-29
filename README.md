# multiroom-shairport
Distribute airplay audio stream synchronous to multiple shairport-sync hosts

## Draft
The basic idea is that you have a airplay source which sends it's audio to one shairport host. That host will redistribute the signal to multiple shairport-sync hosts to get synchronous multiroom audio.

###Traffic Flow
Airplay source -> shairport -> fifo -> forked-daap -> shairport-sync


##Install Client (Rasbian)
```
$ git clone --recursive https://github.com/copyrights/multiroom-shairport.git
$ cd multiroom-shairport/shairport-sync/
$ sudo apt-get install autoconf libtool libdaemon-dev libasound2-dev libpopt-dev libconfig-dev avahi-daemon libavahi-client-dev libssl-dev
$ autoreconf -i -f
$ ./configure --with-alsa --with-avahi --with-ssl=openssl --with-systemv
$ make
$ sudo make install 
$ sudo update-rc.d shairport-sync defaults 90 10

```

In /etc/init.d/shairport-sync change
```
        start-stop-daemon --start --quiet --pidfile $PIDFILE --exec $DAEMON -- -d || return 2
```

to

```
start-stop-daemon --start --quiet --pidfile $PIDFILE --exec $DAEMON -- -d -a "RoomName" -- -d hw:0 -t hardware -c PCM || return 2
```

reboot or start the service and your done.
