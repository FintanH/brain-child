Basic object of `systemd` is a "unit".

Units can be of many types

Most common unit is a `.service`

`systemctl` command manages services

Units are not started automatically at boot by default.
We can enable this behaviour using `systemctl enable`.
Or conversely, `disable`.

3 possible states for a service: `enabled`, `disabled`, or `static`.

`enabled` means it has symlink in a `.wants` directory.
`disabled` means it does not.
`static` means it's missing the `[Install]` section its init script. Static services are usually dependencies of other services.

Most used commands:
```
$ systemctl start [name.service]
$ systemctl stop [name.service]
$ systemctl restart [name.service]
$ systemctl reload [name.service]
$ systemctl status [name.service]
$ systemctl is-active [name.service]
$ systemctl list-units --type service --all
```
`systemd` assumes `.service` as the default so we can drop the suffix.

Other units:

* Target: group of units
* Automount: filesystem auto-mountpoint
* Device: kernel device names, which you can see in sysfs and udev
* Mount: filesystem mountpoint
* Path: file or directory
* Scope: external processes not started by systemd
* Slice: a management unit of processes
* Snapshot: systemd saved state
* Socket: IPC (inter-process communication) socket
* Swap: swap file
* Timer: systemd timer.

Example unit file that executes bash script, `/etc/systemd/system/runme.service`:
```
[Unit]
Description=Cleaning service

[Service]
Type=Simple
ExecStart=/bin/bash /usr/bin/runme.sh

[Install]
WantedBy=multi-user.target
```

