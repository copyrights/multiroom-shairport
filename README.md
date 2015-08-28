# multiroom-shairport
Distribute airplay audio stream synchronous to multiple shairport-sync hosts

## Draft
The basic idea is that you have a airplay source which sends it's audio to one shairport host. That host will redistribute the signal to multiple shairport-sync hosts to get synchronous multiroom audio.

###Traffic Flow
Airplay source -> shairport -> fifo -> forked-daap -> shairport-sync


