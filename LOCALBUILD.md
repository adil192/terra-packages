### Setup

Create submodules from Fedora upstream:
```bash
cd ~/Documents/GitHub/terra-packages

mkdir -p anda/lib/gtk4/
git clone -b f45 https://src.fedoraproject.org/rpms/gtk4.git extern/gtk4
ln -sr extern/gtk4/* anda/lib/gtk4/
echo $'project pkg {\n	rpm {\n		spec = "gtk4.spec"\n	}\n}' > anda/lib/gtk4/anda.hcl

mkdir -p anda/desktops/gnome/mutter/
git clone -b f45 https://src.fedoraproject.org/rpms/mutter.git extern/mutter
ln -sr extern/mutter/* anda/desktops/gnome/mutter/
echo $'project pkg {\n	rpm {\n		spec = "mutter.spec"\n	}\n}' > anda/desktops/gnome/mutter/anda.hcl

mkdir -p anda/desktops/gnome/gnome-shell/
git clone -b f45 https://src.fedoraproject.org/rpms/gnome-shell.git extern/gnome-shell
ln -sr extern/gnome-shell/* anda/desktops/gnome/gnome-shell/
echo $'project pkg {\n	rpm {\n		spec = "gnome-shell.spec"\n	}\n}' > anda/desktops/gnome/gnome-shell/anda.hcl
```

Install build dependencies:
```bash
sudo dnf builddep mesa rpcs3 gtk4 mutter gnome-shell
```

Add these optimization flags to `~/.rpmmacros`:
```bash
%_distro_extra_cflags -march=native -mtune=native
%_distro_extra_cxxflags -march=native -mtune=native
%_distro_extra_fflags -march=native -mtune=native
```
Add them to CFLAGS in gtk4.spec too.

### Update sources

```bash
git pull --rebase
git -C extern/gtk4 pull --rebase
git -C extern/mutter pull --rebase
git -C extern/gnome-shell pull --rebase
```

### Build


```bash
anda build lib/mesa -c terra-45-x86_64 -D "vendor Terra" -r rpmbuild
anda build lib/mesa -c terra-45-i386 -D "vendor Terra"
```

```bash
anda build games/rpcs3 -c terra-45-x86_64 -D "vendor Terra" -r rpmbuild
```

```bash
anda build lib/gtk4 -c terra-45-x86_64 -D "vendor Fedora Project" -r rpmbuild
anda build desktops/gnome/mutter -c terra-45-x86_64 -D "vendor Fedora Project" -r rpmbuild
anda build desktops/gnome/gnome-shell -c terra-45-x86_64 -D "vendor Fedora Project" -r rpmbuild
```

### Install

```bash
sudo dnf update anda-build/rpm/rpms/*.rpm
```
