# Raspberry

### installing [plex on Ubuntu Mate](http://dev2day.de/pms/pool/main/p/)

```bash
## Install both of this packages
# plexmediaserver-installer
wget http://dev2day.de/pms/pool/main/p/plexmediaserver-installer/plexmediaserver-installer_0.9.16.6.1993-5089475-1~jessie_armhf.deb
# plexmediaserver
wget http://dev2day.de/pms/pool/main/p/plexmediaserver/plexmediaserver_0.9.16.4.1911-ee6e505-2~jessie_all.deb
sudo dpkg -i plex*
```

Sometimes you may run into permissions problems. You can edit the user Plex is running as:
```bash
sudo vim /etc/default/plexmediaserver
# change this line PLEX_MEDIA_SERVER_USER=plex and write your user there
```

### Mount raspberry on the Mac Finder as a Network Drive
```bash
# install Netatalk
sudo apt-get install netatalk
# stop it
sudo /etc/init.d/netatalk stop
# edit the preferences
sudo vim /etc/netatalk/AppleVolumes.default
# in this line you can change the directory and the name it will take
~/      "Home Directory"
# save it and start it again
sudo /etc/init.d/netatalk start
```

### Fix permissions problems on Transmission Web Interface
[http://askubuntu.com/questions/221081/permission-denied-when-downloading-with-transmission-deamon](http://askubuntu.com/questions/221081/permission-denied-when-downloading-with-transmission-deamon)
