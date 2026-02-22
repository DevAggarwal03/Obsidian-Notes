**Intro: Data Acqusition**
- Data acquistions => process of ***copying data***
- In context of Digital Forensics: *It is the task of collecting digital evidence from electronic media*
- **2 types** of data acquisitions:
    1.Static Data Acquisition 
        - Capturing of data which is not held by a process that can change it's contents
        - making a copy of an originally preserved data will produce the same result.
    2.Live Data Acquisition  
        - More prevalent in modern times because: disk encryption, newer Operating Systemes, collecting data from RAM is becoming important
        - Capturing live data can change file metadata eg: date and time can change
        - New data is acquired on subsequent attempts in capturing live data
- Goal of static Data Acqusition is to preserve Digital Evidence. 
- Do not depend on one tool only, because you might have only one chance to create a copy and something might go wrong. So keeping a backup acquistion tool is recommended.

**Understanding storage formats for digital Evidence**
- many acquisitions tools create **Disk to image** in older open-src format "RAW"
- AFF: Advanced Forensic Format (new open-src format that is gaining attraction)

1. **RAW**:
    - first format that was used to preserve digital data for forensics
    - **Bit by Bit copy (Disk to image)** of a source drive into another drive of same or larger file
    - *Bit stream data* is copied directly into a *file*
    - Some os have built in utility to create a disk to image copy eg: UNIX/linux using '**dd**' command
    - This Copy technique produces **Sequential Flat Files** of a suspect drive. The output of these flat files is refered to as the Raw format
    - some **commercial acquisitions tools** producing raw format also provide **data validation** using **crc32, md5, sha1** etc but it creates a totally new file where hashes are stored.
	
    **Adv**
    - Fast data transfer.
    - Ability to **ignore minor data** read error on the source drive.
    - Almost all the forensic tools support this format, hence it is an **Universal Acquistion Format**.

    **dis**
    - Requires the same amount of storage as the Suspect drive uses.
    - Most of the time Marginal (bad) sectors are ignored by free software. But proprietary software might have more threshold for retry for reading weak
	    media spot on the source drive.
        
2. **proprietary Format**:
    - format that are created by commercial forensics acquisition tools that supports many extra features native to their tool.
    - eg: Guidance software EnCase tool's .E01 (the number increases from 1 for subsequent segments formed) file (popularly knows as Expert Witness file)
    - example **features**:
        - compressable image files to save storage
        - ability to segment a large image file into small segments for sparse/logical acquisiton while also providing Integrity checks using hashing
            algorithms eg: Can be seen in FTK imager.
        - Ability to add metadata in the image file eg: date and item of the acquisition, hash of the original disk, name of the examiner etc.
    
    **disadvantages**:
        - The inability to share a proprietary format file with other acquistion tools. eg: (in the book not gonna write it pg:96);
        - The limitation of size of the segmented file ie, a segmented file can be as low as ~650Mb and as large as 2Gb, **Beaucse**: modern 
            drives used are generally formatted as FAT(file allocation Table) that has a limit of 2Gb.

3. **Advanced Forensic Format:**
    - Developed by Simson L. Garfinkle
    - open source file format
    - **design goals**
        - can produce compressable and uncompressable image file 
        - No size restrictiorn for disk to image
        - contains space in the image/segmented files for metadata
        - Open source
        - data integrity check for self authentication
    - extention: .afd: image file, .afm: metadate file

---------

# determining the best acquisition method
- there are two types of Acquisitions 
    1. Live
        - done on powered on systems
        - ex: on computer/device that is only accessible over the network
    2. Static
        - done on powered off systems
        - ex: create an image of a computer's hard-disk after a police raid on a crime scene
- these two Acquisitions have 4 common methods of data collection:
    1. disk to image
    2. disk to disk
    3. sparse file copy 
    4. logical disk to disk 

- Best method depends on the cicumstances of the investigations
- **key principal**: Never work on an original disk, always work on a copy. this preserves evidence integrity and maintains chain of custody

1. Disk to image:
    - bit for bit replication of the original drive which results into an image file (most popular method). 
    - can be read my almost all the forensic tool (open source or commercial) 
    - in the past tool on MS-Dos require the whole drive to analyse, so duplicating the drive was required (disk to disk)
    - now mordern GUI tools saves time, and resources by enabling investigators to read from an image stored on the system it self.
