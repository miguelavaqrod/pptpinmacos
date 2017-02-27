# pptpinosx
A Sierra+ command line alternative for connecting to legacy systems using PPTP

First of all, I have to say that this method is not from my own. I found it time ago (googling) and I think it is a good idea to save it here. If the owner has something to tell me, just inform me.

I know PPTP is unsecure, but please Apple, let me decide what to do with my computer and where to connect to...

---

Method:

First we create our settings file
```
sudo vi /etc/ppp/peers/MY_PPTP_DOMAIN_I_WANT_TO_CONNECT_TO_OR_WHATEVER_NAME_YOU_CHOOSE
```
Paste the following that I think suits all needs:
```
plugin PPTP.ppp
noauth
# logfile /tmp/ppp.log
remoteaddress THE_DOMAIN_NAME_OR_IP_OF_THE_SERVER_TO_CONNECT_TO
redialcount 1
redialtimer 5
idle 1800
mru 1368
mtu 1368
receive-all
novj 0:0
ipcp-accept-local
ipcp-accept-remote
# noauth
refuse-pap
refuse-chap-md5
user THE_USERNAME
hide-password
mppe-stateless
mppe-128
looplocal
password THE_PASSWORD
nodetach
ms-dns 8.8.8.8
# used in ip-up script
ipparam gwvpn
```
Save and repeat for every server you need to connect to.

I chmod the files to keep them secure...
```
sudo chmod 640 MY_PPTP_DOMAIN_I_WANT_TO_CONNECT_TO_OR_WHATEVER_NAME_YOU_CHOOSE
```
To establish a connection just:
```
sudo pppd call MY_PPTP_DOMAIN_I_WANT_TO_CONNECT_TO_OR_WHATEVER_NAME_YOU_CHOOSE
```
Note:

It does not respond to CTRL+Z or similar... so I kill it from another Terminal window.

Regards.
