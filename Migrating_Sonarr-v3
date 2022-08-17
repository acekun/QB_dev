# Migrating to Sonarr v3 from v2 in Sonarr
This guide assumes using either Debian or Ubuntu. You must have screen installed, as well as wget or curl. Assumption is that your pwd is ``~``.

Start at: ``cd ~``

Stop Sonarr Service ``sudo systemctl stop sonarr@yourusernamehere``

Disable Sonarr Service (don't worry, we'll fix this later) ``sudo systemctl disable sonarr@yourusernamehere``

Grab the update: ``wget http://download.sonarr.tv/v3/phantom-develop/3.0.3.913/Sonarr.phantom-develop.3.0.3.913.linux.tar.gz``
If you prefer curl: ``curl -O -L http://download.sonarr.tv/v3/phantom-develop/3.0.3.913/Sonarr.phantom-develop.3.0.3.913.linux.tar.gz``

Untar: ``tar xvf Sonarr.*.tar.gz``

Copy old config: ``cp -a ~/.config/NzbDrone ~/.config/Sonarr``

Delete old Sonarr install: ``sudo rm -rf /opt/Sonarr``

Copy new Sonarr install: ``sudo mv Sonarr /opt/``

Own the Sonarr install: ``sudo chown -R yourusernamehere /opt/Sonarr``

Edit the service to know about the new install: ``sudo nano /etc/systemd/system/sonarr@.service``

### [sonarr@.service](https://gist.githubusercontent.com/brettpetch/d7903b175662795c8642eb2344e1f144/raw/7e26c61451d29a37845d46b440d8e351e1289e83/sonarr@.service)
```
[Unit]
Description=nzbdrone
After=syslog.target network.target

[Service]
Type=forking
KillMode=process
User=%i
ExecStart=/usr/bin/screen -f -a -d -m -S nzbdrone mono /opt/Sonarr/Sonarr.exe -nobrowser
ExecStop=-/bin/kill -HUP
WorkingDirectory=/home/%i/

[Install]
WantedBy=multi-user.target
```

### Renabling services: 
Refresh services (that blow-in-cartridge feel): ``sudo systemctl daemon-reload``

Re-enable Sonarr service (we're in the home stretch): ``sudo systemctl enable sonarr@yourusernamehere``

Startup Sonarr again (yee-haw): ``sudo systemctl start sonarr@yourusernamehere``

Try going to your sonarr install at swizzin(dot)tld/sonarr and see if it's working...

Setup normally. You'll realize that your Ombi install broke, so you'll need to tell it you've updated to v3.

Don't bork it too hard... do not disable with box either... it'll remove it from the swizzin main page.
