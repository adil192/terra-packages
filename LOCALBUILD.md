```bash

cd ~/Documents/GitHub/terra-packages

sudo dnf builddep mesa rpcs3

anda build lib/mesa -c terra-45-x86_64 -D "vendor Terra" -r rpmbuild
anda build lib/mesa -c terra-45-i386 -D "vendor Terra"

anda build games/rpcs3 -c terra-45-x86_64 -D "vendor Terra" -r rpmbuild

sudo dnf update anda-build/rpm/rpms/*.rpm

```
