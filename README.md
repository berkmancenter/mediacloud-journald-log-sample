Sample Ubuntu 20.04 journald logs used for testing.

To recreate:

```bash
host$ vagrant up
host$ vagrant ssh

guest$ sudo bash
guest# mkdir -p /var/log/journal/
guest# chown root:systemd-journal /var/log/journal/
guest# service systemd-journald restart
guest# sleep 3
guest# journalctl --header | grep -q 'File path' || { echo "journalctl doesn't appear to work."; exit 1; }
guest# mkdir -p /vagrant/var/log/journal/
guest# rm -rf /vagrant/var/log/journal/*
guest# cp -R /var/log/journal/* /vagrant/var/log/journal/
guest# mv /vagrant/var/log/journal/$(ls /vagrant/var/log/journal) /vagrant/var/log/journal/$(cat /vagrant/etc/machine-id)
guest# exit
guest$ exit

host$ vagrant destroy -f
```

