# linbpq-builds
Build pipelines for LinBPQ.

For now, has an action which when manually run, pulls the linbpq source from John's git repo, builds it on Ubuntu amd64, and publishes a single release from it.

That release runs on Ubuntu 22.04.1 LTS amd64 with just one dependency:

```shell
sudo apt install libconfig9
wget https://github.com/M0LTE/linbpq-builds/releases/download/release/linbpq
chmod +x linbpq
./linbpq -v
```
