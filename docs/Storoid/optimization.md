# Optimizations
[ [ Intro ] ](README.md) -- [ [Add User](user.md) ] -- [ [Create Partition](harddrive.md) ] -- [ [Install & Run Daemon](daemon.md) ] -- [ [**Optimization**](optimization.md) ] -- [ [Monitoring](monitor.md) ]

-----
## Auto-Start Daemon on Boot
- `$ env > ~/.env`
- `$ nano ~/watchdog.sh`

Paste in the following code ([credit](https://docs.storj.io/docs/setting-up-storj-share-on-a-raspberry-pi#section-2-start-storj-share-at-raspberry-pi-boot-time-using-a-startup-script)), and remember to replace `<0bXXX>.json` with your own config file accordingly.
```
#!/bin/bash
. $HOME/.bashrc
. $HOME/.profile
. $HOME/.env
APP=$(ps aux | grep -v grep | grep storjshare)
if [ -z "$APP" ];
then
echo "Restarting daemon"
storjshare daemon
fi
APP=$(ps aux | grep -v grep | grep 'farmer.js --config')
if [ -z "$APP" ];
then
echo "Restarting node"
storjshare start --config $HOME/.config/storjshare/configs/<0bXXX>.json
fi
```
Make the script executable.
- `$ chmod +x ~/watchdog.sh`

Create a Cron job.
- `$ crontab -e`

And append the following:
```
*/5 * * * * $HOME/watchdog.sh
@reboot $HOME/watchdog.sh
```

---
Next: [Monitoring](monitor.md)