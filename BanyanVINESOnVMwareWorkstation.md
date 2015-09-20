1. Download the archive containing the Disk Images from http://house404.co.uk/VINES_8.5.zip, and unzip the archive.
You should now have 5 files (`85INST1.FIL`, and `85INST2.FIL` (Install Images), and the Release Images (`85REL1.FIL`, `85REL2.FIL`, and `85REL3.FIL`)).

The Release Images contain the bulk of the VINES operating system itself (mostly concentrated in `85REL3.FIL`).

The Install Images are used to bootstrap the installation process.

2. Start VMware Workstation and create a new virtual machine with the following settings:<br />
> `Memory: 88MB` (96MB is the maximum, due to System V limitations)<br />
> `Processors: 1`<br />
> `Display: Auto Detect`<br />

> The Hard Disk MUST be 0.4GB or less, and MUST be IDE for this to work. You can choose to "`Allocate all disk space now`" (I didn't), and unselect "`Split disk into 2GB files`" as it is not required.
> Name the disk image something like "`VINES.vmdk`" or something else you can remember

> Check the settings for the Virtual Machine. You should have `Memory: 88MB`, `Processors: 1`, `Floppy:` Path to `85INST1.FIL`, `Display:` as defaults, `Hard Disk (IDE 0:0:)` 409MB or less

> Set Guest Operating System to "`Other`" in the `Options` tab, disable Shared Folders and the Guest Isolation options, and finally disable Acceleration.

3. Start the virtual machine, and press and hold the F2 key to enter BIOS setup
> Select `Primary Master`, and set `Type` to `User`.
> IMPORTANT: Set `Cylinders` to `1023` or installation will fail after the first reboot. Set "`LBA Mode Control`" to `Disabled` and `32 Bit I/O` to `Disabled` (if these aren't disabled, the system will bail out with an `srmount` error and a kernel panic).
> You can now press Escape to exit the menu, and then F10 and answer "`Yes`"

4. Now the disk image should start to boot and you should arrive at "`BANYAN NETWORKING SOLUTION`", and then additional data will be loaded from the floppy image. When prompted, switch the floppy image to `85INST2.FIL` and then press Enter.

> At the menu, just press 1 and hit Enter. At the next menu, say no (press the N key and then hit enter).
> Answer "`Y`" to "`Would you like to install Enterprise Backup/Restore (EBR)?`", and `Y` again to "`Install OS/2 client files?`"
> When asked to override the default file system sizes, just answer "`N`" and wait for the Banyan S5 and S10 file systems to be created.

5. Switch the floppy image to `85REL1.FIL` (Release Diskette #1) and then press Enter, and then when prompted, switch to `85REL2.FIL`
and finally `85REL3.FIL` when prompted. Wait for the installation to complete, until it asks about the Kernel configuration.
Choose the default option (`D`) and hit enter, the kernel will be assembled from the modules on `85REL3.FIL` and then copied to `/unix` on the hard disk image.
If you want, you can create an empty VMware floppy image, and switch the virtual floppy drive to it at this point and answer `Y` to save a copy of the kernel to the floppy image (it becomes a CPIO archive that you can manipulate with UNIX/Windows archiving tools).
Otherwise, say `N`and hit enter, Disconnect the floppy image, and then wait for VINES to reboot.

6. If the virtual machine didn't crash or hang at some stage and installation needed to be restarted, it should start booting from the virtual hard disk, and VINES should start checking the hard disk image. If it hangs and kernel panics, then something is wrong.

If everything went well, you should now be at "`Password Installation Menu`". Since Banyan Systems, Inc is dead, and isn't likely to recieve a support call from you, just choose option 2 or option 3 and then hit enter. If you wanted to be adventurous, you could choose option 1 (not that I'd recommend it). If you chose 2 or 3, just press enter, and then answer `Y` and then hit enter again.

It's up to you, when you get to "`Number of previous root passwords that cannot be re-used (1-20, none)`", you could choose the default (10) or you could choose "`none`" as I did. Just press enter for the "`Minimum Password Length`" and then again at "`Password expiration in weeks (1-52, never)`", and then hit "Y" and Enter again.
Choose a password if you want, or hit Enter twice for no password.

7. You should be at "`Release media will be diskettes. Is this correct?`" now. Just hit Enter twice, before reaching the following:

`This procedure will install your disks using the following parameters:`<br />

> `Banyan Server Software Version..........8.50 (0)`<br />
> `Banyan Client Files Load................DOS, OS/2`<br />
> `Enterprise Backup/Restore (EBR) Files...INCLUDED`<br />
> `Banyan Release Media Type...............diskettes`<br />

Answer `Y`, and then Enter at this point.

8. I'm not sure what should happen at this stage, since I only get the following:

`/install/fullinstall: test: argument expected`

`Error occured during installation ... Installation Aborted.`

## Notes ##

From VMware Workstation's VM menu, choose "`Send Ctrl+Alt+Del`" to flush the changes to disk and do a clean reboot.

You may reboot the server and try from the "`Password Installation Menu`" screen again, if you get the error at the start of this section.

After rebooting, by playing with the options at the "`Password Installation` Menu" screen that appeared again (and manually killing VINES with Workstation's `Power Off` button and installing another IDE HDD image), I managed to get a shell, but couldn't do much.