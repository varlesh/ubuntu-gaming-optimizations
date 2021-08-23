# Ubuntu optimizations for games

## Update and install latest NVIDIA GPU drivers:
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt dist-upgrade
sudo ubuntu-drivers autoinstall
```

## Update and install latest AMD GPU drivers:
```
sudo add-apt-repository ppa:oibaf/graphics-drivers
sudo apt dist-upgrade
```

## Install [Liquorix](https://liquorix.net/) kernel:
```
sudo add-apt-repository ppa:damentz/liquorix
sudo apt-get update
sudo apt-get install linux-image-liquorix-amd64 linux-headers-liquorix-amd64
```
## INTEL CPU optimizations 

Enable [intel_pstate](https://www.kernel.org/doc/html/v4.12/admin-guide/pm/intel_pstate.html) module, if you use Sandy Bridge or newer CPU:
```
sudo sed -i s/quiet\ splash/quiet\ splash\ intel_pstate=enable/g /etc/default/grub
sudo update-grub
```

## Added some environment variables for NVIDIA GPU:
```
echo "export __GL_THREADED_OPTIMIZATIONS=1" >> ~/.profile
echo "export _GL_SHADER_DISK_CACHE=1" >> ~/.profile
```

## Added some environment variables for AMD GPU:
```
echo "export RADV_PERFTEST=aco" >> ~/.profile
echo "export mesa_glthread=true" >> ~/.profile
sudo reboot
```

## Install [VULKAN](https://www.vulkan.org/) and [VKBASALT](https://github.com/DadSchoorse/vkBasalt)
```
sudo add-apt-repository ppa:flexiondotorg/mangohud
sudo apt install mesa-vulkan-drivers vkbasalt
echo "export ENABLE_VKBASALT=1" >> ~/.profile
```

## Additional settings for NVIDIA GPU & KDE

On NVIDIA settings:

- disable **Force Composition Pipeline**  and **Force Full Composition Pipeline**
- disable **Sync to VBlank**
- set **Performance mode**
- save changes to `/etc/X11/xorg.conf`

Fix tearing for KWin:
```
touch ~/.config/plasma-workspace/env/kwin.sh
chmod +x ~/.config/plasma-workspace/env/kwin.sh
echo "export KWIN_TRIPLE_BUFFER=1" >> ~/.config/plasma-workspace/env/kwin.sh
echo "export __GL_YIELD=USLEEP" >> ~/.config/plasma-workspace/env/kwin.sh
echo "export __GL_MaxFramesAllowed=1" >> ~/.config/plasma-workspace/env/kwin.sh
sudo reboot
```
