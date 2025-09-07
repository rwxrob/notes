> Disregarding any current bugs with routing, etc, which can be fixed, the issue is more fundamental
>
>Moblink connections as of right now only allow the stream to go through. A moblink-only BELABOX is crippled: no DNS, no NTP, no BB remote, no updates, no Internet for the hotspot(s). If you have a bunch of real modems and 1 moblink, you'll probably be fine. But as you switch the balance towards more connections via moblink and less direct modem connections, chances are that you'll experience degraded operation more and more often. That could mean the hotspot losing Internet connectivity, the remote disconnecting, DNS not working, the remote and updates never working because that one real modem you have blocks NTP and the TLS certs don't validate, etc.
>
>And the main appeal of moblink is to move a whole bunch of connections onto it, otherwise for 1-2 devices you might as well just have regular wifi connections. So it doesn't really make sense to say hey we support moblink, start using it when chances are that you'll have a degraded experience, and weird difficult to troubleshoot issues. This is on top of the other limitations of putting all your eggs into one WiFi network basket, and using phones instead of modems, which in my experience just doesn't work well anywhere with a warm climate
>
>And moblink was designed for a different use case, I'm not going to go to Erik like hey can we add a TCP proxy, and a DNS resolver, and maybe an NTP forwarder, etc (rationalirl)

I have been saying since people started hounding me about Moblin that the Moblin community does not fit my usage for the following obvious reasons that rationalirl also calls out:

- Moblin *requires* an iPhone
- Phones are notoriously bad at overheating
- Moblin phones require a reliable local wifi router (subject to interference) to work at all
- Phones have notoriously horrible antennas making them useless when signal is limited
- Moblink sucks when a struggling device is mixed in (Starlink with periodic trees)
- Phone data is usually automatically deprioritized unlike dedicated data plans
- You cannot easily get a different sim card for a phone in different areas like you can a modem
- Mobile hotspot modems have ethernet connections that are not affected by interference
- Mobile hotspot modems almost always have mimo antenna extension options