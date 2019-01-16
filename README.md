# VFIO

This repo is used as my notes for my vfio setup, also known as GPU passthrough. I wanted to save it in case I'll want to pick it up in the future and start from there.

## Install
`apt install firmware-linux nvidia-driver ovmf virt-manager` at the minimum. This is for my setup only.

## Potential improvements
- kwin_x11 is sometimes stuck in infinite CPU loop while stopping sddm, possible workaround would be to kill -9 it if not responding for longer than a few seconds during waiting for SDDM to shutdown
- evdev passthrough works good enough, but pushing too many buttons can freeze the machine, very likely the same as https://lists.gnu.org/archive/html/qemu-devel/2017-04/msg05847.html
- Maybe it'd be possible to somehow switch xorg to the other GPU instead of forcing its restart, it's definitely possible with third-party programs but they add their own overhead that I don't want
- VM has several issues in regards to freezes, potentially on I/O usage. This could probably be improved if I dug deeper into the drives used
- Even idle VM uses around 100% CPU usage of a single thread. This can be normal in regards to keeping VM up, or it could be somehow improved
- PulseAudio works good enough but sometimes subtle cracking can be heard, it could be related to my Xonar DX sound card, or it could be irrelevant, investigate if possible
- Very rarely my script can be stuck at unbinding the GPU, I couldn't reproduce it for a while so maybe that one is fixed, it can happen only when my script won't take into account some app using the GPU - `sddm`, `Xorg` and `kwin_x11` are already took into account

## Annoying shit
- Capslock issue still not fixed https://bugs.launchpad.net/ubuntu/+source/xorg-server/+bug/1376903
- Xorg still can't use more than one GPU at the same time
