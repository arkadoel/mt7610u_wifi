# mt7610u_wifi
Ubuntu 14.10 w/ Kernel 3.16.0-29-generic compatible driver for ASUS Dual-Band Wireless-AC600 Wi-Fi Adapter (USB-AC51)

I didn't clean up any of the warnings and I pretty much did the quickest hacks to get this functioning.

Kernel panics after 1-5 mintues of connection on Xubuntu 14.10. I spent about 15 total hours trying to get ubuntu to crap out logs or some sort of information regarding it and it just refuses. The issue is that Kexec-tools is broken (again) so until that gets fixed I can't be bothered to care. Myabe when Vivid comes out I'll revisit this.

```
sudo apt-get update
sudo apt-get install linux-headers-generic build-essential git
git clone https://github.com/likwidoxigen/mt7610u_wifi.git
cd ~/rtl8812au
make
sudo make install
```
  

At this point I did 
```
sudo modprobe -v mt7650u_sta
iwconfig
```

I saw the RA0 adapter but I could only configure it manually not in network-mangager. 

Out of frustration I did the "windows fix" and rebooted the thing. That did the trick.
It all popped up in network manager like it was supposed to and I could connect like a boss.



References:
- https://wikidevi.com/wiki/ASUS_USB-AC51
- https://ubuntuforums.org/showthread.php?t=2228244&page=1
- http://ubuntuforums.org/showthread.php?t=1659919
- http://ubuntuforums.org/showthread.php?t=2171240


Things that don't work to get a core dump or any sort of panic info & general info:
- https://wiki.ubuntu.com/Kernel/KernelDebuggingTricks  
- https://help.ubuntu.com/lts/serverguide/kernel-crash-dump.html
- http://www.dedoimedo.com/computers/crash-analyze.html
- http://stackoverflow.com/questions/7732983/core-dump-file-is-not-generated
- https://wiki.ubuntu.com/Kernel/CrashdumpRecipe?action=show&redirect=KernelTeam%2FCrashdumpRecipe
- http://magazine.redhat.com/2007/08/15/a-quick-overview-of-linux-kernel-crash-dump-analysis/
- http://unix.stackexchange.com/questions/5459/how-to-understand-the-kernel-panic-core-dump-output
- http://unix.stackexchange.com/questions/60574/determining-cause-of-linux-kernel-panic


Other ralink implementations or references:
- https://github.com/luckasfb
- https://github.com/cnt0/rt5390
- https://github.com/qualiabyte/install-rt2860
- https://github.com/kuba-moo/mt7601u
- https://github.com/porjo/mt7601
- https://github.com/chenhaiq/mt7610u_wifi_sta_v3002_dpo_20130916
- https://github.com/sugree/asus-ac51
- https://github.com/hro424/mt7610u_wifi

My sincerest apologies for the dreadful commit graph, I'm still working on figuring out how git works and leveraging it properly. Thank you for your patience and I apologize for any issues I may have un-intentionally caused.

H2. Aditional info
```
sudo ifconfig ra0 up
sudo service network-manager stop
sudo service network-manager start
```
