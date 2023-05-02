Download Link: https://assignmentchef.com/product/solved-coen177-lab-7-minix-scheduling
<br>
<strong>Objectives</strong>

<h5>1.     To understand Minix scheduler implementation.</h5>

<h5>2.     To modify the Minix scheduler and observe effects.</h5>

<h5></h5>

<h5><strong>Guidelines</strong></h5>

In this lab, you will be working once more on the Minix operating system. You will once again install, run, and rebuild Minix, but you will work on the scheduling algorithm. Minix uses a multi-level priority queue scheduler, and modification of the scheduling algorithm, particularly changes to high priority queues, may make the system unstable. You will need to experiment with what changes can be done safely.




<strong>Reminder – Getting started with Minix on the ECC Systems</strong>

For consistency, it is recommended that you run the provided Minix image on the ECC systems. If you have not done so already, follow these instructions to install and run Minix on the ECC Systems.




Start by setting up VMware




<strong>$ setup vmware</strong>This command prepares vmware to run. You should only need to run it once, until the next time you log into your machine. To obtain a copy of a Minix system image, you can use “minix-get-image”<strong>$ minix-get-image (can tab complete)</strong>Please note that this will COMPLETELY ERASE any old image (including any changes you may have made which are not saved outside the Minix system). You must do this once, the first time you are setting up vmware. After that, you should only do this if you need a new image, such as if a modification you make causes your VM to break and become unresponsive. Next, you should run vmware.

<strong>$ vmware &amp;</strong>

This may take a little while to boot up, so be patient. Don’t assume that it is not working.Once it boots up, if you don’t see the “minix” option on the left, go to:

<ul>

 <li>Open a Virtual Machine -&gt; “vm images” subfolder -&gt; “minix3” subfolder -&gt; minix3.vmx</li>

</ul>

When you launch the minix system, you will eventually be promoted for a username. The username for the minix system is “root” (with no password, at least until you set one).




To copy files between the Minix system (running in the vmware virtual machine), and your local system, you may use FTP.  Inside of the VM, do the following:




If you have not already, type “<strong>passwd</strong>” to give the system a password. Make sure it’s a password you’ll easily remember (ask yourself, how secure does this particular system need to be? What would it take for someone to access it?) (<strong>Note:</strong> If you wipe your minix image, you will need to do this again.)Type the following command (again within the Minix system): <strong>tcpd ftp /usr/bin/in.ftpd &amp;</strong>

This will launch the FTP daemon in the Minix system, allowing the local system to connect to it through FTP.

Type “<strong>ifconfig</strong>” to find out what the IP address for the VM is.Now get out of the VM (with Ctrl+Alt) and open a terminal on the host machine. In that terminal, type:

<strong>ftp &lt;the IP address you got from ifconfig&gt;</strong>

This will launch FTP.




In case you are unfamiliar with FTP commands:

<em>For Remote Navigation </em>

<strong>ls</strong> – show contents of remote directory<strong>pwd</strong> – show current location in VM<strong>cd</strong> – change directory on the VM

<em>For Local Navigation </em>

<strong>lcd</strong> – show current location on host machine<strong>lcd &lt;directory&gt;</strong> – change location to &lt;directory&gt;

<em>File Transfer </em>

<strong>get &lt;file&gt;</strong> – copy &lt;file&gt; from current location in VM to current location on host.<strong>put &lt;file&gt;</strong> – copy &lt;file&gt; from current location on host to current location in VM.

DO NOT work on files inside of the VM. You should use FTP to transfer files from the VM to the host, work on them there, then transfer them back. This is so that you do not lose all of your progress if you should make a mistake which crashes the VM and corrupts the bootable OS.

The files for which you must search in this lab can be found somewhere beneath the /usr/src directory.

The grep utility can be very helpful for finding which files contain particular strings, and should be very helpful in this lab.




Once you have modified a file and wish to see the effects of your changes, do the following:

Return to the /usr/src directory.

Type <strong>make world</strong>. This will recompile Minix, and may take some time, so be patient.

When that finishes, type <strong>reboot</strong>. This will reboot the VM with your modifications in effect.

If your VM freezes/crashes during/after a reboot and you wish to restart with a fresh image and setup, start with the first instructions above to get a fresh copy (and note that it will overwrite your existing copy).




<h5><strong>The Minix Scheduler</strong></h5>

The goal of this assignment is to gain experience in modifying an operating system kernel, and specifically the process scheduling algorithm. You are to modify the queue selection algorithm to skew the priority scheduling. Specifically, the current selection is based on a pure priority order, then you are to include a random selection of a lower-level priority job. Note that if you modify the priority queue imprudently, the operating system will cease to function. Your goal is to achieve the following:




<ul>

 <li>upon attempting to select the next job, modify the selection to add a random possibility of choosing from a different level (the lower the probability you choose for this, the more consistent with the current selection mechanism you are, some experimentation may be required to select a reasonable value).</li>

</ul>




You will be graded based on both your implementation of this modification, and on how well you explain the mechanism. It is therefore important to realize that this is both an exercise in coding, as well as an exercise in familiarizing yourself with, and understanding to the point of being able to explain, an unfamiliar code base.




<strong>Observing a change</strong>

A second challenge in this assignment is to demonstrate how the scheduler has been modified. You are to note an observable change in behavior between the unmodified and modified schedulers. To achieve this, you may need to write a simple test program (e.g., a simple hello world program that identifies which process is running).




<strong>Additional Resources:</strong>

<ul>

 <li>Minix Wiki: https://en.wikipedia.org/wiki/MINIX</li>

 <li>Minix user guide: https://wiki.minix3.org/doku.php?id=usersguide:start</li>

 <li>Minix installation guide: https://wiki.minix3.org/doku.php?id=usersguide:doinginstallation</li>

</ul>


