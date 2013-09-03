---
layout: default
title: Ideation
---

# The flow of information

My friends have friends, and theirs have friends as well.  There are
three types or users:

*  The one who originates the stream
*  The one who receives it, and passes it along
*  The one who don’t have any more friends to share the content with

![tree](/images/ideation-tree1.jpg)

Once files are introduced in the stream by its originator, they are available for all its downstream friends to fetch. When that happens, those files will be available for the next level of friends.
The only operation requiring human intervention is the initial introduction, all the later transmission happen transparently.

**Use case**: We are buddies. You have subscribed to my *alo.media.talks* channel, where I put the recording of talks and I find interesting. You wake up in the morning and you find that you’ve got a couple of video files in your Incoming directory with a conference on Code Optimization totally worth watching. By that time, the friends from the office who subscribed that *alo.media.talks* channel from you already received it as well, as so do their friends.



# Channels
Files must be classified in channels for the system to be useful. Otherwise, it wouldn’t be much more than a program to fill all your storage with random garbage.
*  Files must belong to a channel
*  Only friends subscribing the channel will receive it
*  Users can subscribe as many channels as they want (and their upstream allows)


![tree](/images/ideation-tree2.jpg)


There are slightly more complex scenarios when a user can have, for instance, subscriptions from more than one upstream. In that case, the channels would be aggregated. Any downstream subscriber would perceive all of them as regular channels:

**TODO**: There are a few corner cases to clarify here.

*  Streams should not cycle, it should implement a method of detecting the situation and breaking the cycle.
*  Concurrency would potentially be an issue if a user subscribed the same channel from two different hosts. That situation should also be covered.

![tree](/images/ideation-tree3.jpg)


# Security

Communication between hosts MUST be as secure as possible.

For that purpose each user will have their own 8192 bits asymmetric GPG key. They don’t have to use their own or generate it by hand. The key management and creating will be completely transparent for the user.

Every single byte transmitted between friends will be encrypted with these keys. That implies that friends have to exchange keys. We’ll have to figure out how to ease this process. Ideally it would happen in person over a beer, although that’s not always possible.

The transport will happen through HTTPS. It’s a well known protocol, proxies and filter usually allow it and it provides certain grade of security:

*  The default  443 port will be used unless its indicated otherwise
*  Clients might or might not have an open port
*  TLS will use a 4096 bits RSA key

![security](/images/ideation-security1.jpg)

The exchange of information between friends will always use the GPG keys. That includes commands like “Give me the list of your channels”, “What’s new on the XYZ channels”, or “Send the this file starting at offset 123456789”. Both requests and responses are encrypted with the friend’s key at the other end.

![security](/images/ideation-security2.jpg)

Is it too much to nest a 8192 bits key over a 4096 bits one? Yes, probably it is, but it doesn’t hurt. Also, a cheap modern computer will be able to encode/decode ~20MB/s of this rock solid stream.