2. Disk to Disk:
    - some times due to software or hardware error, create an image will not be possible. In these situations the original drive is stored
        into another drive while geometry matches the original one.
    - this is more common if the origin drive is very old.
    - This can be dome my some imageing tool like **EnCase** and **X-ways forensics**
    - here the geometry include: cylinder, sectors, partitions, head, track configurations
3. Sparse File copy:
    - collecting only files that are of interest to the case from a large source of data (includes unallocated space fragments as well);
4. Logical acquistion:
    - collecting only files that are of interst to the case from a large source of data (excludes unallocated space);

*examples where Logical Acqusitions are used*:
- Email investigations, say we only need outlook files like .ost, .pst etc
- Data acquistion from large storage base like a RAID acquistions or from a cloud storage or from a Storage Area Network (SAN) servers containing
    ExaBytes (EB) of data.
- e-discovery for civil litigation that involves acquistions of data from a large data base have been done via logical acquisitons
    

**Factors for determining best acquistions method: **
- Considering the disk size/storage
- Whether the disk can be retained or must be returned to the owner
- How much time does it take for the acquistions of the said disk
- where is the evidence located

**If the disk size is very large**
- If the disk size is say 4Tb then make sure the target disk have free space of more that 4Tb in it.
- If not then see for some methods to reduce the size of the resulting image:
    1. Older microsoft tools like: *DiskDrive*, *DoubleSpace* : Only removes slack(space that is left in a cluster after the files a stored in the disk)
        space from the disk.
    2. Some software provide a compression method that use algorithms to reduce file size. Ex: **winRAR**, **PKZip**, **WinZip** use LossLess compression
        that do not distort/corrupt the data while also reducing the overall storage consumption of the file.
    3. Files containing graphic media like images, audio file etc use compression algorithms called "lossless", since some information/data can be ignored
        and be implicittly infered by human brain.
    4. Lossy compression alters the underlying data hence it isn't used in digital forensics
    5. Many forensics tools provide the option to compress the drive using lossless compression, which can reduce the size of drive to about 50%.
- Validation of the files befor and after the compression can be done my hashing using SHA1 or MD5 etc, by matching the hash of entire data before and
    after the compression.
- If the disk is to be returned to the owner, then logical acquisition can be performed in order just acquire data that is of interest.
- also it is imp to make sure that we use a reliable forensics tool that we know how to operate, also have some backup tools too.

-------

# Contingency Planning for image Acquisition
- creating multiple copies of the evidence
- not depending on a single forensics tool
- if multiple tools available then create copies of the evidence using all of them
- if only one tool available then create multiple copies of the Evidence
- creating one uncompressed image and one compressed image of the evdence
- Making sure that the tool used can read the data that resides in the HPA (Host Protected Area)
    - Because attackers can hide malicious code/data inside Host protected Area with the OS is not privy to
    - So use a tool that is able to read data at the BIOS/UEIF level.
    - **Examples**: FTKImager, Autopsy, Belkasoft, ILookIX IXImager, X-ways Replica, Image MASSter Solo etc.
- Due to the introduction of **Full disk encryption** (BitLocker in Windows) Static Acquisiton has become a difficult
  job since keys are required to decrypt the whole disk in order to gather data.
    - tools like Elcomsoft Forensic Disk Decryptor can be used to decrypt the disk if the Decryption
      keys are known.
    - Here the user's Co-operaiton is required
    - The process of decrytion (if the keys are found) can take hours.

-----

# Using Acquisitions Tools
- Makes Data acquisition from a suspect drive convenient
- Hot - Swappable drives are used for more versatility eg: USB drives, CD etc
- BUT: these drives should be used with a write - Blocker (hardware tool that prohibits write actions on to the disk).
- Because: OSs (Windows & Linux) can alter data while mounting the disks on them.

## Mini-WinFE book CD and USB drives
- Mini-WinFE : Mini windows Forensics Environment
- This Boot env is installed on to the CD/USB and is booted on the target computer
- Once booted, select the suspects HDD/SDD to in read only mode, this is done so that any metadata/data is not changed while accessing the target's drive. 
- once that is done, Using the acquisition tool in the CD/USB create an image of the suspect drive to the USB/CD.

