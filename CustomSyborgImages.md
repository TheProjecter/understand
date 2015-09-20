# Introduction #
## Preamble ##
This article assumes that you have successfully configured the Symbian Kernel Kit components and toolchain on a system running Windows XP, including ARM RealView Compilation Tools (RVCT) 4.0, ActivePerl, and Symbian's patched Mercurial version of QEMU.

**NOTE** - In order to run the Mercurial version of the QEMU-based emulator, as supplied in a Symbian Kernel Kit in binary form, it is imperative that the [Microsoft Visual Studio C++ 2008 Redistributable Package](http://www.microsoft.com/downloadS/details.aspx?familyid=9B2DA534-3E03-4391-8A4D-074B9F2BC1BF&displaylang=en) be installed, as a `"The application failed to initialize properly (0xc0150002). Click on OK to terminate the application."` error dialogue will be produced, otherwise.

## Useful Tips ##
  * When running QEMU, it may be necessary to specify that serial port debugging output gets dumped to a file, using an argument similar to: `-serial file:"SOSDUMP.TXT"`

## EUserHL on Host-Bound Storage (Drive `S:\`) ##

### `EUserHL` Package Installation and `PATH` Testing ###
  * Download the `EUserHL.zip` archive from [here](http://developer.symbian.org/wiki/index.php/File:EUserHL.zip), and extract it using your favourite ZIP archive management tool
  * Run the extracted `EUserHL.exe` executable to begin the process of copying a number of files to `C:\Symbian` (example code, header files, a set of `.SIS` files, a number of ARM `UREL`/`UDEB` DLLs and executables, and a number of Windows x86 `WINSCW` DLLs and executables for use in the old Windows-based simulator)
  * Ensure that the `C:\epoc32\tools` directory is present in the `PATH` environment variable, so that the `dumpsis` utility can be used

### Extracting and Examining the Payload ###
  * Create a new, empty directory at `C:\Symbian\ExtractedFiles` to store any temporary files used during this process
  * Copy `C:\Symbian\EUserHL.sis` into the new `ExtractedFiles` directory
  * Open a `cmd.exe` (or another shell of choice) session, and switch to the `C:\Symbian\ExtractedFiles` directory
  * Run `dumpsis EUserHL.sis` to extract the contents of the `.SIS` file to a `EUserHL` directory containing 3 files (`file0`, `file1` and `EUserHL.pkg`)
  * Rename `file0` to `euserhl.dll`, and `file1` to `backup_registration.xml`
  * Theoretically, given that the `.PKG` file suggests that these files are (Symbian Platform) drive letter-agnostic, we should be able to move them to specified subdirectories in `C:\svphostfs\`, and have them function within QEMU
  * Create a nested set of directories at `C:\svphostfs\private\10202D56\import\packages\2001B440`
  * Create another nested set of directories at `C:\svphostfs\sys\bin`, if they don't exist already
  * Move `C:\Symbian\ExtractedFiles\EUserHL\euserhl.dll` to `C:\svphostfs\sys\bin`
  * Move `C:\Symbian\ExtractedFiles\EUserHL\backup_registration.xml` to `C:\svphostfs\private\10202D56\import\packages\2001B440`

At this stage, we can attempt to run an example binary

### Running an Example Binary ###
  * Copy the `euserhl_walkthrough.exe` binary from `C:\Symbian\epoc32\release\armv5\urel` to `C:\svphostfs\sys\bin`
  * Run `arm-none-symbianelf-qemu-system -M \sf\adaptation\qemu\baseport\syborg\syborg.dtb -kernel \epoc32\rom\syborg.img` to start the QEMU-based emulator, assuming that the ROM image and `.DTB` files are in the specified locations
  * At present, it appears that the `euserhl_walkthrough.exe` binary fails out with a `Not found` error when executed