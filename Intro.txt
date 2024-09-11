Cold system forensics emerged as a direct response to a malicious technique known as a cold boot attack. Attackers would use this technique to take advantage of the fact that data in a computer's RAM persists for a short period, depending on the RAM's temperature, after the system is powered off. The cooler the RAM chips are, the longer the data can be retained. Attackers could rapidly reboot a compromised machine to access sensitive information, such as encryption keys, passwords, or in-memory data, before it is completely erased.

To counter this threat, researchers began exploring methods to preserve and analyse the contents of a system's volatile memory even when powered off, marking the initiation of cold system forensics.

Analysis of a system in its powered-off state ensures that forensic analysts preserve the integrity of evidence, preventing potential tampering and modification. This is particularly crucial in legal proceedings where the admissibility of evidence hinges on its unaltered state.

+---------------+---------------+---------------+
|  Aspect      | Cold Forensics | Live Forensics |
+---------------+---------------+---------------+
|  System State |  Examines     |  Examines     |
|               |  powered-off  |  running      |
|               |  systems      |  systems      |
+---------------+---------------+---------------+
|  Evidence     |  Minimal risk |  High risk    |
|  Integrity    |               |               |
+---------------+---------------+---------------+
|  Data Capture |  Comprehensive|  Limited to   |
|               |  capture of   |  active data  |
|               |  entire drives|               |
+---------------+---------------+---------------+
|  Volatile     |  Cannot       |  Captures     |
|  Memory Access|  retrieve     |  volatile data|
|               |               |  (memory,     |
|               |               |  network)     |
+---------------+---------------+---------------+
|  Time Efficiency|  Time-consuming|  Faster      |
|               |               |  identification|
|               |               |  of threats    |
+---------------+---------------+---------------+
|  Data Volume  |  Suitable for |  Limited by   |
|  Handling     |  large data   |  system resources|
|               |  volumes      |               |
+---------------+---------------+---------------+
|  Legal        |  Ideal for    |  May alter    |
|  Suitability  |  legal cases  |  evidence,    |
|               |  where integrity|  less suitable |
|               |  is paramount  |  for legal cases|
+---------------+---------------+---------------+
|  Access to    |  Risk of losing|  Immediate    |
|  Encrypted Files|  access if    |  access while  |
|               |  passwords are |  the system is |
|               |  reset        |  running       |
+---------------+---------------+---------------+

The order of volatility is an essential concept in digital forensics. It refers to the sequence in which data should be collected based on its volatility or likelihood to change. This order helps forensic analysts prioritise data acquisition, with the most ephemeral data being captured before it is lost or altered.

A typical order from the most volatile to the least volatile might look as follows:
+---------------------------------------+
|  VOLATILE DATA                         |
+---------------------------------------+
|  CPU registers and cache              |
|  - Most volatile data, lost on power down  |
|  - Insights into current operations     |
+---------------------------------------+
|  Routing Table, ARP Cache, Process Table,  |
|  Kernel Statistics, and RAM            |
|  - Data changes rapidly                |
|  - Reveals running processes and network  |
|  connections, helps identify malicious  |
|  activity                              |
+---------------------------------------+
|  TEMPORARY FILE SYSTEMS               |
|  - Data cleared on reboot, changes frequently|
|  - Uncovers recently accessed files or  |
|  applications on a host               |
+---------------------------------------+
|  LESS VOLATILE DATA                    |
+---------------------------------------+
|  Hard Disk                             |
|  - Data undergoes alterations and deletions|
|  - Imaging provides a comprehensive snapshot|
|  of all stored data, including deleted  |
|  files and fragments                   |
+---------------------------------------+
|  REMOTE LOGGING AND MONITORING DATA    |
|  - Relatively stable, less likely to change|
|  - Record of network activity and system  |
|  events over time                      |
+---------------------------------------+
|  PHYSICAL CONFIGURATION AND NETWORK    |
|  TOPOLOGY                              |
|  - Documents infrastructure and context  |
|  of investigation                     |
|  - Collects data transmitted over network  |
|  for forensics                         |
+---------------------------------------+
|  ARCHIVAL MEDIA                        |
|  - Stored offline, such as tapes and    |
|  optical discs                         |
+---------------------------------------+

