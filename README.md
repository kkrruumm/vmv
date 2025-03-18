# vmv
Mullvad client installer for Void Linux (Void MullVad)

This is a highly temporary and scuffed solution.

There is no guarantee that this will even work for you.

Requires glibc.

# Features
Install, update, and remove the Mullvad client

# Instructions

Installation:
```
git clone https://github.com/kkrruumm/vmv
chmod +x vmv
doas ./vmv install
Done.
```

Removal:
```
doas ./vmv remove
Done.
```

Update:
```
doas ./vmv install
Done.
```

# Thanks to:
https://github.com/loukamb/void-mullvad

I rewrote this in shell script specifically just to have a shell script version.

# Notes

The Mullvad daemon will mount v1 net-cls, which can create breakage if you run your system in pure v2 (unified) cgroups mode.

The solution to this is to mount net-cls elsewhere- the location is arbitrary, the Mullvad daemon has an environment variable you can set to tell it where to mount, and can be set by modifying the ``exec`` line in the ``/etc/sv/mullvad/run`` script:

``exec env TALPID_NET_CLS_MOUNT_DIR="/opt/net-cls-v1" /usr/bin/mullvad-daemon -v --disable-stdout-timestamps``

Again, the location you choose is arbitrary, but ``/opt/net-cls-v1`` is sane enough.
