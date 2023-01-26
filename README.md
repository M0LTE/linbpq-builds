# linbpq-builds
Build pipelines for LinBPQ.

For now, builds the linbpq source on Ubuntu amd64 into a binary, and publishes a release in this repo from it.

That binary currently runs on Ubuntu 22.04.1 LTS amd64 with just one dependency, `libconfig9`.

To get up and running using this binary on Ubuntu amd64:

```shell
sudo apt install libconfig9
wget https://github.com/M0LTE/linbpq-builds/releases/download/release/linbpq
chmod +x linbpq
./linbpq -v
sudo mkdir /usr/bin/linbpq
sudo mv linbpq /usr/bin/linbpq/
```

This approach avoids the need to install the i386 architecture and loads of i386 packages on your amd64 box. It also avoids the need to have all of the `-dev` dependencies installed to allow you to build it from source.

I may iterate on this to automate further and bring other tools (e.g. QtTermTCP) and other platforms (e.g. Raspberry Pi) into scope.

No attempt is made to retain previous releases - only the latest release is retained currently.

## Auto-start

```shell
sudo sh -c 'echo "[Unit]
After=network.target

[Service]
ExecStart=/usr/bin/linbpq/linbpq
WorkingDirectory=/usr/bin/linbpq
Restart=always

[Install]
WantedBy=multi-user.target" > /etc/systemd/system/linbpq.service'
sudo systemctl enable linbpq
```

and after you have written a config file to `/etc/bpq32.cfg`, e.g.

```shell
sudo sh -c 'echo "SIMPLE
LOCATOR=none
NODECALL=N0CALL
PORT
ENDPORT" > /etc/bpq32.cfg'
```

symlink it to `/etc`:

```shell
sudo ln -s /etc/bpq32.cfg /usr/bin/linbpq/bpq32.cfg
```

then start the service:

```shell
sudo systemctl start linbpq
```
