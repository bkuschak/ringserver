## Installation as a systemd service

### Build and install

First build and install ringserver with the defaults. This will install 
ringserver executable, a default configuration file /etc/ringserver.conf, and
a systemd service file /etc/systemd/system/ringserver.service

```
make
sudo make install
```

At this point the files are installed but the service is not yet activated. You
may make any changes to the configuration files before continuing:

```
/etc/ringserver.conf
/etc/systemd/system/ringserver.service
```

### Configuration

Edit /etc/ringserver.conf if you want to change any of the defaults, including
ring size and storage location.  Ringserver is configured to store its data in 
/ringserver. By default this is a 128 MB ring size.

For embedded systems with flash filesystem storage it might be best to store 
the ring on a ramdisk instead. Make the ramdisk slightly larger than the ring
size. For example:

Add to /etc/fstab:
```
tmpfs  /ringserver  tmpfs  rw,nosuid,nodev,size=129m   0  0
```

Mount the ramdisk:
sudo mkdir -p /ringserver
sudo mount /ringserver

### Run as a service

To activate the systemd serivce to run ringserver automatically at boot, and
to start it immediately:

```
sudo make activate
```

To deactivate the service for any reason:

```
sudo make activate
```