Advanced encryption methods, such as AES-256, protect data at rest. Encryption ensures the data remains unreadable without the decryption key, even if unauthorised access occurs.

To maintain the integrity and chain of custody of forensic data, we can follow the following guidelines:

    Document every step: No matter how small an action is during the forensic analysis, it must be documented and aligned with whoever is handling the evidence, what time was taken, and the reasons behind their access to the evidence.
    Hashing: Using cryptographic hash functions such as MD5 and SHA-1 to create unique data fingerprints and verify that it has not been altered.
    Write blocking: Using write blockers helps prevent any modification of the original data.
+---------------------------------------+
|  TOOLS FOR COLD SYSTEM FORENSICS      |
+---------------------------------------+
|  DISK IMAGING TOOLS                  |
|  - dd and dc3dd: Command-line utilities  |
|    for exact bit-by-bit copies of hard drives|
|  - Guymager: Graphical disk imaging tool  |
|    for Linux, supports various disk image  |
|    formats, provides write-blocking and    |
|    checksums for data integrity          |
|  - FTK Imager: Comprehensive disk imaging  |
|    tool, supports various media types,    |
|    provides data previewing and multiple  |
|    output formats                        |
+---------------------------------------+
|  MEMORY FORENSIC TOOLS                |
|  - Volatility: Robust framework for     |
|    extracting digital artefacts from    |
|    volatile memory (RAM) dumps          |
+---------------------------------------+
|  DISK IMAGE ANALYSIS TOOLS            |
|  - The Sleuth Kit (TSK): Collection of  |
|    command-line tools for analysing disk |
|    images and recovering deleted data   |
|  - Autopsy: Graphical interface for TSK  |
|    functions, provides keyword searches,  |
|    timeline analysis, and file carving  |
|    features                             |
|  - EnCase: Professional-grade forensic  |
|    tool for deep forensic investigations|
+---------------------------------------+
|  TECHNIQUES FOR ANALYSING DISK IMAGES  |
|  AND MEMORY DUMPS                     |
+---------------------------------------+
|  MOUNTING AND EXPLORING DISK IMAGES    |
|  - Mounting disk image, creating virtual |
|    representation of physical drive     |
|  - Key considerations: image format    |
|    compatibility, write-blocking, and   |
|    using virtual machines for isolated  |
|    analysis                             |
+---------------------------------------+
|  EXTRACTING RELEVANT ARTEFACTS        |
|  - Identifying and extracting critical  |
|    evidence from disk image            |
|  - Techniques: keyword searching, file  |
|    signature analysis, registry analysis,|
|    email extraction, and web history    |
|    extraction                           |
+---------------------------------------+
|  RECOVERING DELETED DATA              |
|  - Forensic techniques: file carving,   |
|    unallocated space analysis, and     |
|    specialized data recovery tools     |
|  - Understanding file system structures |
|    is crucial for effective recovery    |
+---------------------------------------+
|  ANALYSING MEMORY DUMPS               |
|  - Capturing contents of system's RAM   |
|  - Insights into running processes,     |
|    network connections, loaded modules, |
|    and other volatile data            |
+---------------------------------------+
|  ASSOCIATED RISKS AND COMMON MISTAKES |
|  - Data Integrity: Ensuring integrity  |
|    of disk image, using cryptographic  |
|    hash functions and write-blocking    |
|  - Misinterpretation of data: Correlate |
|    evidence from multiple sources,     |
|    consider limitations of tools used  |
|  - Documentation: Maintain detailed and |
|    accurate documentation of all steps  |
|    taken during analysis process       |
+---------------------------------------+