# Linux Boot CD
- Why we need this:
	- When connecting an external drive, newer linux version and windows mount it immedieatly hence change metadata.
	- so to prevent that we need a Boot CD (just like Mini-WinFE)
- Ofcourse other way is to use a read write blocker hardware 

#### Linux ISO image for forensics
- Sone linux distributions are specially made for digital Forensics 
- has built in tools for data acquistion and analysis.
- they also have the functionality to read external drives without mounting.
- and mounting a drive can be controlled via terminal/gui.
NOTE: We use these ISO Images in our CD/USB so that it can work just like mini-winFE boot CDs

#### How to do that
- Download the specific ISO image for digital forensics
- burn that image into an USB/CD using burner s/w eg: "Roxio", "Nero" etc if using a CD.
- if using a USB then use tools such as isoToUsb.
- Then just attach the USB/CD into the suspect computer and boot it via the linux installed on it.

#### digital acquisition using Live Linux CD.
- To do this we first create a target disk where our image will be stored
	- Through Linux we can create a partition on the target disk 
	- then format that partition to FAT32
	- then use that to store the suspects computer image.
	
- ###### To format the Target Drive
	- Make sure that while creating a partition the shell is a super user, To do that use "su" command and type the password to get admin privileges
	- to create partition and format it we using the following commands
		1. fdisk \<drive location\> (for partition)
		2. mkfs.msdos -vF32 \<drive location\> (for Formatting it to FAT32)
		
- ###### To Acquire data using dd in linux	
	**NOTE:** "dd" command can copy drives that are not mounted. So it not bound by the logical structure of the file system.
	- use ***dd*** command to do a bit by bit copy of a selected drive to the target drive
	- make sure the target drive is large enough to contain the suspect drive
	- if not use the ***split*** command to segment the suspect drive to store sparse data.
	- steps:
			###### Vocabulary (for the term used): 
			- /dev/sdb5 : this is the unmounted target drive 
			- /mnt/sdb5 : this is the directory where we will mount our target drive. 
			
		1.  Boot the computer using the Live Linux CD
		2. Open shell using super user
		3. see the list of drives connected to the system using ***fdisk -l***
		4. Mount the target drive:
			- Create a directory where the drive will mount, Eg: ***mkdir /mnt/sda5***
			- using the following command to mount the /dev/sdb5 drive to the created directory: ***mount -t vfat /dev/sdb5 /mnt/sdb5*** 
			- change to the mnt/sdb5 directory ***cd /mnt/sdb5***
		5. Now use dd command using split command with inputfile as the suspect's drive. eg:
				***dd if=/dev/sdb | split -b 650m image_file.***
		6. To list all copied images use ***ls -al***

```
fdisk -l	
mkdir /mnt/sdb5
mount -t vfat /dev/sdb5 /mnt/sdb5
cd /mnt/sdb5
dd if=/dev/sdb | split -b 650m image_file.
```

