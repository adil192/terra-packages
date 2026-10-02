```bash

cd ~/Documents/GitHub/terra-packages

anda build -c terra-45-x86_64 lib/mesa --rpm-builder rpmbuild
anda build -c terra-45-i386 lib/mesa

anda build -c terra-45-x86_64 games/rpcs3 --rpm-builder rpmbuild

sudo dnf update anda-build/rpm/rpms/*.rpm

```
