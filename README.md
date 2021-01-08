retroIO
=======
Turn your PC into a retro machine using real hardware! By using the VFIO capabilities of the Linux kernel, you can create virtual machines where the CPU, mainboard, and storage are emulated, but components like the video card and sound card are real.

This allows you to use older operating systems through their native drivers, at native performance and quality, with the convenience of modern virtualization like snapshots and emulated networking, keyboard sharing, and DVD/floppy emulation. You can also use vendor-exclusive features like 3D Sound and GLIDE/DirectX just like on a real machine.

This project has support for PCI and PCIe cards. ISA, PCI-X, and AGP hardware is not yet supported, but could be possible with custom bridges.

Getting Started
===============

You Will Need
-------------
  - AMD or Intel PC with support for AMD-Vi/VT-d
  - Linux
  - PCIe/PCI cards to use with the retro VM
  - PCI bridge riser (if needed)
    
Most AMD Ryzen CPUs with B450/X470 boards support VFIO, alongside higher end Intel CPUs (check your specs!)

Supported Emulators
-------------------
  - QEMU

PCI Bridge Options
------------------
There are two major PCI to PCIe bridge chips available, the ASM1083 (from ASMedia) and PI7C9X11x (from Pericom). 

The ASM1083 is cheaper (around $10 USD) but generally single-slot and might have bugs with certain hardware (such as Firewire cards); it is recommended for sound cards and low speed PCI devices. The PI7C9X11x is more expensive ($20) but better supports hardware, including dual-slot and 66Mhz mode.

Note that most motherboards with a built-in PCI slot use the ASM1083 bridge chip.

P17C9X11x
https://www.aliexpress.com/item/32975912171.html  
https://www.ebay.com/itm/311915485839  
https://www.ebay.com/itm/143648841107  

ASM1083
https://www.aliexpress.com/item/4001221339492.html (single-slot)  
https://www.aliexpress.com/item/1005001373451558.html (dual-slot)  

Hardware
========

Video Card Options
------------------
The choices are pretty extensive, but you will need to get a video card that supports the operating system you plan to use. Some starting examples include:
  - NVIDIA Quadro FX 3500 (PCIe, 2000/XP/Vista/7/8)
  - ATI Radeon X300 (PCIe, 98/ME/2000/XP)
  - Cirrus Logic GD5446 (PCI, 3.1/95/98/ME/NT/2000)
    
Software
========
Practically any operating system that can run on a PC BIOS is supported. QEMU by default uses SeaBIOS for its firmware, and this supports booting:
  - Windows NT4/2000/XP/Vista/7/8/10
  - Windows 95/98/98SE/ME
  - DOS 6.22 + Win 3.1/3.11
  - Linux
    
QEMU supports both hardware-accelerated and software CPU modes. The latter allows more control of the CPU speed for cycle-sensitive games in combination with `cpulimit`, although this isn't perfect.

FAQ
===

Can this support other emulators?
---------------------------------
Potentially, yes! VFIO is part of the Linux kernel, but the API is available to all Linux applications, not just QEMU. Any number of emulators could add support for the VFIO API, although this requires support from their respective developers.

Can I use a motherboard with built-in PCI?
------------------------------------------
Yes, motherboards with built-in PCI bridges should work as long as the board and CPU itself supports VFIO as noted in getting started. The process of binding those cards is the same as with an external bridge.

Will a capture/modem/storage/etc card work?
----------------------------------------------------------
The only way to know is to try, although so far capture cards, modems, and ethernet cards have been tested without issues.