##### dcfldd
- Created by Nicholas Harbor
- dd cmd what not made for digital acquistion
- so this command was made.
- has following functions:
	1. specify hexadecimal patters or text while wiping the disk
	2. Write all the error encountered in a separate log file.
	3. Supports multiple hashing schemes (MD5, SHA1, SHA384, SHA256, SHA512)
	4. Status display (indicated the amount of bytes copied)
	5. Verifies the original and the copied image after imaging
	6. Files can be segmented into multiple volumes with varying extensions (more that 99 (dd command's limit) )
command:
```
dcfldd if=/dev/sdb hash=MD5 md5log=usbimgmd5.txt split=650M of=usbimg.dat
```

- now the data is acquired to a target USB
- Next step involves using forensic imaging tools to analyzer the acquired RAW file

##### FTK Imager
- Comes with a copied license of Access Data toolKit
- uses:
	1. To create disk to image copies of a drive from a logical partition level or a physical one level.
	2. Ability to segment the image into multiple volumes while creating the disk to image copy. (650Mb for CDs and 2Gb for FAT32 drives)
	3. Used for Live Acquisition of suspect's RAM, this is done my booting the suspects computer with a Live Linux CD boot or Mini-WinFE boot CD.
	4. FTK imager by default doest not copies HPA (host protected Areas) while creating an image. So it is recommended to use a more advanced tool if HPA is present
- Steps:
	1. Boot the workstation with windows with write blockers on
	2. Connected the USB drive/CD to the workstation
	3. Start FTK imager
	4. Select source type: Physical Drive
	5. Select the actual drive whose image needs to be created from the drop down
	6. Select the type of the image that will be created from the following 4:
		i. RAW (dd)
		ii. AFF
		iii. Smart 
		iv. e01 
	7. A dilog box prompting case information will be shows, fill the information ie,. Case name, evidence number, examiner name, notes etc. 
	8. Select the destination of where the image will be stored, the image name, number of segments to be created, specify if compression is needed and how much, and specify if AD encryption is needed.
	9. then click start to start the acquisition phase, this will take time
	10. Then a dialog box asking to verify the result ie,. the hash generated etc is displayed then click close.   

--------

## Validating Data Acquisition
- Linux's inbuilt dd and dcfldd commands can be used to validate the acquired data.
- To validate data using dd we use other shell commands along with dd to validate 
- While dcfldd has it's own options to validate.
- Linux has hashing utilities built in Eg: md5sum and sha1sum.
- Chronology of validation:
	1. generate the hash of entire original/suspect drive
	2. generate the hash of all the volumes of acquired data (see dd command acquisition above)
	3. then check if they are equal.

##### Validate dd acquired data
steps:
1. boot linux using Live linux CD distribution
2. go to the /mnt/sdb5 directory where all the segments are present
3. type the command ***md5sum /dev/sdb5 > md5sum.txt*** this cmd outputs the hash of /dev/sdb5 drive into md5sum.txt file.
4. type the command ***cat image_file.\* | md5sum >> md5sum.txt*** this command is used to contat all the segments then use md5sum utility to generate the hash of the acquired data and append at the end of md5sum.txt 
5. now check the file using the command ***cat md5sum.txt*** and check if the hashes match.

##### validate dcfldd acquired data
- hash of the image can be generated while acquiring the data itself
- so use the following cmd to acquire data from a suspect drive along with the generated hash.
```
dcfldd if=\dev\sdb5 split=650M of=sdb5_img hash=md5 hashlog=hash_sdb5.log
```
- this creates multiple volumes of size 650Mb with extension .000, .001 and so on.  
- this also creates a hash_sdb5.log file where the md5 hash of the acquired data is kept.
- To verify it with the original just output the hash using md5sum utitility using the following command.
```
md5sum \dev\sdb5 > hash_sdb5_original.txt
```

# Windows Validation Methods (Digital Forensics)

## 1. Hashing in Windows
- Windows does not have built-in forensic hashing tools.
- Third-party tools are used for validation.
- Examples:
  - Hex editors (WinHex, Hex Workshop)
  - Forensic tools (Autopsy, EnCase, FTK, OSForensics)
## 2. Purpose of Validation
- Ensures acquired image is identical to original disk.
- Uses hashing algorithms (MD5, SHA-1, SHA-256).
## 3. Proprietary Image Formats
Examples:
- Expert Witness Format (.e01)
- SMART Format (.s01)
- AFF format

Features:
- Store metadata
- Store original hash value
- Allow automatic validation
- Software compares stored hash with recalculated hash

If mismatch:
- Tool alerts that acquisition is unreliable.
## 4. RAW Image Format
- RAW images do not store metadata.
- No embedded hash value.
- Manual validation required.
- Separate validation (hash) file must be saved.
- Later hash comparison ensures evidence integrity.
## 5. FTK Imager Validation
When selecting:
- .e01 (Encase file format or Expert Witness file)
- .s01 (smart)

FTK provides:
- Built-in validation report
- MD5 and SHA-1 hash values
- Hash stored inside image file

On loading image:
- Software recalculates hash
- Compares with stored hash
- Confirms acquisition integrity

----
### Raid
- Raid: Redundant Array of Independent Disks.
- Raid Systems are a computer configurations that have 2 or more physical drives/disks that act as one logical storage unit.
- The OS perceives the underlying storage as one logical unit instead of 2 more more physical storage units.
- Mainly designed to minimize data loss in times of system failure of data corruption.
- Raid systems can be configured using 2 ways:
	1. Software RAID
		- A software on the host system configures the underlying RAID
	2. Hardware RAID
		- A hardware system using it's own controllers, memory and processing which connects to the host os.
- Windows 2000 and Xp can only be configured with RAID 0 and 1
- More advanced Raid system uses RAID 5 for high end data process, storing and accessing.
##### why RAID acquisitions are hard?
1. due to its under lying configurations, design and it's size
2. mainly it's size as most of the RAID systems are pushing above ExaBytes

RAID 0:
1. Involves a configuration of 2 or more disks
2. Tracks of each disks seems contiguous by the implemented logical addressing schemes. Hence it seems as one bit storage unit
3. Data is **stripped** to be saved in multiple disks. Eg: 128Gb data is cut in half if 2 disks are involved and are stored in each of these disks
4. advantages:
	1. Has increased access speed
	2. can store large amounts of data
5. disadvantages
	1. Lack of Redundancy: if fails the no way for recovery.
	\<refer image from classroom's pdf \>
	
RAID 1:
1. Data **mirroring** takes place: when OS writes the data is stored identically on all the disks in the system
2. This requires more storage
3. This also add more cost hence making it more expensive than RAID 0
4. minimum 2 disks required
5. Adv:	
	1. Recovery if system fails and data is corrupted.
	2. If one drive fails then OS switches of another hence eliminating some downtime of the system
6. Dis:
	1. more expensive

RAID 2:
1. Data is stripped on a bit level: Meaning each individual bits are distributed across multiple disk in the RAID system and an ECC (error correction code) file is calculated and stored in a other remaining disks, in case of disk failure. 
2. Provides better data integrity than RAID 0 and RAID 1 systems
3. Provides rapid access and increased storage capabilities just like RAID 0 (because stripping is done)	
4. In comparison RAID 2 is slower than RAID 0 because each disks are browsed in order to get the data of a whole file.
5. minimum 2 disks req
6. Adv:
	1. Increased Data storage
	2. Better Data integrity
	3. Better measures for when disks are corrupted
7. Dis:
	1. Expensive
	2. Slow
	
RAID 3:
8. Same as RAID2 but 
	1. Uses byte level data stripping
	2. Has just one dedicated parity disk storing ECC for data recovery.
9. Disadv and adv are same
10. RAID3 is faster than RAID2
11. minimum 3 disks req

RAID4:
1. Same as RAID3 and RAID2 but
	1. Uses Block level data stripping
	2. Has dedicated parity disk containing ECC for recovery.
2. RAID 4 is faster if the data is small (because the stored data will not use multiple disk hence only small no of disks are used in order to fetch data)
3. RAID 4 is slower if the data is a large sequential Data
4. Minimum 3 disks required

RAID 5:
1. Byte level stripping takes place (same as in RAID 0 and RAID 3)
2. Unlike RAID 3 parity is placed in each of the disks, hence more scope of data recovery when failure. 
3. Minimum Drives required: 3
4. recoverable upto single disk failure
5. Diff between RAID 5 and RAID 3
	1. RAID 5 is more faster because each disk has parity bits so cooperation of all disks is not required
	2. RAID 5 is used more commonly in real applications
	3. RAID 5 has distributed parity, while RAID 3 has single parity

RAID 6:
1. Block level stripping 
2. minimum 4 disks req
3. can survive 2 disk failures
4. contains redundant parity blocks in each disks
5. diff between 6 and 5
	1. Same for read performance 
	2. RAID 6 can survive 2 disk failures
	3.  RAID 6 write is slower due to calculation of more ECC in each disks.

RAID 10:
1. Also knows as RAID 1 + 0.
2. uses both mirroring and stripping
3. combination of RAID 1 and 0
4. fast access and redundancy of data storage

RAID 15:
1. Mirroring and stripping with ECC code on each disks
2. combination of RAID 1 and RAID 5 
3. faster access and redundancy
4. It is the most costly RAID Configuration

### Acquiring RAID Disks
- Before starting the Acquisition there are sone concerns that needs addressing 
#### Concerns before RAID Acquisition 
1. Do we have large enough space to hold the data from a RAID system	
2. What is the Architecture of the RAID system in question
3. Do all the disks in the RAID needs to be connected so that OS can see the whole data?
4. Can your forensic tool even copy the disks data correctly?
5. Can you forensic tool read the forensically copied disk image of a RAID System?
6. Can your Forensic tool merge the distributed data across multiple RAID disks into a large virtual RAID drive?
#### Raid Acquisition of small systems
- Also RAID acquisition of small systems are possible due to the availability of large USD drives.
	- Ex: 
		- A RAID 0 system having 8 32GB disks can be acquired using a USB drive of around 300GB of storage.
		- Also Almost all forensic tools can analyse the image because it acts as a one large drive instead of 8 32GB drives.
		- If a proprietary file format is used then even less storage is consumed if compression is applied.

- Other way for acquiring raid data is to have multiple drives of same storage space as each disks of the RAID system.
	- Ex:
		- let the suspect RAID be: 3 - 2TB raid 0 configuration
		- Then 3 2TB drives are required for acquisition
		- If we use AFF or Proprietary File Format then we can get away will less than that too.
#### vendors providing RAID acquisition features
- Vendors that have RAID acquisition features in their product (they specialize in one or two types of RAID system only)
	1. Guidance Software EnCase
	2. X-ways Forensics
	3. Access Data FTK
	4. Runtime software
	5. R-tools Technologies
- A good investigator must know which vendor speacializes in which RAID and keep up to data with further developments.

- Tools like Runtime Software and R-tool Technologies are mainly ***Data recovery tools*** but they provided RAID recovery features, and hence repair broken RAID 0 and 5 systems.
- What does RAID reconstruction involves?
	- Acquire data from a broken RAID 0 or 5 system
	- Create another RAID with exact configurations
	- Then load the captured image on this new RAID
	- Work on this to fix the broken RAID
	- Then once fixed change the original RAID with the fixed data.
	
- What does R-tool technologies do to recover RAID?
	- It creates a virtual RAID system instead of setting up an actual physical RAID 
	- All the repair work is done on this virtual RAID in order to fix it.
#### Acquisition when RAID is very large
- Acquiring the whole RAID which has a storage of more that multiple terabytes becomes impractical
- So we use sparse or logical acquisition in order to meet our agenda/investigation requirements.
- consulting the forensics vendor is a wise choice when every attempting to acquire a RAID.
- Carrying a portable RAIDbank is recommended while investigation of any crime scene. (cuz you never know 😭 );

----

## Remote Network Forensic acquisition tools

##### Introduction
- Modern forensic tools can remotely acquire full disks or specific data fragments over a network.
- Some tools require manual action on the suspect system, while others can push a remote access program through a seemingly un-harmful link.
- Remote acquisition saves time and reduces the chance of alerting the suspect.
- Most remote acquisitions are performed as live acquisitions and require administrative privileges.
- Security software or user-installed protections on the suspect system may detect or block remote access attempts.

#### Remote Network Live Forensics using various tools

##### Remote Acquisiton using ProDiscover
- ProDiscovery incident Response tool is integrated with capabilities of network intrusion and live forensics
- Features provided for remote network live forensics:
	1. Capturing volatile system state information
	2. Analysis of all the current running processes
	3. Ability to analyse hidden / unnoticed processes that may run spyware / malware
	4. Run Hash comparisons to check for any known Trojal or Rootkits. 
	5. To create an inventory containing the hash of every running process in order to check if any attacks were done
- This involves 2 main steps:
	1. Connecting the remote (usually the suspect) computer with the warkstation
	2. Then using the usual method of data acquisition via ProDiscover 
- The connection is established when "PDserver remote agent" a utility for remote network live forensics for ProDiscover needs to be installed on the remote (usually the suspect) machine. 
- Ways to install ***PDserver*** on a machine are:
	1. Trusted CD: Manually installing the PDserver using a CD.
	2. Preinstallation: Installing PDserver when setting up the OS of a system in a network. This is often done as a way to deal with any attacks/intrusions on the network and a quick incident response.
	3. Pushing out and running remotely: installing PDserver on the suspect's machine remotely. 
- Other benefits provided for communication between remote and workstation communications are:
	1. Password protected: any access to the PDserver is password protected
	2. Encryption: All the communication happening between is encrypted (AES or twofish encryption)
	3. Proper communication protocols: each packet is labeld with a global unique Identifiers (GUIDs) so that no insertion of foreign packets can be done
	4. Digital Signatures to check for any tampering of PDserver with before or during the connection

##### Remote Acquisition using EnCase
1. first remote network acquisition and analysis tools to be released in the market.
2. features:
	1. Can investigate external and internal network over a large geographical area.
	2. support multiple OSs and file systems.
	3. triage and help in determining the usage a computer system for investigation
	4. Can search 5 systems simultaneously

##### Remote Acquisition with R-tools R-studios
1. R-tools suite mainly used for data recovery
2. R-studio network edition can access network of computer systems remotely
3. Data acquired by R-studio network edition is in RAW format
4. capable of recovery many different file systems

##### Remote Acquisition with wetStone US-Latt Pro
- US - LATT Pro is a member of the suit provided by WetStone
- Can connect to a remote network and acquire the data of all the drives connected to it.

##### Remote Acquisition with F-response
- It is a vendor-neutral Remote Accesses Utility
- Works with any forensic tool
- Sets up a read only access connection between the workstation and the suspects machines
- gives a raw physical level view of the data in all the connected disks.
- the raw data can then be analyzed using any forensic tools.
- Sold in 4 different versions:
	1. Enterprise Edition
	2. Consultant Edition
	3. Consultant + convert Edition
	4. TACTICAL Edition.

-------

### Using other Forensic Acquisition Tool
- Following are the other commercial paid forensics tools. 
	1. Passmark Software - ImageUSB: By Passmark Software, the ImageUSB used for OSForensic Analysis. Can be used to create bootable flash drives
	2. ASR Data SMART: Tool that lets you create an image of a suspect drive. can create image in AFF or proprietary format and includes the following capabilities:
			1. Robust Data reading of corrupted (bad) sectors
			2. Mounting suspect drives in write only modes
			3. Mounting target drives including NTFS in read/write modes
			4. Option Compression schemes while creating the image.
	3. Runtime Software:
		1. Raid Reconstructor
		2. DiskExplorer for FAT
		3. DiskExplorer for NTFS
		4. Creating an image in RAW format
		5. Compression and segmenting capabilities for archiving
		6. Accessing Network Computers' Drives.
	4. ILookIX IXImager:
		1. IXImager runs from a bootable thumb drive CD/DVD
		2. It is stand alone proprietary software that is compatible with only ILookIX.
		3. It's IXImager proprietary format can be converted to RAW if other forensic tools are used.
	5. SourceForge:
		1. Source forge provides several applications for security, Analysis and investigations

----

### Performing Live Acquisitions
#### Introduction:
1. Useful when dealing with network intrusions, attacks, checking the network if any member is doing something they are not suppose to.
2. Getting all the information before the system goes down has become a necessity
3. Some viruses/malware tend to delete all its footprint from the system when it shuts down
4. hence it is necessary that we analyse the system while it is running
5. Also when Live forensics is done RAM data changes since the process of conducting a live forensics change it hence the RAM information cannont be reproduced.
6. OOV (order of volatility):
	- A measure of how long a piece of information stays on the device
	- This is a major issue while conducting a Live Forensics
	- Ram -> as low as 1 millisec
	- Secondary storage -> as long as 10 years

##### General Procedure for a Live Forensics
1. if suspect is on the same network then use a suitable live network forensics tool to start gather data
2. If not then create a Live Linux boot CD or a Mini-WinFE CD/DVD, insert it into the suspect's system.
3. Make sure to log all the activities you are doing somewhere.
4. Use a network usb to send all the data captured from the RAM, If no network USB is setup, then use an external drive to store that data there.
5. start capturing the RAM using 
	1. WindowScope
	2. Magnet Axiom
	3. FTK imager
	4. OSForensic tools etc
6. Next step is more specific towards the goal of the forensics
	Eg: we might be investigating intrusion so we need to detect any root-kit being used, for this we might use softwares like PChunter or MalwareBytes Anti-Rootkit.
7. Also make sure to get a forensically sound hash values of every files recovered during the whole process.

##### Performing a Live Acquisition in Windows
1. tools that can be used for RAM caupturing:
	1. Mandiant Memoryze 
	2. Belkasoft RamCapture
	3. Kali Linux (priviously known BackTrack)
2. Can be done using GUI tools as well but has some cons:
	1. Uses home resources hence making the system slow
	2. Can show false reading in windows OSs.
3. Kali Linux has over 300 cli tools that give you more control and gives accurate reading. 
	eg: Sleuth Kit.