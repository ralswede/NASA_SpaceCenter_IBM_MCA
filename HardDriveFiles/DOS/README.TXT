
README.TXT

NOTES ON IBM DOS VERSION 5.0
===========================

This readme provides important information not included in the
IBM DOS User's Guide and Reference or in on-line Help.

Look through the following table of contents to determine
whether your software or hardware is included.

ATTENTION CODEVIEW AND INTEL ABOVEBOARD USERS
+++++++++++++++++++++++++++++++++++++++++++++
APPNOTES.TXT contains critical information about
using CodeView and Intel Aboveboard with DOS
5.0.
+++++++++++++++++++++++++++++++++++++++++++++

For information about using applications with DOS 5.0,
see the APPNOTES.TXT file.

The following topics are discussed in this file:

1. Readme Conventions
2. Machine-Specific HIMEM.SYS Switches
        * Bull Micral 60
        * COMPUADD 386
        * Datamedia 386/486
        * Hitachi HL500C
        * Intel 301z or 302
        * JDR 386/33
        * Toshiba 5100
        * UNISYS PowerPort
3. Installing DOS 5.0 on an OS/2 Dual-Boot System
4. Notes on Memory Management
   4.1 Problems Loading into the Upper Memory Area
   4.2 Intel Expanded-Memory Driver (EMM.SYS)
   4.3 Phoenix BIOS and HIMEM.SYS
5. Notes on Windows
   5.1 DOS Applications in Expanded Memory
   5.2 "Unable to start Enhanced Mode Windows" Message
   5.3 WINA20.386 File
   5.4 "High Memory Area in Use" Message (Windows/386 2.1)
   5.5 "Cannot run Windows in standard mode" Message
6. Making Your Hardware Compatible with DOS 5.0
   6.1 Using a Mouse with DOS Shell
        * Logitech
        * Microsoft
   6.2 XGA and EMM386.EXE
7. Making Your Network Compatible with DOS 5.0
   7.1 DOS Shell and Networks
   7.2 AT&T StarGROUP
   7.3 PC-NFS 3.0
   7.4 TOPS Network
8. Documentation Corrections and Additions
   8.1 New CV.COM for CodeView
   8.2 Documentation Corrections
   8.3 Hercules Display Adapter (MSHERC.COM)
   8.4 QBasic "On Error" Command
   8.5 SMARTDRV and Third-Party Partitions

1. README CONVENTIONS
=====================
If you have questions about procedures or commands mentioned
in this file, you will probably find answers in the IBM
DOS User's Guide and Reference. The following paragraphs
describe frequently mentioned topics that the guide covers in
more detail.

Many sections of the readme discuss changing your CONFIG.SYS
file. For detailed information about modifying a CONFIG.SYS
file, see Chapter 11 of the DOS User's Guide and Reference.

The readme often refers to DEVICE commands in your CONFIG.SYS
file. For example, one section recommends "adding a machine:1
switch to the DEVICE=HIMEM.SYS command in your CONFIG.SYS
file." These DEVICE= statements indicate the type of command
in the CONFIG.SYS file. You need to modify these statements to
reflect the configuration of your system. For more information,
see the DEVICE command in Chapter 14 of the DOS User's
Guide and Reference.

The readme sometimes asks you to use the EXPAND command to copy
files from the distribution disks to your hard disk. See Chapter
14 of the DOS User's Guide and Reference for more
information about using the EXPAND command.


2. MACHINE-SPECIFIC HIMEM.SYS SWITCHES
--------------------------------------
To install DOS 5.0 on a system listed in this section,
you must do the following:
    1. Insert Disk 1 in drive A and restart your system to
       run Setup.
    2. When Setup ends, press F3.
    3. Edit your CONFIG.SYS file as follows:
       a. Add the appropriate /machine switch to the
          DEVICE=HIMEM.SYS command. For example, if you have an
          Intel 301z, your DEVICE=HIMEM.SYS command would look
          like this:
             device=c:\dos\himem.sys /machine:8
       b. Restart your system.

   System                    Switch
   ------                    ------
   Bull Micral 60            /machine:16
   COMPUADD 386 systems      /machine:1 or /machine:8
   Datamedia 386/486         /machine:2
   Hitachi HL500C            /machine:8
   Intel 301z or 302         /machine:8
   JDR 386/33                /machine:1
   Toshiba 5100              /machine:7
   UNISYS PowerPort          /machine:2

