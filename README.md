# UCEEE
Alternative utility for the EEE PC 901 similar to the Super Hybrid Engine and EEECTL utilities. Allows for overclocking and underclocking of the CPU.

## For:
This utility was designed for (and developed on) the Asus EEE PC 901 running 32-bit Windows XP SP3. This may work on select other machines that are very similar (e.g. the EEE PC 1000, 1000H, and 1000HA), although consider these cases untested. The '901 uses an Intel Atom N270 CPU, coupled with an ICS9LPR427AGLF clockgen chip and ICH7-M chipset, so unless your machine contains these exact parts, don't expect it to work.

## Pre-Requisites:
This does require some additional downloads:
 - .NET Framework v3.5 or later;
 - RW-Everything v1.7;
 - CPU-Z is a very handy program for ensuring the system is actually performing the over/underclocking.

This also requires a couple of settings to be tweaked in the BIOS. My machine is running BIOS version 2103 with AHCI support only as modified by Yukata. Over time, I will compile a list of compatible BIOS versions on my completely stock '901, also on 32-bit Windows XP SP3. The BIOS settings need to be tweaked as follows:

 - Navigate to the `Advanced` tab in the BIOS menu (press `F2` on the splash screen to enter the BIOS menu);
 - Enter the `CPU Configuration` menu;
 - Set `Max CPUID Value Limit` to `Enabled`;
 - Set `Intel(R) SpeedStep(tm) tech` to `Enabled`.
 - Press `F10` to exit and save changes.

RW-Everything will require a suitable path environment variable to be created. This is a relatively simple procedure, and there are numerous tutorials online on how to achieve this. Should these become unavailable at any point (and/or when I get the motivation to include a full tutorial), I will put the instructions here.

And finally, switch to the `Always On` power management profile in the Control Panel.

## Installation:
To 'install' this utility, simply extract the zip folder to a location of your choice. The application is entirely self-contained, and should work from any directory. Do not mess with the (albeit simple) internal file structure.

## Usage:
Run the application by double-clicking UCEEE.exe, or by placing a shortcut in the start menu. This shortcut can be put in the `startup` folder so that it launches when first logging into your machine, much like the Super Hybrid Engine utility by Asus. Running the application should show an icon in the task tray in the bottom right corner of the screen. Right clicking this icon gives you a selection of clock frequencies to choose from. By default, ~the system will always begin on 1.6GHz (1600MHz)~ the system will always have an FSB frequency of 133MHz, which corresponds to a CPU frequency of either 800MHz (6x multiplier) or 1600MHz (12x multiplier). This applies both when powering on, and when resuming from sleep, hibernate, etc. To this end, one MUST (for now at least) remember to set the overclock back to either 800MHz or 1600MHz before putting the system to sleep, otherwise, a crash will ensue immediately after resuming.

## Disclaimers:
This utility is NOT a professional piece of software, merely a project I have been working on. I do not believe the CPU is actually powerful enough to fry itself (highest temperature I have seen is 64°C) even with the fan off; however, I accept no liability if this does damage some part of your machine, or brick it in any other way (again, not that this should be possible).

## Recovery:
I strongly suggest saving all unsaved work before adjusting the clock frequency, just in case the system does crash. I have implemented hidden 'intermediate' frequency steps to make this utility as stable as possible, but overclocking (and underclocking) carry an inherent risk to system stability. If the system does lock up (usually with a completely garbled display), simply press and hold the power button until the machine shuts off, and then switch the machine on again as normal. If the system fails to respond to the power button after approximately 30 seconds or so, or if the screen remains blank when turning back on, simply unplug the AC adapter and remove the main battery (CMOS/BIOS/backup battery does not need to be removed) for a few seconds, reassemble/replug, and then switch on again as normal.

# Changelog
## v1.2.0
Updated to automatically return the CPU frequency (or rather, the FSB frequency) to one of the two 'safe' values when switching user, or when entering suspend (sleep). The program also automatically restores the clock speed to the previous value before switching user or resuming from suspend. In theory, the program also sets a 'safe' FSB clock when logging off and/or shutting down; however, this portion is untested.

## v1.1.0
Updated to increase the range of underclocking: Total CPU frequency range is now 400MHz (0.4GHz) to 1800MHz (1.8GHz), again in discrete steps of 200MHz. RW Scripts have been tweaked slightly to maintain stability throughout the frequency range. Added CMD commands to adjust the AC and DC processor throttle value in powercfg (/processor-throttle-ac and /processor-throttle-dc, respectively) which is used to adjust core voltage (from 0.9V to 1.1V and vice versa) and CPU multiplier (from 6x to 12x and vice versa).

## v1.0.0
This is the first release. Current capabilities allow over/underclocking between 1000MHz (1GHz) and 1800MHz (1.8GHz) in discrete steps of 200MHz. This is done manually, and the only feedback available to the user would be the use of an external program such as CPU-Z or HWMonitor. The user must manually ensure the system is reset to 1600MHz before putting the system to sleep. Utility resets CPU frequency to 1600MHz automatically upon exit.
