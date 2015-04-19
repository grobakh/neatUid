# neatUid
### Clean and simple time-based Unique Id generator
neatUid uses Date.getTime() to eliminate single machine creation conflict.

It applies small random seed to timestamp
1. Better conflict-proof generation
2. Сamouflage sequental nature of increasing ms in time.

##### Output samples:
```
1v3grha41ly
gvnzto7lpy
2a197ak4er
2vawtlektv
35xqmqtt2x
```

##### Comparisson with uuid and sequencers.
`UUID('a8098c1a-f86e-11da-bd1a-00112444be1e')`
UUID objects according to RFC 4122 contains time-stamp, possible MAC, and huge amount of random.
It is possible to create objects with uuid on UI and store them without any conflict on DB in several threads and DB instances.

`Sequnce('1','2','3'...)`
Sequnce integers are DB generated. It is possible to create ids of entities only with DB and only on single instance.
They are sequental, so they are predictable. Users can see this progression in URLs and use it.
For example: mysite.com/user/1, mysite.com/user/2, mysite.com/user/888 - so we have 888 users and can iterate them.

##### Time-stamp non-destructive encoding
neatUid shifts random seed to 10^13 and apply that seed to the timestamp.
So it is possible to get back creation time by next expression:
`new Date(parseInt('xxxxxxxxxx', 36) % Math.pow(10,13))`