3. INSTALLING DOS 5.0 ON AN OS/2 DUAL-BOOT SYSTEM
----------------------------------------------------
If you install your operating system by using the BOOT /OS2 or
BOOT /DOS command, install DOS 5.0 as follows:
   1. Start DOS by using the BOOT /DOS command.
   2. Run Setup.

If you use the form of an OS/2 dual-boot system that prompts
you at startup to select an operating system, do the following:
   1. Install DOS 5.0 on your hard disk.
   2. Create a system disk by inserting a disk in drive A and
      typing the FORMAT A: /S command.
   3. Delete the COMMAND.COM file from the floppy disk.
   4. On the floppy disk, create a CONFIG.SYS file that
      includes the following:
             shell=c:\dos\command.com /p /e:256
   5. On the floppy disk, create an AUTOEXEC.BAT file that
      includes the following commands:
             path=c:\dos
             append /e
             append c:\dos
             prompt $p$g
             set comspec=
   6. Reinstall the OS/2 operating system on your hard disk.
   7. Insert in drive A the system disk you created and restart
      your computer.
   8. Run the dual-boot program (C:\DUALBOOT\DUALBOOT.EXE).

4. NOTES ON MEMORY MANAGEMENT
=============================

4.1 Problems Loading into the Upper Memory Area
-----------------------------------------------
Some computers with hard disk controllers, specifically bus
master DMA controllers, may not be able to load device drivers
or programs into the upper memory area. Try adding a
DEVICE=SMARTDRV.SYS command before any DEVICEHIGH commands in
your CONFIG.SYS file.

4.2 Intel Expanded-Memory Driver (EMM.SYS)
------------------------------------------
Use the Intel expanded-memory driver NE or E switch when
installing the driver for Aboveboard. See your Aboveboard
documentation for more information.

4.3 Phoenix BIOS and HIMEM.SYS
------------------------------
If your system includes a Phoenix BIOS and DOS 5.0 doesn't
work correctly, try adding a /machine:1 or /machine:8 switch
to the DEVICE=HIMEM.SYS command in your CONFIG.SYS file.

5. NOTES ON WINDOWS
===================

5.1 DOS Applications in Expanded Memory
---------------------------------------
If you load device drivers and memory-resident programs into
the upper memory area, and you run DOS applications that use
expanded memory under Windows 3.0, specify the RAM switch with
the DEVICE=EMM386.EXE command in your CONFIG.SYS file.

5.2 "Unable to start Enhanced Mode Windows" Message
---------------------------------------------------
If you start Windows enhanced mode 3.0, and get a message
stating "EMM386: Unable to start Enhanced Mode Windows due
to invalid path specification for EMM386", add the /y=path
switch to the DEVICE=EMM386.EXE command in your CONFIG.SYS
file. "Path" specifies the location of the EMM386.EXE file
when you start Windows.

For example, if the EMM386.EXE file is in the \DOS directory on
drive C, your command would look like this:
   DEVICE=EMM386.EXE /y=c:\dos\emm386.exe

5.3 WINA20.386 File
-------------------
Setup installs a read-only file named WINA20.386 in your root
directory.

If you move the WINA20.386 file to a different directory, do the
following:
   1. Add a SWITCHES=/W command to your CONFIG.SYS file.
   2. Add a DEVICE=[drive:][path]]WINA20.386 command to the
      [386Enh] section of your Windows SYSTEM.INI file.

5.4 "High Memory Area in Use" Message (Windows/386 2.1)
-------------------------------------------------------
You cannot run Windows/386 2.1 when DOS 5.0 is loaded into
the high memory area. Also, the DOS 5.0 versions of
SMARTDRV.SYS and RAMDRIVE.SYS are not compatible with Windows/386
2.1. To run Windows/386 2.1 with DOS 5.0, use the versions of
SMARTDRV.SYS and RAMDRIVE.SYS that came with Windows and remove
the DOS=HIGH command, if any, from your CONFIG.SYS file.

5.5 "Cannot run Windows in standard mode" Message
-------------------------------------------------
If you have a DEVICE=EMM386.EXE command in your CONFIG.SYS file,
you cannot run Windows 3.0 in standard mode. Either remove
the DEVICE=EMM386.EXE command or run Windows in real or enhanced
mode.

