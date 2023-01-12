# linbpq-builds
Build pipelines for LinBPQ.

For now, has an action which when manually run, pulls the linbpq source from John's git repo, builds it on Ubuntu amd64, and publishes a single release from it.

That binary currently runs on Ubuntu 22.04.1 LTS amd64 with just one dependency.

To get up and running using this binary:

```shell
sudo apt install libconfig9
wget https://github.com/M0LTE/linbpq-builds/releases/download/release/linbpq
chmod +x linbpq
./linbpq -v
```

The build is run weekly. The pipeline is [here](https://github.com/M0LTE/linbpq-builds/actions/workflows/build-linbpq.yml).

This approach the need to install the i386 architecture and loads of i386 packages on your amd64 box. It also avoids the need to have all of the `-dev` dependencies installed to allow you to build it from source.

I may iterate on this to automate further and bring other tools (e.g. QtTermTCP) and other platforms (e.g. Raspberry Pi) into scope.
