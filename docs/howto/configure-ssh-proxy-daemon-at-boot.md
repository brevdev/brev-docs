# How To

## Configure ssh proxy to start at Boot

Make sure that you have installed the [cli](https://github.com/brevdev/brev-cli/)

### Mac OS

Add the following configuration to <!-- todo what location -->

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>dev.brev</string>
    <key>ProgramArguments</key>
    <array>
        <string>/opt/brev/bin/brev</string>
        <string>run-tasks</string>
    </array>
    <key>KeepAlive</key>
    <true/>
</dict>
</plist>

```


### Linux

Add the the following configuration to `/etc/systemd/user/brev.service`
or `$HOME/.config/systemd/user/brev.service`

```ini
[Install]
WantedBy=multi-user.target

[Unit]
Description=Brev SSH Proxy Daemon
After=systend-user-sessions.service

[Service]
Type=simple
ExecStart=/opt/brev/bin/brev run-tasks
Restart=always
```

enable and start the daemon by running :
```shell
$ systemctl --user enable brev
$ systemctl --user start brev
```


check status with

```
$ systemctl --user status brev

```

and you should see an output similar to:

```shell
● brev.service - Brev SSH Proxy Daemon
     Loaded: loaded (/etc/xdg/systemd/user/brev.service; disabled; vendor preset: enabled)
     Active: active (running) since Tue 2022-01-18 19:03:49 PST; 3s ago
   Main PID: 264331 (brev)
      Tasks: 11 (limit: 47870)
     Memory: 8.8M
        CPU: 59ms
     CGroup: /user.slice/user-1000.slice/user@1000.service/app.slice/brev.service
             └─264331 /opt/brev/bin/brev run-tasks

Jan 18 19:03:49 pop-os systemd[4294]: Started Brev SSH Proxy Daemon.
Jan 18 19:03:51 pop-os brev[264331]: 2022/01/18 19:03:51 creating new ssh config
Jan 18 19:03:51 pop-os brev[264331]: 2022/01/18 19:03:51 ensuring has include
```