NOTE: Using EMM386 may reduce the amount of extended memory
available to Windows and cause Windows to try to start in
standard mode. To prevent this, reduce the amount of extended
memory that other device drivers use. For example, if you are
using SMARTDRV, try setting the MinCacheSize parameter to 0.

6. MAKING YOUR HARDWARE COMPATIBLE WITH DOS 5.0
==================================================

6.1 Using a Mouse with DOS Shell
-----------------------------------
If you have a Logitech or Microsoft mouse, use the following
driver versions with DOS Shell:
   Logitech mouse version 5.01 or later
   Microsoft mouse version 6.21 or later

6.2 XGA and EMM386.EXE
----------------------
If you use an XGA display with EMM386.EXE, you may need to
exclude certain memory ranges with the EMM386 EXCLUDE option
(x=). To determine which memory ranges to exclude, use your
reference disk to view the memory map.


7. MAKING YOUR NETWORK COMPATIBLE WITH DOS 5.0
=================================================

7.1 DOS Shell and Networks
-----------------------------
Most network software won't work correctly if you start it from
a DOS Shell command prompt. Start your network before starting
DOS Shell.

7.2 AT&T StarGROUP
-------------------
If your AT&T StarGROUP version does not support DOS 5.0,
contact your AT&T representative or the AT&T National Systems
Support Hotline for information about required modifications or
upgrades.

7.3 PC-NFS 3.0
--------------
If you use PC-NFS 3.0 with DOS Shell, DOS Shell may
display more drives than you have currently enabled. To
prevent this, use the PC-NFS /d switch to specify the number
of drives you are using. For more information, see your PC-NFS
documentation.

If you can't use the COPY or XCOPY command on PC-NFS 3.01,
contact your vendor to get an updated version of the PCNFS.SYS
device driver.

7.4 TOPS Network
----------------
If your system is a TOPS workstation, the DOS Shell MOVE
command may not work.

Don't use the LOADHIGH command with a TOPS network.

8. DOCUMENTATION CORRECTIONS AND ADDITIONS
==========================================

8.1 New CV.COM for CodeView
---------------------------
Users of CodeView versions 3.0 to 3.13 should use the program
CV.COM to start CodeView.  For more details, see the section
on CodeView in the file APPNOTES.TXT.

8.2 Documentation Corrections
-----------------------------
The following are corrections to the DOS User's
Guide and Reference:

COMP /? Help:
   Online help for the COMP command /d switch should state that
   the default format is hexadecimal.

FORMAT Command:
     If you can't use the FORMAT command to format an
     unformatted disk, try using the /u switch.

MIRROR Command:
     You cannot use the MIRROR command with a network drive or
     any drive you created by using the ASSIGN, SUBST, or JOIN
     command.

UNDELETE Command:
     Do not use the UNDELETE command in the following
     circumstances:
     * When other programs are active.
     * With the LOAD= command or the Shift+Enter key
       combination in Windows.
     * With Task Swapper in DOS Shell.

UNFORMAT Command:
     The UNFORMAT /p switch is not compatible with the /j switch.

8.3 Hercules Display Adapter (MSHERC.COM)
-----------------------------------------
If you use DOS Editor or QBasic with a Hercules display
adapter, run MSHERC.COM before you run either program.

8.4 QBasic "On Error" Command
-----------------------------
Online help for QBasic incorrectly states that
ON ERROR RESUME NEXT is a valid statement. The correct syntax
is as follows:
   ON ERROR GOTO <LINE/LABEL>

8.5 SMARTDRV and Third-Party Partitions
-----------------------------------------
If your system includes a third-party disk partition and you
try to use SMARTDRV, you may receive a message stating that
you cannot load SMARTDRV.

You can force SMARTDRV to load by specifying the /p switch.
However, doing so may corrupt your hard disk if either of the
following conditions is true:
   * Your hard disk contains more than 1024 cylinders.
   * Your hard disk is not supported by the system's ROM BIOS.

If you have partitions created by using third-party
disk-partitioning software, use SMARTDRV ONLY if you are sure
your hard disk contains 1024 or fewer cylinders AND it is
supported directly by the system's ROM BIOS.
