---
layout: post
title: Zookeeper's MyID
---

Original Thread on StackOverflow: [Zookeeper error: Cannot open channel to X at election address](https://stackoverflow.com/questions/30940981/zookeeper-error-cannot-open-channel-to-x-at-election-address)

## Problem ##

One of the Zookeepers came back with this error in the file `/opt/zookeeper/zookeeper-X.X.X/bin/zookeeper.out`
```
2019-03-20 20:37:51,117 [myid:1] 
- WARN  [QuorumPeer[myid=1]/0:0:0:0:0:0:0:0:2183:QuorumCnxManager@400] 
- Cannot open channel to 2 at election address /XXX.XXX.XXX.XXX:3888
```

Restarting the instance didn't work. The configuration files on all instances `/opt/zookeeper/zookeeper-X.X.X/conf/zoo.cfg` looked normal.

## Solution ##

The StackOverflow thread listed above suggested that `myid` is not being set properly, therefore the "bad" instance had an identity crisis and insisted that it cannot be `server.1` because `server.1` already exists.

Went on and did a Unix `find` to locate the file that will set `myid`: `/opt/zookeeper/data/myid`

Once giving `/opt/zookeeper/data/myid` to the one that matched in `/opt/zookeeper/zookeeper-X.X.X/conf/zoo.cfg`, e.g. `2` and restarting that Zookeeper instance resolves the issue.