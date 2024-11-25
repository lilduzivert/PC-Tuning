# PC-Tuning

Caution

In order of performance scaling, Hardware > BIOS > Operating System.

Caution

Do NOT blindly trust or believe everything you read online (including this resource) and typically doubt everything. Instead, validate statements through evidence, research and benchmarks.

Caution

Do NOT apply random, unknown or undocumented changes, programs and script to your system without a comprehensive understanding of what they are changing and impact they have on security, privacy and performance.

1. Table of Contents
1. Table of Contents
2. Introduction
3. Benchmarking
4. Physical Setup
5. Cooling
6. BIOS/UEFI
6.1. Partition Style
6.2. Consider Windows Version
6.3. BIOS Recovery Methods
6.4. BIOS Updates
6.5. BIOS Microcode
6.6. Accessing Hidden Options
6.7. Unnecessary Devices
6.8. Resizable Bar (ReBAR)
6.9. Hyper-Threading/Simultaneous Multithreading
6.10. Power States
6.11. Virtualization/SVM Mode
6.12. Power-Saving
6.13. Trusted Platform Module (TPM)
6.14. Compatibility Support Module (CSM)
6.15. Secure Boot
6.16. Fast Startup, Standby and Hibernate
6.17. Spread Spectrum
6.18. Legacy USB Support
6.19. Software Installation Options
6.20. PCI Link Speed for Devices
6.21. Fan Curves
6.22. BIOS Profiles and Backups
7. Configure USB Port Layout
7.1. Reviewing Accessible USB Ports
7.2. Layout Planning
7.3. Plugging In Devices
8. Configure Peripherals
8.1. Cleaning
8.2. Onboard Memory Profiles
8.3. RGB Lighting Effects
8.4. DPI
8.5. Report Rate
8.6. Polling Stability Analysis
8.7. Monitor
9. Stability, Hardware Clocking and Thermal Performance
9.1. Temporary Operating System
9.2. General Information
9.3. Error Correction
9.4. Thermal Management
9.5. Load-line Calibration
9.6. GPU
9.7. RAM/CPU
9.8. Stress-Testing Tools
10. Install Windows
10.1. Storage Partitions
10.2. What Version of Windows Should You Use?
10.3. Downloading and Preparing a Stock Windows ISO
10.4. ISO Sources
10.5. ISO Preparation
10.6. Fetching Required Files
10.7. Booting Into the ISO
11. Configure Windows
11.1 OOBE Setup
11.2. Unrestricted PowerShell Execution Policy
11.3. Importing bin Folder
11.4. Process Mitigations (Windows 10 1709+)
11.5. Merging Registry Options
11.5.1. Registry Options Documentation
11.5.2. Applying Options
11.6. Installing Drivers
11.7. Windows Server Specific Options (Windows Server)
11.8. Privacy Options (Windows 8+)
11.9. Search Indexing
11.10. Time, Language and Region
11.11. Web Browser
11.12. Scheduled Tasks
11.13. Activate Windows
11.14. Declutter Interface
11.15. Visual Effects
11.16. Superfetch and Prefetch
11.17. Operating System and Partition Name
11.18. Show Tray Icons
11.19. Hibernation
11.20. Runtimes
11.21. Handling Bloatware
11.22. Optional Features
11.22.1. NET 3.5
11.23. 7-Zip
11.24. Graphics Driver
11.25. MSI Afterburner
11.26. Display Resolutions and Scaling Modes
11.27. Open-Shell (Windows 8+)
11.28. Spectre, Meltdown and CPU Microcode
11.29. Power Options
11.30. Process Explorer
11.31. Memory Management Settings (Windows 8+)
11.32. Network Adapter Options
11.33. Audio Devices
11.34. Device Manager
11.35. Device Power-Saving
11.36. Event Trace Sessions (ETS)
11.37. File System
11.38. Message Signaled Interrupts
11.39. XHCI Interrupt Moderation (IMOD)
11.40. Control Panel
11.41. Configuring Applications
11.41.1 NVIDIA Reflex
11.41.2 Framerate Limit
11.41.3. Register Game in Config Store
11.41.4 Presentation Mode
11.41.5. Game Mode
11.41.6. Media Player
11.41.7. QoS Policies
11.42. Kernel-Mode Scheduling (Interrupts, DPCs and more)
11.42.1. GPU and DirectX Graphics Kernel
11.42.2. XHCI and Audio Controller
11.42.3. Network Interface Card
11.43. User-Mode Scheduling (Processes, Threads)
11.43.1. Starting a Process with a Specified Affinity Mask
11.43.2. Specifying an Affinity Mask for Running Processes
11.44. Reserved CPU Sets (Windows 10+)
11.44.1. Use Cases
11.45. Analyzing Event Viewer
11.46. Virtualization Based Security (VBS)
11.47. CPU Idle States
11.47.1. Enable Idle States (default)
11.47.2. Disable Idle States
11.48. Thread Quantums and Scheduling
11.48.1. Bitmask Explaination
11.48.2. Win32PrioritySeparation Values
11.49. Clock Interrupt Frequency (Timer Resolution)
11.50. Paging File
11.51. Cleanup and Maintenance
2. Introduction
This resource can be used to whatever extent you prefer, but be sure to heed the warnings. The primary objective of this resource is to utilize an evidence-oriented approach to explore practices for tuning Windows-based systems for a variety of use cases, covering hardware, operating system, and software configurations. If your daily workflow allows for Linux, then use it. Linux offers far more flexibility than Windows ever will in various aspects. Especially for "power users". This resource is designed to accommodate a broad audience, addressing various goals such as enhancing security and privacy however, it generally favors and caters for gaining a competitive edge in games and executing real-time tasks. There is a strong emphasis on encouraging users to make the changes themselves, with minimal use of scripts to ensure transparency and prevent unintended modifications to the reader's system.

The reader is expected to follow the sections in sequential order as subsequent steps are contingent upon the completion of preceding steps. Therefore, each section is numbered.

2.1. Other Resources
BoringBoredom/PC-Optimization-Hub
Calypto's Latency Guide
djdallmann/GamingPCSetup
Windows Internals, Part 1: System Architecture, Processes, Threads, Memory Management, and More
Windows Internals, Part 2
3. Benchmarking
Benchmarking is employed to objectively assess and eliminate the influence of potential placebo effects in system modifications while evaluating the quality or characteristic of a given change. In the context of this resource, it typically refers to measuring performance scaling after making certain changes to your system. It is important to learn and understand what is involved in the benchmarking process as you will need to carry out your own experiments to assist in decision-making such as identifying whether a certain change results in a performance regression or what settings to use in-game. For given changes, ask yourself questions such as "What am I trying to achieve?", "What is my goal?", "What am I trying to improve with this change?", "What is this change supposed to affect?", "How can the effects of this change be measured and demonstrated?".

FrameView - PC Latency in games that support PC Latency Stats and frame pacing
Frame Latency Meter
PresentMon - Various metrics such as frame pacing and GPU Busy. See a full list here
Windows Performance Toolkit - Advanced performance analysis library for Windows. Extract ISR/DPC execution time data with xperf
Mouse Tester - Mice performance metrics (e.g. polling interval, X/Y counts and more plots against time)
NVIDIA Reflex Analyzer - End-to-end latency
Frame-Time-Analysis - Analyze CSV data logged by the programs mentioned above including 1%, 0.1% lows metrics
Latency Grapher - Analyze latency results from RLA, FrameView and PresentMon
4. Physical Setup
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

New installations of Windows are recommended after major hardware changes including but not limited to motherboards, CPUs, platforms and chipsets

See Higher Airflow Cases | Calypto

Avoid multi-CCX/CCD Ryzen CPUs due to the latency penalty incurred from inter-CCX/CCD communication (1, 2)

See Low Latency Hardware | Calypto

Avoid overtightening screws

Verify whether all connectors are seated properly and that none are loose (e.g. PSU cables)

Disconnect unnecessary and unused devices from your setup including peripherals, LEDs, RGB light strips, USB devices, storage drives, wireless receivers and more

Favor wired over cordless devices (e.g. peripherals, Ethernet) due to the degraded performance and inconsistency associated with wireless devices, aggressive power-saving features for a longer battery life along with the downside of being negatively affected by interference and transmission overhead (1, 2, 3, 4, 5)

An SSD or NVMe storage is strongly recommended due to the degraded performance (1) and excessive interference of HDDs. Ensure that there is always a sufficient amount of free space as SSDs slow down as they are filled up (1) however most drives are overprovisioned from factory (1, 2)

Assess the condition and performance of storage devices with CrystalDiskInfo and CrystalDiskMark to determine whether they require replacement or maintenance

Check and update firmware for devices including but not limited to NVMe, NICs, peripherals and more. Beware of problems brought up in reviews and forums regarding specific firmware versions if applicable

Install the RAM in the correct slots by referring to the motherboard manual. Consider the memory trace layout when determining the amount of sticks to use

See Motherboard Memory Layouts | buildzoid
Favor PCIe ports that are connected directly to the CPU rather than chipset. This typically applies to M.2, NVMe drives and GPUs. This can be determined with the PCIe Bus category in HWiNFO. Additionally, ensure that all your PCIe devices under the PCIe Bus category are running at their rated specification such as x16 3.0 (example). The current link width/speed of the device should match the maximum supported by the device. For certain devices such as GPUs, the link speed may decrease when idling. In these situations, place the device under load to get a meaningful reading

IRQ sharing is problematic and is a source of high interrupt latency (1). IRQ conflicts can be assessed by typing msinfo32 in Win+R then navigating to the Conflicts/Sharing section. The causes may be due to the hardware or software configuration. To isolate potential hardware-related causes, enable Message Signaled Interrupts on the problematic device then restart the system. If the device still shares an IRQ, this can indicate incorrectly configured hardware

If multiple onboard Ethernet NICs are present, consider using the one that supports MSI-X by checking in MSI Utility or GoInterruptPolicy as it is required for Receive Side Scaling to function properly (1). This can be achieved by plugging the Ethernet cable into the port that corresponds to the desired NIC on the motherboard

Measure and minimize bufferbloat as it is a cause of high latency and jitter in packet-switched networks caused by excess buffering of packets (1, 2)

See Waveform Bufferbloat and Internet Speed Test | Waveform
See How to test your Internet Ping (PingPlotter) | Netduma
See What Can I Do About Bufferbloat? | Bufferbloat.net
See stoplagging.com
Avoid daisy-chaining power cables anywhere in your setup

See Installation Remark for High Power Consumption Graphics Cards | Seasonic
Favor shielded cables and avoid unnecessarily long ones as they offer more protection against interference (1)

Ensure that there is a moderate amount of space between cables to reduce the risk of coupling

Clean dust from components and heat sinks as they have the potential to cause short circuits and reduce airflow (1). Be careful in regard to voltage feedback to the motherboard when dusting case fans

Clean the contact pins and connectors of components. Use compressed air to remove dust from slots before installing components such as PCIe, NVMe, RAM and more

Insert the display cable into the discrete GPU if present instead of the motherboard

Minimize GPU sag with an anti-sag bracket or similar to prevent damage to the PCIe contacts and the slot itself

Multi-monitor setups have the potential to introduce processing overhead (1)

5. Cooling
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

If you plan on overclocking, consider the points below to maximize temperature headroom and overclocking potential. It is important to note that lower temperatures can affect other variables even if you are not overclocking such as CPU boosting behavior as the boosting algorithm is affected by temperature and much more

Remove the side panels from your case as they tend to trap heat or consider an open-bench setup (beware of dust)
Delid your CPU and use liquid metal for a significant thermal improvement depending on the quality of the IHS (1). Direct die and lapping are also worth considering however users should assess the risk with carrying out these procedures
Avoid tower and air coolers due to limited cooling potential (1) and lack of space for fans to cool other components such as RAM and VRMs
Remove the heat sink from your RAM as they tend to trap heat due to them being attached to the PCB with foam or glue (1). Replace them with higher quality heat sinks and pads as hotspots can incur with naked RAM. Get creative with mounting a fan (140mm recommended) over them using cable ties
Mount a fan over VRMs, PCH and other hot spots
Replace thermal pads with higher-quality ones if the stock pads are inadequate
Reapply the thermal interface material on the GPU due to factory application of it often being inadequate and optionally replace the stock fans with higher quality ones
Consider contact frames and offset mounts if applicable

See Investigating Intel’s CPU Socket Problems | Thermal Grizzly Contact Frame Benchmark | Gamers Nexus
See Noctua Releases Offset Mounting for Improved Cooling Performance on AMD AM5 CPUs | Noctua
Use high-quality thermal interface material and an adequate amount upon application

See Best Thermal Paste for CPUs | Tom’s Hardware
Assess contact patches on the IHS/Die and cold plate

Mount your AIO cooler properly

See Stop Doing It Wrong: How To Kill Your CPU Cooler | Gamers Nexus
Use non-RGB fans while favoring ones with a high static pressure as mesh filters, radiators, heatsink fins and more obstruct airflow

See PC Fans | Calypto
Ensure not to overload the motherboard fan header, especially if you are using fan splitters

Use an M.2/NVMe heat sink to reduce temperatures (1) and optionally mount a fan over it

6. BIOS/UEFI
As a general rule of thumb, ensure that the settings you are changing results in positive performance scaling and make note of them for future reference/backtracking to resolve potential issues. I would recommend resetting settings to factory defaults to work with a clean slate in case anything was misconfigured initially.

6.1. Partition Style
If you aren't already using the partition style you would like to be using, you should switch now because some settings listed in this section depend on the partition style (search for "GPT/UEFI" in this section). GPT/UEFI is recommended for most systems as it offers the most compatibility (1). The current partition style can be determined by typing msinfo32 in Win+R. The recommended method to convert the partition style is to wipe and convert the disk using diskpart within Windows setup (1).

See How To Convert MBR to GPT During Windows 10/8/7 Installation | MDTechVideos
6.2. Consider Windows Version
Consider what Windows version you will be using because some settings listed in this section depend on the Windows version being used (search for "Windows" in this section). Read section What Version of Windows Should You Use? to help decide which version best suits your requirements.

6.3. BIOS Recovery Methods
Modifying BIOS is never without risks. Explore methods to flash a stock BIOS such as USB flashback or a CH341A programmer if clearing CMOS does not restore everything to its original state.

6.4. BIOS Updates
Check for BIOS updates and positive changes in the change logs (e.g. increased memory stability). Beware of problems brought up in reviews and forums regarding specific BIOS versions if applicable.

6.5. BIOS Microcode
Warning

🔒 Upgrading or downgrading microcode may negatively impact security and expose the system to vulnerabilities. Users should evaluate the security risks associated with modifying the specified setting.

Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

On much older platforms and CPUs, BIOS-level Spectre, Meltdown and other CPU microcode patches had the ability to drastically influence performance which isn't so much the case with modern systems nowadays. CPU-Z's validation feature exposes the microcode version and it was possible to manipulate microcode and their versions within the BIOS using tools such as MMTool. Nonetheless, this is not necessarily required to be changed on modern platforms and is here as an informative note.

6.6. Accessing Hidden Options
Motherboard vendors hide and lock a lot of settings so that they aren't visible to a regular user. For clarification, unlocking BIOS corresponds to making hidden settings visible and accessible. The easiest approach to take is to change the access levels within the BIOS using UEFI-Editor then flash it which will result in hidden options available in the UEFI. An alternative approach is to configure what is already accessible in UEFI then access hidden options by reading and writing to NVRAM using GRUB (script generator) or SCEWIN.

6.7. Unnecessary Devices
Generally, follow the rule of "If you're not using it, disable it". It is preferable to physically disconnect components if possible, but this typically includes NICs, WLAN, Bluetooth, High Definition Audio (if you are not utilizing motherboard audio) controllers, integrated graphics, SATA, RAM slots, onboard devices visible in USB Device Tree Viewer (e.g. LED controllers, IR receivers) and more. Keep in mind that some motherboards have the High Definition Audio controller linked to the USB controller (1) so don't get confused if this is encountered in the USB device tree.

6.8. Resizable Bar (ReBAR)
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

See this for an overview of what Resizable Bar is. It is worth noting that ReBAR can result in a performance regression in some games (1) so carry out your own benchmarks.

ReBAR requires the GPT/UEFI BIOS mode and Above 4G Decoding to be enabled. For unsupported motherboards, consider viewing ReBarUEFI/NvStrapsReBar. To verify that Resizable Bar is enabled, check the status with GPU-Z.

6.9. Hyper-Threading/Simultaneous Multithreading
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

If you have enough CPUs for your application then consider disabling Hyper-Threading (HT)/Simultaneous Multithreading (SMT). This feature is beneficial for highly threaded operations such as encoding, compiling and rendering however using multiple execution threads per CPU increases contention on processor resources and is a potential source of system latency and jitter (1). Disabling HT/SMT has the additional benefit of increased overclocking potential due to lower temperatures which can affect performance positively or negatively in some games hence, I would recommend benchmarking these options thoroughly and not blindly disabling them.

6.10. Power States
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

To be completed.

6.11. Virtualization/SVM Mode
Disable Virtualization/SVM Mode and Intel VT-d/AMD-Vi if applicable as they can cause a difference in latency for memory access (1). Virtualization also has the potential to affect BCLK (1). The virtualization status can be verified using Task Manager's CPU section.

6.12. Power-Saving
Power-saving has no place on a machine executing real-time tasks. These features can be named differently, including but not limited to ASPM (Active State Power Management) (e.g. search for L0, L1), ALPM (Aggressive Link Power Management), Power/Clock Gating and more. You can also look out for options named power management or power saving. Search the internet if you are unsure whether a given setting is power-saving related.

6.13. Trusted Platform Module (TPM)
Warning

🔒 Disabling TPM may negatively impact security and expose the system to vulnerabilities. Users should evaluate the security risks associated with modifying the specified setting.

Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

Disable Trusted Platform Module as it may cause the system to enter System Management Mode (SMM) via System Management Interrupts (SMIs) (1) which are high priority unmaskable hardware interrupts which cause the CPU to immediately suspend all other activities, including the operating system (1). On Windows 11, a minority of anticheats (Vanguard, FACEIT) require it to be enabled and its status can be verified by typing tpm.msc in Win+R.

6.14. Compatibility Support Module (CSM)
MBR/Legacy requires Compatibility Support Module to be enabled and typically, only the storage and PCIe OpROMs are required, but you can enable all of them if you are unsure. Disable CSM if you are using GPT/UEFI with the exception being Windows 7 GPT/UEFI as it requires CSM and OpROMs unless you are using uefiseven. Disable CSM if you are using Resizable Bar.

6.15. Secure Boot
Warning

🔒 Disabling Secure Boot may negatively impact security and expose the system to vulnerabilities. Users should evaluate the security risks associated with modifying the specified setting.

On Windows 11, a minority of anticheats (Vanguard, FACEIT, THE FINALS) require Secure Boot to be enabled. If something fails due to Secure Boot being enabled such as bootable tools, I recommended temporarily disabling it rather than resorting to alternative solutions such as enrolling keys as they can lead to issues. If Secure Boot is not required, it can be disabled to avoid various issues. Its status can be verified by typing msinfo32 in Win+R.

6.16. Fast Startup, Standby and Hibernate
This boils down to personal preference, perceptions and experiences however, some individuals prefer not to utilize features such as Fast Startup, standby and hibernation, as they can lead to unexpected issues (explanation), while preferring to perform clean system boots instead of saving and restoring kernel and software state thus limiting the system power states to S0 (working state) and S5 (soft off). Learn about system power states and their meaning here and here. These options in BIOS are often named Fast Startup, Suspend to RAM, S-States (search for S1, S2, S3, S4, S5), standby or similar options. S-State status can be verified with powercfg /a in CMD.

Windows also has a toggle that disables Fast Startup, hibernation and removes C:\hiberfil.sys:

powercfg /h off
6.17. Spread Spectrum
Disable Spread Spectrum (read more) and ensure BCLK frequency is close to the desired value as possible (e.g. 100MHz not 99.97MHz) in CPU-Z however, this highly dependent on the system and motherboard.

6.18. Legacy USB Support
Disable Legacy USB Support as it may cause the system to enter System Management Mode (SMM) via System Management Interrupts (SMIs) (1, 2) which are high priority unmaskable hardware interrupts which cause the CPU to immediately suspend all other activities, including the operating system (1). You may need to turn this on to install a new operating system, access BIOS or USB devices in some cases.

6.19. Software Installation Options
If there are options relating to software installation (e.g. ASUS Armoury Crate), then disable them. These types of software are typically in-line with other bloatware which can safely be avoided and are present in various BIOSes (ASUS, Gigabyte, MSI, ASRock).

6.20. PCI Link Speed for Devices
Set PCIe link speed to the maximum supported such as Gen 4.0. This may be represented as gigatransfers per second (GT/s) (1). This helps with alleviating unexpected behavior and issues.

6.21. Fan Curves
To maximize cooling potential, configure fan curves (example) or set a static, high, noise-acceptable RPM. Set your AIO pump speed to full if applicable.

6.22. BIOS Profiles and Backups
Backup BIOS by saving the current settings to a profile or export one to local storage as clearing CMOS will wipe all settings if you need to do so (e.g. while overclocking).

In my experience on various motherboards, loading a saved profile fails to restore certain settings after clearing CMOS. I would recommend dumping NVRAM using a tool such as SCEWIN so that when you restore a profile, dump NVRAM again then compare it to the previous/original export to see whether anything failed to restore by using a text comparison tool such as the Notepad++ Compare plugin or Visual Studio Code.

7. Configure USB Port Layout
7.1. Reviewing Accessible USB Ports
Firstly, familiarize yourself with which USB ports correspond to given USB controllers as some ports shown in USB Device Tree Viewer may not be physically accessible. I recommended plugging a device into every accessible port on your system such as the ones on the motherboard I/O and front panels, then take a note of which controller and port each physical port corresponds to in USB Device Tree Viewer.

7.2. Layout Planning
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

Secondly, plan and decide which USB controllers you would like to plug devices into but don't plug them in yet. As for which USB controllers should be used, that is up to you. If you have more than one USB controller, you can isolate devices such as your mouse, keyboard and audio devices onto another USB controller as they have the potential to interfere with polling consistency (1). More USB controllers may be made available by using PCIe expansion cards or external USB 2.0 and 3.0 headers on your motherboard. Always verify with USB Device Tree Viewer. Ryzen systems have a USB controller that is directly connected to the CPU (1) which can be identified under the PCIe Bus category in HWiNFO. It is usually the USB controller that is connected to an Internal PCIe Bridge to bus which is also labelled with the CPU architecture (example).

7.3. Plugging In Devices
Lastly, plug the devices into the ports and USB controllers that you have decided to use. In any case, consider populating ones that are closest to the root of the USB controller's hub tree first. Additionally, I would also recommend avoiding internal hubs (example).

8. Configure Peripherals
8.1. Cleaning
Carefully use an air dust blower to remove dirt and debris from the mouse sensor lens without damage.

8.2. Onboard Memory Profiles
Most modern peripherals support onboard memory profiles such as mice and keyboards. Configure them before configuring the OS as you will not be required to install the bloatware such as Razer Synapse to change the settings later. Details for separating bloat-free and bloated environments using a dual-boot will be discussed in later steps. Alternatively, limit the bloated software to a bootable Windows USB (Windows To Go).

8.3. RGB Lighting Effects
USB 2/3 are limited to 0.5A/0.9A respectively (1) and RGB requires unnecessary power. Turn off lighting effects or strip the LED from the peripheral as running an RGB effect/animation can take a great toll on the MCU and will delay other processes (1, 2, 3).

8.4. DPI
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

Higher sensor DPI reduces latency and helps in saturating polls with motion data (1, 2, 3). Avoid jitter reduction (e.g. DPI downshift) and sensor smoothing kicking in with higher DPI values. If your game uses raw input, you can reduce the pointer speed in Windows to offset the sensitivity from higher DPI. Otherwise, leave the slider at the default position as input will be negatively affected due to scaling. One way to determine whether a given application is using raw input is to spy on the raw input API calls with API Monitor or check whether the enhance pointer precision option has any effect in-game. If you are still unsure or have doubts, leave the slider at the default position.

8.5. Report Rate
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

Higher polling rates reduce jitter and latency (1, 2, 3). Higher polling rates may negatively impact performance depending on your hardware and general configuration so adjust accordingly.

8.6. Polling Stability Analysis
Use Mouse Tester to check whether each poll contains data. As an example, if the interval is spiking to 2ms (500Hz) or higher from 1ms (1kHz), this is not the expected behavior and is problematic. This may be due to several variables such as the device itself (e.g. sensor fault), cable, power issues, hardware, operating system and more. You may need to lower or disable USB interrupt moderation using the XHCI-IMOD-Interval.ps1 script if there are multiple devices generating interrupts on the same USB controller and/or the mouse interrupts are being generated at a rate greater than or equal to the default IMOD interval during the benchmark resulting in IMOD kicking in.

8.7. Monitor
Optionally reset your monitor to factory settings and reconfigure it in case anything was misconfigured initially. Overdrive/AMA reduces latency (1) however, it comes with the penalty of additional overshoot. Additionally, you can attempt to calibrate it. Optionally overclock your display with Custom Resolution Utility and test for frame skipping. Aim for an actual integer refresh rate such as 60.00/240.00, not 59.94/239.76.

See Can You Calibrate a Monitor WITHOUT a Colorimeter? | techless
9. Stability, Hardware Clocking and Thermal Performance
Ensure that all of your hardware is stable before configuring a new operating system as unstable hardware can lead to crashes, data corruption, worse performance or indirectly irreversible damage to hardware. The effectiveness of testing for instability varies between tools which is why it is important to use a range of them for a sufficient amount of time (a non-exhaustive list of recommended tools is listed below).

9.1. Temporary Operating System
I would highly recommend configuring a temporary dual-boot with a fresh installation of Windows or a bootable Windows USB (Windows To Go) to avoid corrupting your main operating system while stress-testing and overclocking. In terms of memory stress-testing, this also allows the stress-test to use more RAM as it isn't being hogged by potential bloatware on your current installation. Safe mode can also serve as a minimal testing environment but certain software may not work.

9.2. General Information
Verify and validate changes within software to avoid unexpected results and behavior (e.g. frequency, voltages, timings)

Save a BIOS profile before each change when overclocking such as changing CPU/RAM frequency and RAM timings so that you don't lose progress if you need to clear CMOS. Refer to section BIOS Profiles and Backups regarding restoring settings properly

When overclocking, you may be required to raise various power limits if the default limits are exceeded

Use HWiNFO to monitor system sensors. A higher polling interval can help to identify sudden spikes but not transients on a microsecond scale as an example. Avoid running while benchmarking as it has the potential to reduce the reliability of results

A single error or crash is one too many. Monitor WHEAs with HWiNFO's error count or configure an Event Viewer filter

Monitor voltages where applicable due to potential overvolting

There are countless factors that contribute to stability such as temperature, power delivery, quality of hardware in general, silicon lottery and more

9.3. Error Correction
Overclocking does not necessarily mean that the system will perform better due to factors such as error correction where applicable. You should verify whether whatever you are changing scales positively by adopting a systematic benchmarking methodology.

9.4. Thermal Management
Avoid thermal throttling at all costs. As a reminder, ambient temperature will generally increase during the summer. Deliberately underclock if your cooler is inadequate. A thermally stable component with an overall lower frequency is preferable compared to thermal throttling at a higher frequency/voltage. To apply additional thermal stress when tuning any component (e.g. CPU, RAM, GPU), consider turning off case, RAM fans or reducing RPM along with generating extra heat (e.g. GPU load, room heaters) while stress-testing.

See RAM Overclock Stability and Heat Management | buildzoid
9.5. Load-line Calibration
This is not a recommendation of what LLC mode to use and is instead, here for informative purposes.

See VRM Load-Line Visualized | ElmorLabs
See Vdroop setting and it’s impact on CPU operation | xDevs
See Why Vdroop is good for overclocking and taking a look at Gigabyte's Override Vcore mode | buildzoid
9.6. GPU
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

When overclocking the GPU, you may be required to flash a BIOS with a higher power limit or raise them.

On NVIDIA systems, ensure to disable CUDA - Force P2 State with NVIDIA Profile Inspector to prevent memory downclocking while stress-testing
See A Slightly Better Way To Overclock and Tweak Your Nvidia GPU | Cancerogeno
See LunarPSD/NvidiaOverclocking
9.7. RAM/CPU
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

Ensure that your CPU is able to boost correctly before starting in case you have disabled options such as SpeedStep and Speed Shift which can prevent the processor from exceeding its base frequency

Configure RAM frequency and timings manually for a significant performance improvement (1). XMP does not tune many timings nor does it guarantee stability

See Eden’s DDR4 guide
See KoTbelowall/INTEL-DDR4-RAM-OC-GUIDE-by-KoT
See integralfx/MemTestHelper
Configure static all-core frequencies and voltages for the CPU. Variations in hardware clocks can introduce jitter due to the process of frequency transitions. Precision Boost Overdrive for Ryzen CPUs is an alternative option to a static frequency and voltages and is often recommended

The previous two bullet points affect each other in terms of stability which means that your RAM overclock may become unstable after tuning the CPU, so run RAM stress-tests again and adjust your CPU settings if required

9.8. Stress-Testing Tools
StresKit (bootable)

Linpack

StresKit's Linpack
Linpack-Extended
Linpack Xtreme Bootable
Use a range of memory sizes
Residuals should match otherwise, it may be a sign of instability
GFLOP variation should be minimal
Prime95

FIRESTARTER

y-cruncher

Memory Testing Software

HCI
MemTest86 (bootable)
MemTest86+ (bootable)
UNIGINE Superposition

OCCT

memtest_vulkan

10. Install Windows
10.1. Storage Partitions
Set up a multi-boot system to maintain separate environments for work/bloatware and gaming, ensuring the latter one remains free of bloatware. This allows you to keep the gaming partition clean and free of unnecessary software, as discussed in earlier sections. By doing so, you avoid installing bloatware on the same partition where you use real-time applications without sacrificing usability. To achieve this, shrink a volume in Disk Management (instructions) to create unallocated space for installing the new operating system.

10.2. What Version of Windows Should You Use?
This section contains important points to consider that have been collected over the years in regard to Windows versions, compatibility and exclusive features.

Earlier versions of Windows lack anticheat support (due to lack of security updates from end-of-life OSes), driver support (commonly GPU, NIC) and application support in general, so some users are forced to use newer builds. See the table below of the minimum version required to install drivers for given GPUs. Subject to change

GPU	Minimum Windows Version
NVIDIA 10 series and lower	Supported by almost all Windows versions
NVIDIA 16, 20 series	Win7, Win8, Win10 1709+
NVIDIA 30 series	Win7, Win10 1803+
NVIDIA 40 series	Win10 1803+
AMD	Refer to driver support page
Windows Server lacks support for a lot of consumer NICs. Workaround tends such as this tend to interfere with anticheats due to invalid signing certificates

NVIDIA DCH drivers are supported on Windows 10 1803+ (1)

During media playback exclusively on Windows 10 1709, the Multimedia Class Scheduler Service raises the timer resolution to 0.5ms which limits control regarding the requested resolution

Windows 10 1809+ is required for Ray Tracing on NVIDIA GPUs

Microsoft implemented a fixed 10MHz QueryPerformanceFrequency on Windows 10 1809+

Windows 10 1903+ has an updated scheduler for multi CCX Ryzen CPUs (1)

DirectStorage requires Windows 10 1909+ but according to an article, games running on Windows 11 benefit further from new storage stack optimizations (1)

Windows 10 2004+ is required for Hardware Accelerated GPU Scheduling which is necessary for DLSS Frame Generation (1)

Processes raising the timer resolution on Windows 10 2004+ no longer affect the global timer resolution (1, 2) meaning that it is set on a per-process basis in which, processes that do not explicitly raise the resolution are not guaranteed a higher resolution and are serviced less often. This was further developed on Windows 11 as a higher resolution is not guaranteed to the calling process if its window is minimized or visibly occluded (1). Microsoft added the ability to restore the global behavior on Windows Server 2022+ and Windows 11+ with a registry entry (1) meaning that the implementation can not be restored on Windows 10 versions 2004 - 22H2

Windows 11+ has an updated scheduler for Intel 12th Gen CPUs and above (1) but the behavior can be replicated manually with affinity policies on any Windows version as explained in later sections

Windows 11+ limits the window message rate of background processes (1)

Windows 11 is a minimum requirement for Cross Adapter Scan-Out (1)

AllowTelemetry can be set to 0 on Windows Server editions (1)

10.3. Downloading and Preparing a Stock Windows ISO
In order to install Windows, an installation media must be created using an ISO file. Upon downloading ISOs, ensure to cross-check the hashes for the file with official sources to verify that it is genuine and not corrupted. Use the command certutil -hashfile <file> in CMD to obtain the hashes of the file.

Ensure to download an ISO that contains an edition with group policy support as several policies are configured in later steps. Sometimes, you can get ISOs with specific editions missing so be careful. Below is a list of recommended editions.

Client editions: Professional
Server editions: Standard (Desktop Experience)
10.4. ISO Sources
os.click
New Download Links
Adguard File List
Microsoft Software Download Listing
Fido
UUP dump
10.5. ISO Preparation
Windows 7
Windows 8.1
Windows 10+
Important

The presence of OEMs keys can force the installation of specific editions of Windows editions (e.g. Home) which is explained in section Downloading and Preparing a Stock Windows ISO. To circumvent this, you can either customize EI.cfg and PID.txt (instructions) or remove every edition apart from the edition you would like to install using NTLite or DISM in CLI (instructions), however NTLite is more user-friendly.

10.6. Fetching Required Files
There are primarily two prerequisites before installing Windows. These can be done later if you are willing to fetch them from another system but I would recommend getting them now. Store these somewhere that you can access offline after installing Windows such as a USB storage device as the installation process consists of not being connected to a network in the initial steps.

Download your NIC driver as it may not be packaged with Windows and must be installed in order to connect to a network
The bin folder from this repository which can be downloaded here
10.7. Booting Into the ISO
This section covers booting into the ISO retrieved and prepared in the previous section. For the next steps, you are required to disconnect the Ethernet cable and not be connected to the internet during the installation process. This will allow us to bypass the forced Microsoft login during OOBE, allowing us to use Windows with a local account along with preventing installation of unwanted updates and drivers. There are two options when it comes to installing Windows, installing using USB storage or using DISM (without USB storage). Either option can be used. The latter option requires dual-booting.

Option 1 - Install using USB storage
Option 2 - Install using DISM Apply-Image (without USB storage)
11. Configure Windows
11.1 OOBE Setup
Windows Server may force you to enter a password which can be optionally be removed in later steps

If you are configuring Windows 11, press Shift+F10 to open CMD and execute oobe\BypassNRO.cmd. This will allow us to continue without an internet connection by unlocking the continue with limited setup option as demonstrated in the video examples below. With that said, this also removes the requirement to sign in with a Microsoft account which I highly advise against for privacy reasons generally speaking

See assets/videos/oobe-windows7-example.mp4

See assets/videos/oobe-windows8-example.mp4

See assets/videos/oobe-windows10+-example.mp4

11.2. Unrestricted PowerShell Execution Policy
Warning

🔒 Setting the PowerShell Execution Policy to Unrestricted may negatively impact security and expose the system to vulnerabilities. Users should evaluate the security risks associated with modifying the specified setting. Alternatively, -ExecutionPolicy Bypass can be used when starting a PowerShell instance instead of configuring it globally.

This is required to execute the scripts within the repository. Open PowerShell as administrator and enter the command below.

Set-ExecutionPolicy Unrestricted
11.3. Importing bin Folder
Move the bin folder that you downloaded prior to installing Windows to the C: drive as outlined in section Fetching Required Files. If you haven't downloaded it yet, you will need to fetch it from another system as you don't have network access at this stage. The complete path should be C:\bin.

11.4. Process Mitigations (Windows 10 1709+)
Warning

🔒 Disabling process mitigations may negatively impact security and expose the system to vulnerabilities. Users should evaluate the security risks associated with modifying the specified setting.

Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

There are several OS-level mitigations (1) that are enabled by default and may impact performance. If desired, these can be disabled in Windows Defender's "Exploit Protection" page. It should be apparent that disabling mitigations reduces security. This step is carried out now as if you choose to disable Windows Defender in the next steps, the interface will no longer be accessible however they can be toggled using the Get-ProcessMitigation and Set-ProcessMitigation commands in PowerShell. Some programs may require mitigations to be enabled and will break if they are disabled so proceed with caution.

11.5. Merging Registry Options
Warning

🔒 Some changes outlined in the table below may negatively impact security and expose the system to vulnerabilities. Users should evaluate the security risks associated with modifying the specified setting.

The registry settings are merged with the apply-registry.ps1 script. As for which options get applied, there are outlined in the table below which this can be customized by editing C:\bin\registry-options.json in a text editor and setting properties to either true or false. You can backup the config file so that you don't need to modify it each time you reinstall Windows.

11.5.1. Registry Options Documentation
Important

As of now, the script does not revert options if re-run. For example, if the script was run with an option set to true, then running the script with a given option set to false will not revert the changed made as the script is unaware of the previous state of the registry keys associated with the option. This functionality may be implemented in the future but for now, use the -get_option_keys <option> argument with the script to get all relevant keys for a given option so that you can revert them manually.

Option	Incentive	Notes	Default Value
disable windows update	1. Reducing CPU overhead

2. Gaining finer control over the feature in question	🔒 A value of true may negatively impact security and expose the system to vulnerabilities. Users should evaluate the security risks associated with modifying the specified setting

Disabling Windows Update is in Microsoft's recommendations for configuring devices for real-time performance (1). Alternatively automatic updates can be disabled instead of disabling Windows Update completely which achieves the same effect in terms of reducing CPU overhead but still being able to update Windows by configuring disable windows update to false and disable automatic windows updates to true. The Windows Update processes are known to use a lot of CPU and memory resources. Disabling Windows Update breaks the Microsoft Store however you can download and install Appx packages directly (instructions)	false
disable automatic windows updates	1. Reducing CPU overhead

2. Gaining finer control over the feature in question	🔒 A value of true may negatively impact security and expose the system to vulnerabilities. Users should evaluate the security risks associated with modifying the specified setting

Prevents automatic download and installation of Windows updates rather than disabling Windows Update completely and instead, check for updates manually from time to time. Updates can occur at inconvenient times which leads to excessive CPU and memory usage at random intervals along with disrupting shutdowns in certain cases. This option is overridden if disable windows update is set to true.

This option does not affect upgrades which can be controlled using group policies (instructions). However, you are limited to preventing upgrades until the specified version reaches end-of-life	true
disable driver installation via windows update	1. Reducing CPU overhead

2. Gaining finer control over the feature in question	Prevents outdated, vulnerable and potentially poorly performing drivers from being installed via Windows Update. It is recommended to manually install only the bare minimum version of the ones that your system requires (as the full installer often installs other bloatware that persistently runs in the background) along with the latest version directly from the manufacture's website as outlined in section Installing Drivers. This option is overridden if disable windows update is set to true	true
disable automatic store app updates	1. Reducing CPU overhead

2. Gaining finer control over the feature in question	🔒 A value of true may negatively impact security and expose the system to vulnerabilities. Users should evaluate the security risks associated with modifying the specified setting

Prevents automatic download and installation of store application updates compared to disabling app updates completely which is not desirable in terms of reducing CPU overhead. Instead, check for application updates manually from time to time	true
disable windows defender	1. Reducing CPU overhead

2. Prevents issues with the CPU entering C-State 0 (1)	🔒 A value of true may negatively impact security. Users should assess the security risk involved with modifying the mentioned setting

This option completely disables Windows Defender. Instead, run system scans frequently, use a hardened browser with uBlock Origin, keep UAC enabled and favor free, open source and reputable software. Stay away from proprietary software where you can and ensure to scan files and executables with VirusTotal before opening them	true
disable gamebarpresencewriter	1. Reducing CPU overhead	Process runs constantly in the background and is not required for Game Mode or Game Bar to function from my testing	true
disable background apps	1. Reducing CPU overhead	Prevents apps from running in the background. Background applications are disabled via policies with this option as the option is not available in the interface on Windows 11	true
disable transparency effects	1. Reducing CPU overhead (1)	Disables transparency effects	true
disable notifications network usage	1. Mitigating telemetry and phoning home (1)	N/A	true
disable windows marking file attachments with information about their zone of origin	1. Reducing or disabling intrusive features	🔒 A value of true may negatively impact security. Users should assess the security risk involved with modifying the mentioned setting

Prevents this intrusive security warning as downloaded files are constantly required to be unblocked however this may negatively impact security as the user will not be notified of blocked files via a security warning prompt (1)	true
disable malicious software removal tool updates	1. Gaining finer control over the feature in question	🔒 A value of true may negatively impact security. Users should assess the security risk involved with modifying the mentioned setting

Prevent Windows offering Malicious Software Removal Tool through Windows Update	true
disable sticky keys	1. Reducing or disabling intrusive features	Disables the Do you want to turn on Sticky Keys? promt when the hotkey is pressed a certain number of times. This is severely intrusive in applications that utilize the Shift key for controls such as games	true
disable pointer acceleration	1. Reducing or disabling intrusive features	Ensures one-to-one mouse response for games that do not subscribe to raw input events and on Desktop	true
disable fast startup	1. Reducing or disabling intrusive features	Interferes with shutting down in the sense that the system does not enter S5 which can lead to unexpected issues (explanation). See section Fast Startup, Standby and Hibernate for related information. It is possible to shut down properly without disabling Fast Startup by holding Shift while clicking Shut down in the start menu. However, the downside to this is that you may forget to hold the Shift key	true
disable customer experience improvement program	1. Mitigating telemetry and phoning home (1)	Recommended by privacyguides.org	true
disable windows error reporting	1. Mitigating telemetry and phoning home	Recommended by privacyguides.org	true
disable clipboard history	1. Mitigating telemetry and phoning home	Recommended by privacyguides.org	true
disable activity feed	1. Mitigating telemetry and phoning home	Recommended by privacyguides.org	true
disable advertising id	1. Mitigating telemetry and phoning home	Recommended by privacyguides.org	true
disable autoplay	1. Mitigate security risk	Recommended by privacyguides.org	true
disable cloud content	1. Mitigating telemetry and phoning home	Recommended by privacyguides.org	true
disable account-based explorer features	1. Mitigating telemetry and phoning home	Recommended by privacyguides.org	true
disable mdm enrollment	1. Mitigating telemetry and phoning home	Recommended by privacyguides.org	true
disable microsoft store push to install feature	1. Mitigate security risk	Recommended by privacyguides.org	true
mitigate web-based search info	1. Mitigating telemetry and phoning home	Recommended by privacyguides.org	true
disable sending inking and typing data to microsoft	1. Mitigating telemetry and phoning home	Recommended by privacyguides.org	true
disable automatic maintenance	1. Gaining finer control over the feature in question	N/A	true
disable program compatibility assistant	1. Gaining finer control over the feature in question	Prevents Windows applying changes anonymously after running troubleshooters	true
disable remote assistance	1. Mitigate security risk	N/A	true
disable sign-in and lock last interactive user after a restart	1. Mitigate security risk (1)	N/A	true
show file extensions	1. Mitigate security risk (1)	N/A	true
disable widgets	1. Mitigate security risk (1)	N/A	true
disable telemetry	1. Mitigating telemetry and phoning home	N/A	true
disable retrieval of online tips and help in the immersive control panel	1. Mitigating telemetry and phoning home	N/A	true
disable typing insights	1. Mitigating telemetry and phoning home	N/A	true
disable suggestions in the search box and in search home	1. Mitigating telemetry and phoning home

2. Reducing or disabling intrusive features	N/A	true
disable computer is out of support message	1. Reducing or disabling intrusive features	Disables this intrusive message. Not relevant to users with a modern Windows version	true
disable fault tolerant heap	1. Gaining finer control over the feature in question	Prevents Windows autonomously applying mitigations to prevent future crashes on a per-application basis (1) which can lead to issues (1)	true
11.5.2. Applying Options
Open PowerShell as administrator and enter the command below. If the command fails, then try to disable tamper protection (Windows 10 1909+) and real-time protection in Windows Defender . If that doesn't work, reboot then re-execute the command again. If none of the previous workarounds worked, then try run the command in safe-mode. If you prefer not to run any scripts, the option of manually creating the registry file with the keys you need are explained in /docs/registry-opts.md. This document contains all of the keys that would be merged when using the script

C:\bin\apply-registry.ps1
Ensure that the script prints a "successfully applied" message to the console, if it does not then the registry keys were not successfully merged

After and only after a restart, you can establish an internet connection as the Windows update policies will take effect, which is the primary reason for not being connected to the internet up until this point

Note

To the maintainers and contributors, the features and options should be tested as listed in the table above. It is inevitable that more steps are required to achieve the same goal with operating system updates and upgrades over time (e.g. manual maintenance of a list of services relating to disabling Windows Defender).

11.6. Installing Drivers
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

I would advise against installing drivers via Windows Update as they can be outdated compared to the ones provided by the vendor. Driver updates via Windows Update should be blocked if disable driver installation via windows update was disabled in section Merging Registry Options

See Chipset Device "Drivers" (= INF files) | Fernando

GPU drivers will be installed in section Graphics Driver so do not install them at this stage

You can find drivers by searching for drivers that are compatible with your device's HWID. See media/device-hwid-example.png in regard to finding your HWID in Device Manager for a given device

Try to obtain the driver in its INF form so that it can be installed in Device Manager as executable installers usually install other bloatware along with the driver itself. Sometimes you can extract the installer's executable with 7-Zip

It is recommended to update and install the following:

Network Interface Controller. If you do not have internet access at this stage, you will need to download your NIC driver from another device or dual-boot as they may not be packaged at all with Windows

USB and NVMe (if you are configuring Windows 7, both may have already been integrated in section Downloading and Preparing a Stock Windows ISO)

SATA (required on Windows 7 as the stock driver does not support Message Signaled Interrupts)

Other required drivers can be installed with Snappy Driver Installer Origin

11.7. Windows Server Specific Options (Windows Server)
To enable Wi-Fi, navigate to Manage -> Add Roles and Features in the Server Manager dashboard and enable Wireless LAN Service

In Server Manager, navigate to Manage -> Server Manager Properties and enable the option to prevent Server Manager from starting automatically

Set the Windows Audio and Windows Audio Endpoint Builder services startup type to automatic by typing services.msc in Win+R

Navigate to Computer Configuration -> Windows Settings -> Security Settings -> Account Policies -> Password Policy by typing gpedit.msc in Win+R and disable Password must meet complexity requirements

Open CMD and type gpupdate /force to apply the changes immediately
Navigate to Computer Configuration -> Administrative Templates -> System by typing gpedit.msc in Win+R and disable Display Shutdown Event Tracker to disable the shutdown prompt

To remove the user password, enter your current password and leave the new/confirm password fields blank in User Accounts by typing control userpasswords in Win+R

11.8. Privacy Options (Windows 8+)
Disable all unnecessary permissions in the Privacy section by pressing Win+I.

11.9. Search Indexing
Certain directories on the file system are indexed for search features in Windows which can be viewed by typing control srchadmin.dll in Win+R. Indexing occurs periodically in the background and often results in notable CPU overhead which can be seen using Process Explorer as described in section Process Explorer. Therefore, it is preferable to prevent search indexing globally by disabling the Windows Search service however, search features may be limited. Open CMD as administrator and enter the command below.

reg add "HKLM\SYSTEM\CurrentControlSet\Services\WSearch" /v "Start" /t REG_DWORD /d "4" /f
Important

To prevent unexpected breakage and problems due to service dependency errors, assess the other services that depend on the service you want to disable. This can be done by opening CMD as administrator then typing sc EnumDepend <service> which describes the services that rely on the service you want to disable. These services should be disabled to avoid dependency errors. If you can't disable them (e.g. because you need them), then you have no choice but to leave the service you wanted to disable initially enabled.

11.10. Time, Language and Region
Configure settings by typing intl.cpl and timedate.cpl in Win+R

Windows 10+ Only

Configure settings in Time & Language by pressing Win+I

If you intend to exclusively use one language and keyboard layout, ensure that is the case in actuality so that you don't need to toggle the language bar hotkeys which can become intrusive as the hotkey can be accidentally pressed
Ensure that the system time is synced and is correct

11.11. Web Browser
Configure a browser of your choice.

See privacytests.org

See Desktop Browsers | Privacy Guides

11.12. Scheduled Tasks
There are a handful of scheduled tasks that ship with Windows which can be assessed using TaskSchedulerView. Assessing them can help in having finer control as to what runs on your system silently whether it be updates-related, telemetry-related, defender-related and more. Consider the Last Run, Next Run and Triggers column to evaluate whether there is any point disabling the task in question.

11.13. Activate Windows
Use the commands below to activate Windows using your license key if you do not have one linked to your HWID. Ensure that the activation process was successful by verifying the activation status in computer properties. Open CMD as administrator and enter the commands below.

slmgr /ipk <license key>
slmgr /ato
11.14. Declutter Interface
Disable features on the taskbar and unpin shortcuts and tiles from the taskbar and start menu. This is obviously personal preference.

11.15. Visual Effects
Visual effects options can be accessed by typing sysdm.cpl in Win+R. This menu provides the ability to disable interface animations which contributes to perceived responsiveness when generally interacting with Windows. On Windows 7, desktop composition could natively be disabled here, but the option is no longer available in Windows 8+. The rest of the options are personal preference.

11.16. Superfetch and Prefetch
If a HDD isn't present in the system then Superfetch and Prefetch can be disabled with the command below in CMD. Disabling SysMain is in Microsoft's recommendations for configuring devices for real-time performance (1) and the C:\Windows\Prefetch folder should no longer be populated.

reg add "HKLM\SYSTEM\CurrentControlSet\Services\SysMain" /v "Start" /t REG_DWORD /d "4" /f
Important

To prevent unexpected breakage and problems due to service dependency errors, assess the other services that depend on the service you want to disable. This can be done by opening CMD as administrator then typing sc EnumDepend <service> which describes the services that rely on the service you want to disable. These services should be disabled to avoid dependency errors. If you can't disable them (e.g. because you need them), then you have no choice but to leave the service you wanted to disable initially enabled.

11.17. Operating System and Partition Name
Configure the operating system and drive's partition name. It is recommended to set it to something meaningful or unique such has W10 22H2 Work or W10 22H2 Gaming for clarity when dual-booting or when multiple drives are present. Open CMD as administrator and enter the commands below.

bcdedit /set {current} description "OS_NAME"
label C: "OS_NAME"
11.18. Show Tray Icons
I would recommend enabling the Always show all icons in the notification area for better process management. Hiding icons in the tray area can partially be considered a security risk since you won't be aware of potentially malicious or unwanted programs running silently.

11.19. Hibernation
Windows has a toggle that disables Fast Startup, hibernation and removes C:\hiberfil.sys. It is recommended to shut down instead of saving software state to disk. Open CMD as administrator and enter the command below.

powercfg /h off
11.20. Runtimes
These are runtimes are common dependencies including a magnitude of applications. Typically, application installers automatically install its dependencies but this can't be said for some standalone applications.

Visual C++ Redistributable
.NET 3.5 (less common dependency, instructions include both offline and online installation methods)
.NET 4.8 (ships with Windows 10 1909+)
WebView
DirectX (game launchers typically install this silently)
11.21. Handling Bloatware
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

I heavily discourage running debloating scripts or removing components other than actual bloatware such as Candy Crush or whatever may be packaged with Windows these days to avoid breaking your operating system. It can be argued that removing these applications have no performance benefit if they don't actively run in the background which can be assessed in Task Manager. To adopt the approach of only removing or disabling what actively runs in the background, setup Process Explorer as described in Process Explorer and sort processes by either Context Switch Delta or Cycles Delta to assess what can be removed. The update speed can be changed in View -> Update Speed depending on your tolerance.

AppxPackagesManager can be used to uninstall Appx packages which ship with Windows. I recommend keeping Microsoft.WindowsStore (Microsoft Store) at the very least so that you can download applications in the future. Appx packages can also be installed without the Microsoft Store (instructions). If for whatever reason you removed the Microsoft Store, it can be restored with wsreset -i

I highly recommend removing OneDrive for privacy reasons and if you must, use OneDrive within a browser. Removing OneDrive involves opening CMD as administrator and entering the command below

for %a in ("SysWOW64" "System32") do (if exist "%windir%\%~a\OneDriveSetup.exe" ("%windir%\%~a\OneDriveSetup.exe" /uninstall)) && reg delete "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Desktop\NameSpace\{018D5C66-4533-4307-9B53-224DE2ED1FE6}" /f
Disabling (not uninstalling) Chromium Microsoft Edge involves the steps below. The browser should be disabled instead of uninstalled to retain the WebView runtime

In the Microsoft Edge settings, disable any startup options such as the ones listed below. Doing this prevents an autorun entry being created any time msedge.exe is started despite removing it in the next step with Autoruns

Startup boost
Continue running background extensions and apps when Microsoft Edge is closed
Download Autoruns and navigate to the Everything section then search for "edge". Disable every item that appears in the filtered results

Updating the browser will revert some changes made in the previous step. You can ensure that it does not update if it is opened accidentally with the command below. If any errors occur, ensure that there aren't any hidden Microsoft Edge process running in Task Manager

rd /s /q "C:\Program Files (x86)\Microsoft\EdgeUpdate"
Open CMD and enter the command below to remove all related shortcuts

for /f "delims=" %a in ('where /r C:\ *edge.lnk*') do (del /f /q "%a")
Windows 10+ Only:

In the start menu, uninstall any residual links for applications. Keep in mind that these applications aren't actually installed, they get installed only if the user clicks on them so do not accidentally click on them

Uninstall bloatware in the applications section in the immersive control panel by pressing Win+I (this can also be managed in AppxPackagesManager)

In the Optional features section within the immersive control panel, you can uninstall everything that you don't need if desired

If Windows Defender was disabled in section Merging Registry Options, smartscreen.exe ignores the registry key that controls whether it runs in the background persistently on later versions of Windows. For this reason, open CMD as TrustedInstaller with C:\bin\MinSudo.exe --TrustedInstaller --Privileged and enter the command below to prevent it running in the background

taskkill /f /im smartscreen.exe > nul 2>&1 & ren C:\Windows\System32\smartscreen.exe smartscreen.exee
You can use Task Manager to check for residual bloatware that is running in the background

11.22. Optional Features
Optional features can be accessed by typing OptionalFeatures in Win+R. Enable/disable features that you do/don't need. If Windows Update is disabled then you likely won't be able to install features and instead, must install an offline package using DISM. On Windows Server, this can be accessed via the Server Manager dashboard by navigating to Manage -> Remove Roles and Features.

11.22.1. NET 3.5
Some applications still utilize the NET 3.5 runtime so I would recommend installing it just in case. As mentioned previously, you won't be able to install it in the Optional Features window if Windows Update is disabled but can instead, be installed using an offline package.

For using the offline package, download and extract a Windows ISO (e.g. C:\EXTRACTED_ISO) and open CMD as administrator. Replace C:\EXTRACTED_ISO\sources\sxs with the correct path to the \sources\sxs folder in the ISO that you extracted and run the command.

DISM /Online /Enable-Feature /FeatureName:NetFx3 /LimitAccess /Source:"C:\EXTRACTED_ISO\sources\sxs"
11.23. 7-Zip
Download and install 7-Zip. Open C:\Program Files\7-Zip\7zFM.exe then navigate Tools -> Options and associate 7-Zip with all file extensions by clicking the + button. You may need to click it twice to override existing associated extensions.

11.24. Graphics Driver
See docs/configure-nvidia.md
See docs/configure-amd.md
11.25. MSI Afterburner
If you use MSI Afterburner, download and install it now.

I recommend configuring a static fan speed as using the fan curve feature requires the program to run continually however, it is up to you whether to use the curve or not

To automatically load profile 1 (as an example) when Windows boots, the command below can be used with Task Scheduler (instructions). Ensure to wrap any paths with quotes if there are spaces in them. Ensure to verify whether everything is working correctly after a system restart. You need to enable the Run with highest privileges option if administrator privileges are required

"C:\Program Files (x86)\MSI Afterburner\MSIAfterburner.exe" /Profile1 /Q
11.26. Display Resolutions and Scaling Modes
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

You may have optionally found a stable overclock for your display in earlier sections using Custom Resolution Utility which you can dial in now.

Typically, you have the option of performing scaling on the GPU or display. Native resolution does not require scaling thus results in identity (no) scaling. Furthermore, identity scaling renders most of the scaling options in the GPU control panel obsolete. If you are using a non-native resolution, there is an argument for favoring display scaling due to less GPU processing

Aim for an actual integer refresh rate such as 60.00/240.00, not 59.94/239.76

There are many ways to achieve the same outcome regarding GPU and display scaling. See the table in the link below for example scenarios

See What Is Identity Scaling and How Can You Use It?

Optionally use QueryDisplayScaling to query the current scaling mode

On systems with an NVIDIA GPU, ensure that the Display option for the Perform scaling on setting is still available. If it is not, then find out what change you made in CRU results in it not being accessible through trial and error. This can be accomplished by running reset.exe to reset the settings to default then re-configure CRU. After each change, run restart64.exe then check whether the option is still available

Ensure your resolution is configured properly by typing rundll32.exe display.dll,ShowAdapterSettings in Win+R

11.27. Open-Shell (Windows 8+)
Open-Shell is a FOSS alternative to the Windows Start Menu.

Download and install Open-Shell. Only install the Open-Shell Menu

Settings:

General Behavior

Check for Windows updates on shutdown - Disable
Windows 8 Only:

Open "C:\Program Files\Open-Shell\Start Menu Settings.lnk", enable Show all settings then navigate to the Windows 8 Settings section and set Disable active corners to All
11.28. Spectre, Meltdown and CPU Microcode
Warning

🔒 Disabling Spectre and Meltdown may negatively impact security and expose the system to vulnerabilities. Users should evaluate the security risks associated with modifying the specified setting.

Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

Disabling Spectre and Meltdown is an age-old performance trick familiar amongst many individuals however with newer platforms and system architecture, there may be a performance regression (1). For this reason, extensive tests should be carried out to determine how performance is impacted and whether performance scales positively, negatively or not at all. Its state can be manipulated with the InSpectre tool and/or by renaming the microcode DLLs within the OS depending on whether there is a microcode revision mismatch between the OS and BIOS (1, 2). It is important to note that the microcode revisions are subject to change with Windows updates.

Instructions To Rename DLLs
Meltdown does not affect the AMD architecture (1, 2, 3) and is required for a minority of anticheats (FACEIT).

Use InSpectre and CPU-Z's validation feature to check the status or version before and after a reboot to verify expected behavior.

11.29. Power Options
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

To be completed.

11.30. Process Explorer
Task Manager lacks several useful metrics compared to a tool such as Process Explorer. On Windows 8+, Task Manager reports CPU utility in % which provides misleading CPU utilization details (1). On the other hand, Windows 7's Task Manager and Process Explorer report time-based busy utilization. This also explains as to why disabling idle states within the OS results in 100% CPU utilization in Task Manager.

Download and extract Process Explorer

Copy procexp64.exe into a safe directory such as C:\Windows and open it

Navigate to Options and select Replace Task Manager. Optionally configure the following:

Confirm Kill

Allow Only One Instance

Always On Top (helpful for when applications crash and UI becomes unresponsive)

Enable the following columns for granular resource measurement metrics

Context Switch Delta (Process Performance)

CPU Cycles Delta (Process Performance)

Delta Reads (Process I/O)

Delta Writes (Process I/O)

Delta Other (Process I/O)

Enable the VirusTotal column

11.31. Memory Management Settings (Windows 8+)
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

Open PowerShell and enter the command below to review memory management options

Get-MMAgent
Optionally use the command below as an example to disable a given setting. If you left Superfetch and Prefetch enabled in section Superfetch and Prefetch, then you likely want the prefetching related features enabled

Disable-MMAgent -MemoryCompression
11.32. Network Adapter Options
Open Network Connections by typing ncpa.cpl in Win+R

Disable any unused network adapters then right-click your main one then select Properties

Disable NetBIOS over TCP/IP for all network adapters in Internet Protocol Version 4 (TCP/IPv4) -> Properties -> General -> Advanced -> WINS to prevent unnecessary system listening, typically on ports 137-139 which can be verified in a network monitoring tool such as TCPView or Wirehshark. For future reference, this option has to be changed for newly installed network adapters

Optionally configure DNS settings

See DNS Resolvers - Recommended Providers | Privacy Guides
11.33. Audio Devices
The sound control panel can be opened by typing mmsys.cpl in Win+R

Disable unused Playback and Recording devices

I would recommend avoid using audio enhancements as they appear to marginally waste resources (1)

Optionally set the option in the communications tab to Do nothing to prevent automatic adjustment of audio levels between audio sources as this is an annoyance for the majority of users (1, 2)

Minimize the size of the audio buffer with LowAudioLatency or on your DAC (1). Beware of audio dropouts due to the CPU not being able to keep up under load

11.34. Device Manager
Open Device Manager by typing devmgmt.msc in Win+R

Navigate to View -> Devices by type

In the Disk drives category, you can disable write-cache buffer flushing on all drives in the Properties -> Policies section if your system has a backup power supply or is not prone to power failures to prevent data loss
In the Network adapters category, navigate to Properties -> Advanced and disable any power-saving features
Navigate to View -> Devices by connection

Disable any PCIe, SATA, NVMe and XHCI controllers and USB hubs with nothing connected to them
Disable every device that isn't the GPU on the same PCIe port as the GPU as long as you don't need them
Navigate to View -> Resources by connection

Disable any unneeded devices that are using an IRQ or I/O resources, always ask if unsure and take your time on this step
If there are multiple entries of the same devices and you are unsure which one is in use, refer back to the tree structure in View -> Devices by connection. This is because a single device can use many resources (e.g. IRQs). You can also use MSI Utility to check for duplicate and unneeded devices in case you accidentally miss any with the cluttered Device Manager tree structure
Optionally use DeviceCleanup to remove hidden devices

11.35. Device Power-Saving
Open PowerShell and enter the command below to disable the Allow the computer to turn off this device to save power option for all applicable devices in Device Manager.

Re-plugging devices may cause this option to re-enable so either avoid doing so, run this command again each time or place it in a script and run it at system startup as a precautionary measure with Task Scheduler (instructions). Ensure to wrap any paths with quotes if there are spaces in them. Ensure to verify whether everything is working correctly after a system restart. You need to enable the Run with highest privileges option if administrator privileges are required. For PowerShell scripts, set the program to start to PowerShell and the arguments to the path of the script (e.g. C:\device-power-saving.ps1).

Get-WmiObject MSPower_DeviceEnable -Namespace root\wmi | ForEach-Object { $_.enable = $false; $_.psbase.put(); }
11.36. Event Trace Sessions (ETS)
This section outlines instructions to mass-toggle Event Trace Sessions which can be viewed by typing perfmon in Win+R then navigating to Data Collector Sets -> Event Trace Sessions. Programs that rely on event tracers will not be able to log data until the required sessions are restored (e.g. Windows Event Logging) which is the purpose of creating two registry files to toggle between them. Open CMD as administrator and enter the commands below to build the registry files in the C:\ directory. These registry files must be run with Trusted Installer (use NSudo) to prevent permission errors.

ets-enable.reg

reg export "HKLM\SYSTEM\CurrentControlSet\Control\WMI\Autologger" "C:\ets-enable.reg"
ets-disable.reg

>> "C:\ets-disable.reg" echo Windows Registry Editor Version 5.00 && >> "C:\ets-disable.reg" echo. && >> "C:\ets-disable.reg" echo [-HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\WMI\Autologger]
Additionally disable SleepStudy (UserNotPresentSession)

for %a in ("SleepStudy" "Kernel-Processor-Power" "UserModePowerService") do (wevtutil sl Microsoft-Windows-%~a/Diagnostic /e:false)
11.37. File System
Open CMD as administrator and enter the commands below.

Disable the creation of 8.3 character-length file names on FAT and NTFS-formatted volumes

See Should You Disable 8dot3 for Performance and Security? | TCAT Shelbyville

See Windows Short (8.3) Filenames – A Security Nightmare? | Bogdan Calin

fsutil behavior set disable8dot3 1
Disable updates to the Last Access Time stamp on each directory when directories are listed on an NTFS volume. Disabling the Last Access Time feature improves the speed of file and directory access (1). Beware that this may affect backup and remote storage programs as per the official remarks (1)

fsutil behavior set disablelastaccess 1
11.38. Message Signaled Interrupts
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

Message signaled interrupts (MSIs) are faster than traditional line-based interrupts and may also resolve the issue of shared interrupts which are often the cause of high interrupt latency and stability (1).

Download and open MSI Utility or GoInterruptPolicy

MSIs can be enabled on devices that support it. It is worth noting that it may be in the developer's intention to not enable MSIs in the driver INF file hence MSIs will be disabled by default once the driver is installed. Namely, NVIDIA seems to selectively enable MSIs depending on the GPU architecture (1). Exercise with due care and carry out tests to determine whether changes result in positive performance scaling

You will BSOD if you enable MSIs for the stock Windows 7 SATA driver which you should have already updated as mentioned in section Installing Drivers
To verify whether a device is utilizing MSIs, restart your PC and check whether the given device has a negative IRQ in MSI Utility

Although this step may have been caried out in an earlier section to rule out the hardware-related causes of IRQ sharing, the software-related causes of potential IRQ sharing can be assessed now by confirming that there is no IRQ sharing on your system by typing msinfo32 in Win+R then navigating to the Conflicts/Sharing section

If the System timer device and High precision event timer are sharing IRQ 0, a solution to this is to disable the parent device's driver of System timer which is PCI standard ISA bridge. This can be accomplished with the command below. It is important to note that disabling msisadrv breaks the keyboard on mobile devices

reg add "HKLM\SYSTEM\CurrentControlSet\Services\msisadrv" /v "Start" /t REG_DWORD /d "4" /f
Important

To prevent unexpected breakage and problems due to service dependency errors, assess the other services that depend on the service you want to disable. This can be done by opening CMD as administrator then typing sc EnumDepend <service> which describes the services that rely on the service you want to disable. These services should be disabled to avoid dependency errors. If you can't disable them (e.g. because you need them), then you have no choice but to leave the service you wanted to disable initially enabled.

11.39. XHCI Interrupt Moderation (IMOD)
On most systems, Windows 7 uses an IMOD interval of 1ms whereas recent versions of Windows use 0.05ms (50us) unless specified by the installed USB driver. This means that after an interrupt has been generated, the XHCI controller waits (buffer period) for the specified interval for more data to arrive before generating another interrupt which reduces CPU utilization but potentially results in data from a given device being supplied at an inconsistent rate in the event of expecting data from other devices within the buffer period that are connected to the same XHCI controller.

For example, a mouse with a 1kHz polling rate will report data every 1ms. While only moving the mouse with an IMOD interval of 1ms, interrupt moderation will not be taking place because interrupts are being generated at a rate less than or equal to the specified interval. Realistically while playing a fast-paced game, you will easily surpass 1000 interrupts/s with keyboard and audio interaction while moving the mouse hence there will be a loss of information because you will be expecting data within the waiting period from either devices. Although this is unlikely with an IMOD interval of 0.05ms (50us), it can still happen.

As an example, 1ms IMOD interval with an 8kHz mouse is already problematic because you are expecting data every 0.125ms which is significantly greater than the specified interval which results in a major bottleneck (1).

See How to persistently disable XHCI Interrupt Moderation | BoringBoredom

Microsoft Vulnerable Driver Blocklist may need to be disabled with the command below in order to load the RWEverything driver however a handful of in-game anticheats do not adhere to disabling the blocklist (e.g. CS2, THE FINALS)

reg add "HKLM\SYSTEM\CurrentControlSet\Control\CI\Config" /v "VulnerableDriverBlocklistEnable" /t REG_DWORD /d "0" /f
In some cases, the interrupter index can change after a reboot meaning the address will become invalid if it is hard-coded. To work around this, you can simply disable IMOD for all interrupters by placing the XHCI-IMOD-Interval.ps1 script somewhere safe and launching it at startup with Task Scheduler (instructions). Ensure to wrap any paths with quotes if there are spaces in them. Ensure to verify whether everything is working correctly after a system restart. You need to enable the Run with highest privileges option if administrator privileges are required. For PowerShell scripts, set the program to start to PowerShell and the arguments to the path of the script (e.g. C:\XHCI-IMOD-Interval.ps1)

PowerShell C:\XHCI-IMOD-Interval.ps1
To determine whether changing the IMOD interval is taking effect, you can temporarily set the interval to 0xFA00 (62.5Hz). If the mouse cursor is visibly stuttering upon movement, then the changes are successfully taking effect

11.40. Control Panel
It isn't a bad idea to skim through both the legacy and immersive control panel to ensure nothing is misconfigured.

11.41. Configuring Applications
Install any programs and applications that you use (including games) to prepare us for the next steps

If applicable, favor portable editions of programs as installers tend to leave bloatware behind even after uninstalling them however, this can be circumvented by using programs such as Bulk-Crap-Uninstaller

11.41.1. NVIDIA Reflex
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

NVIDIA Reflex minimizes queued frames in the GPU render queue by dynamically adjusting the framerate in GPU-intensive gaming scenarios and can be enabled in-game if the developer has added support for it. Although this minimizes latency, it acts as a dynamic framerate limiter and can result in minor stuttering or frametime variance. For this reason, I would recommend extensively benchmarking this rather than blindly enabling it in your chosen games.

See NVIDIA Reflex Low Latency - How It Works & Why You Want To Use It | Battle(non)sense
11.41.2. Framerate Limit
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

If you cap your framerate, ensure to set it at a multiple of your monitor refresh rate (calculator) to prevent frame mistiming and a rolling tearline (1, 2). Reducing your refresh rate to avoid mismatching is also applicable (instructions). Other options include Variable Refresh Rate

Ensure that the GPU isn't fully utilized as lower GPU utilization reduces system latency (1, 2)

Capping your framerate with RTSS instead of the in-game limiter will result in consistent frame pacing and a smoother experience as it utilizes busy-wait which offers higher precision than 100% passive-waiting but at the cost of noticeably higher latency and potentially greater CPU overhead (1, 2). Disabling the Enable dedicated encoder server service setting prevents EncoderServer.exe from running

11.41.3. Register Game in Config Store
Ensure that Xbox Game Bar acknowledges the game that you are running or have installed. If not, open Game Bar by pressing Win+G and enabling Remember this is a game while it is open. This also ensures that Game Mode functions properly if you choose to use it.

11.41.4. Presentation Mode
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

This is not a recommendation of what presentation mode to use and is instead, here for informative purposes.

Always verify whether your game is using the desired presentation mode with PresentMon (instructions)

You can experiment and benchmark different presentation modes to assess which you prefer

See Presentation Model | Special K Wiki
If there are no results after searching for the application's binary name in HKCU\SYSTEM\GameConfigStore within registry, you may need to register the game by pressing Win+G and enabling Remember this is a game while it is open. Check whether the entry has been created under the aforementioned registry key once completed

If you want to use the Hardware: Legacy Flip presentation mode, tick the Disable fullscreen optimizations checkbox. If that doesn't work, try running the commands below in CMD and reboot. These registry keys are typically accessed by the game and Windows upon launch

reg add "HKCU\SYSTEM\GameConfigStore" /v "GameDVR_DXGIHonorFSEWindowsCompatible" /t REG_DWORD /d "1" /f
reg add "HKCU\SYSTEM\GameConfigStore" /v "GameDVR_FSEBehavior" /t REG_DWORD /d "2" /f
If you are stuck with Hardware Composed: Independent Flip and would like to use another presentation mode, try running the command below to disable MPOs in CMD and reboot

reg add "HKLM\SOFTWARE\Microsoft\Windows\Dwm" /v "OverlayTestMode" /t REG_DWORD /d "5" /f
11.41.5. Game Mode
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

Game Mode prevents Windows Update running and certain notifications from being pushed to the user (1).

It is worth noting that Game Mode can intefere with process and thread priority boosts depending on the value of PsPrioritySeparation as explained in section Thread Quantums and Scheduling. This is evident by replicating the listening to thread priority boosts experiment in Windows Internals using Performance Monitor and the thread current priority performance counter. For this reason, you can experiment with Game Mode enabled and disabled.

11.41.6. Media Player
mpv or mpv.net
mpc-hc (updated fork)
VLC
11.41.7. QoS Policies
Depending on your network and router configuration, QoS policies can be set in Windows to prioritize packets of an application.

See assets/images/dscp-46-qos-policy.png

See DSCP and Precedence Values | Cisco

See The QoS Expedited Forwarding (EF) Model | Network World

See How Can You Verify Whether a DSCP QoS Policy Is Working?

Microsoft recommend the registry entry below to ensure packets are correctly tagged with the DSCP value, especially when more than one network adapter is present or the policy is used outside a domain (1)

reg add "HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\QoS" /v "Do not use NLA" /t REG_SZ /d "1" /f
11.42. Kernel-Mode Scheduling (Interrupts, DPCs and more)
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

Windows schedules interrupts and DPCs on CPU 0 for several kernel-mode modules by default. In any case, scheduling many tasks on a single CPU can introduce additional overhead and increased jitter due to them competing for CPU time. To alleviate this, affinities can be configured to isolate given modules from disturbances including servicing time-sensitive modules on underutilized CPUs instead of clumping everything on a single CPU.

Use the xperf DPC/ISR report generated by the xperf-dpcisr.bat script to analyze which CPUs kernel-mode modules are being serviced on. You can not manage affinities if you do not know what is running and which CPU(s) they are running on to begin with. The same concept applies to user-mode threads. Additionally, verify whether interrupt affinity policies are performing as expected by analyzing per-CPU usage for the module in question while the device is busy

Additionally, core-to-core-latency benchmarks can assist with decision-making in terms of affinity management

See CXWorld/MicroBenchX
Ensure that the corresponding DPC for an ISR is processed on the same CPU (example). Additional overhead can be introduced if they are processed on different CPUs due to increased inter-processor communication and interfering with cache coherence

Use Microsoft Interrupt Affinity Tool or GoInterruptPolicy to configure driver affinities. The device can be identified by cross-checking the Location in the Properties -> General section of a device in Device Manager

11.42.1. GPU and DirectX Graphics Kernel
AutoGpuAffinity can be used to benchmark the most performant CPUs that the GPU-related modules are assigned to. Configure the custom_cpus option in the config file if applicable. This option is useful for selecting a certain set of cores to benchmark such as P-Cores or a specific CCX/CCD.

11.42.2. XHCI and Audio Controller
The XHCI and audio controller related modules generate a substantial amount of interrupts upon interaction respective of the relevant device. Isolating the related modules to an underutilized CPU is beneficial for reducing contention.

11.42.3. Network Interface Card
The NIC must support MSI-X for Receive Side Scaling to function properly (1). In most cases, RSS base CPU is enough to migrate DPCs and ISRs for the NIC driver which eliminates the need for an interrupt affinity policy. However, if you are having trouble migrating either to other CPUs, try configuring both.

Keep in mind that the amount of RSS queues determines the amount of consecutive CPUs that the network driver is scheduled on. For example, the driver will be scheduled on CPU 2/3/4/5 (2/4/6/8 with HT/SMT enabled) if RSS base CPU is set to 2 along with 4 RSS queues configured.

See How many RSS Queues do you need?

See Receive Side Scaling (RSS) Configuration

11.43. User-Mode Scheduling (Processes, Threads)
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

There are several methods to set affinities for processes. One of which is Task Manager but only persists until the process is closed. A more popular and permanent solution is Process Lasso which allows the configuration to be saved however, a process must run continually in the background which introduces minor overhead. To work around this, you can simply launch the application with a specified CPU affinity which eliminates the requirement of programs such as Process Lasso for affinity management at the expense of usability.

Use the CPU Affinity Mask Calculator to determine the desired hexal affinity bitmask

In some cases, process can be protected so specifying the affinity may fail. To work around this, you can try specifying the affinity for the parent processes which will cause the child process to inherit the affinity when spawned. As an example, a game launcher is usually the parent process of a game. Process Explorer's process tree can be used to identify parent and child processes

Process Hacker and WindowsD can bypass several process-level protections through exploits but is not advised as they interfere with anticheats
It may be worth benchmarking the performance scaling of your application against core count as it may behave differently due to poor scheduling implementations from the application and/or OS. In some cases, it is possible that the application may perform better with fewer cores assigned to it via an affinity mask (1). This will also give you a rough idea as to how many cores you can reserve. In other cases, it can severely harm performance as there is a potential for the game to create more worker threads than CPUs due to the game only considering the amount of physical cores available hence, it is vital that performance scaling is measured

11.43.1. Starting a Process with a Specified Affinity Mask
The command below starts notepad.exe with an affinity of CPU 1 and CPU 2 as an example which will reflect in Task Manager. This command can be placed in a batch script for easy access and must be used each time to start the desired application with the specified affinity.

start /affinity 0x6 notepad.exe
11.43.2. Specifying an Affinity Mask for Running Processes
Sometimes, the processes that you would like to set an affinity mask to are already running, so the previous command is not applicable here. As a random example, the command below sets the affinity mask of the svchost.exe and audiodg.exe processes to CPU 3. Use this example to create a PowerShell script then have it run at startup using Task Scheduler (instructions). Ensure to wrap any paths with quotes if there are spaces in them. Ensure to verify whether everything is working correctly after a system restart. You need to enable the Run with highest privileges option if administrator privileges are required. For PowerShell scripts, set the program to start to PowerShell and the arguments to the path of the script (e.g. C:\process-affinities.ps1).

Get-Process @("svchost", "audiodg") -ErrorAction SilentlyContinue | ForEach-Object { $_.ProcessorAffinity=0x8 }
11.44. Reserved CPU Sets (Windows 10+)
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

ReservedCpuSets can be used to prevent Windows routing ISRs, DPCs and scheduling other threads on specific CPUs. Isolating modules from user and kernel-level disturbances helps reduce contention, jitter and allows time-sensitive modules to get the CPU time they require.

As mentioned in section User-Mode Scheduling (Processes, Threads), you should determine how well or poorly your application's performance scales with core count to give you a rough idea as to how many cores you can afford to reserve

As interrupt affinity policies, process and thread affinities have higher precedence, you can use this hand in hand with user-defined affinities to go a step further and ensure that nothing except what you assigned to specific CPUs will be scheduled on those CPUs

Ensure that you have enough cores to run your real-time application on and aren't reserving too many CPUs to the point where isolating modules does not yield real-time performance

As CPU sets are considered soft policies, the configuration isn't guaranteed. A CPU-intensive process such as a stress-test will utilize the reserved cores if required

Important

Unexpected behavior occurs when a process affinity is set to both reserved and unreserved CPUs. Ensure to set the affinity to either reserved or unreserved CPUs, not a combination of both.

11.44.1. Use Cases
Hinting to the OS to schedule tasks on a group of CPUs. An example of this with modern platforms could be reserving E-Cores (efficiency cores) or either CCX/CCDs so that tasks are scheduled on P-Cores (performance cores) or other CCX/CCDs by default. With this approach, you can explicitly enforce background and unimportant tasks to be scheduled on the reserved CPUs. Note that this is purely an example and the logic can be flipped, but some latency-sensitive processes and modules are protected so affinity policies may fail which is a major limitation. There are several possibilities and trade-offs to consider. Note that performance can degrade when reserving E-Cores or other CCX/CCDs as applications may make use of them. Therefore, it is vital that you measure performance scaling when reserving cores whether it be one, a few or a set of CPUs. Another way of severly degrading performance by reserving E-Cores or CCX/CCDs is that the scheduler or applications can specifically target reserved cores for work to be scheduled on them as the RealTime field is set to 1 in the SYSTEM_CPU_SET_INFORMATION struct

Reserving CPUs that have specific modules assigned to be scheduled on them

11.45. Analyzing Event Viewer
This step isn't required, but can help to justify unexplained performance issues or issues in general. Ensure that there are no errors present on Event Viewer by typing eventvwr.msc in Win+R as anything you may have changed to your operating system could lead to internal errors or exceptions being thrown periodically.

Merge the ets-enable.reg file that was generated in section Event Trace Sessions (ETS) if applicable as it is required for event logging
11.46. Virtualization Based Security (VBS)
Virtualization Based Security negatively impacts performance (1) and in some cases, it is enabled by default. Its status can be determined by typing msinfo32 in Win+R and can be disabled (1, 2) if required. On the other hand, privacyguides.org recommend keeping it enabled. VBS should be disabled when virtualization is disabled in BIOS, so be careful of VBS being enabled if you enable virtualization in BIOS for future reference.

11.47. CPU Idle States
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

Disabling idle states forces C-State 0, which can be seen in HWiNFO, and is in Microsoft's recommendations for configuring devices for real-time performance (1). Forcing C-State 0 mitigates the undesirable delay to execute new instructions on a CPU that has entered a deeper power-saving state at the expense of higher temperatures and power consumption. Therefore, I would recommend keeping idle states enabled for the majority of readers as other problems can occur due to these side effects (e.g. throttling, power issues). The CPU temperature should not increase to the point of thermal throttling because you should have already assessed that in section Stability, Hardware Clocking and Thermal Performance.

If a static CPU frequency is not set, the effects of forcing C-State 0 should be assessed in terms of frequency boosting behavior. For example, you certainly wouldn't want to disable idle states when relying on Precision Boost Overdrive (PBO), Turbo Boost or similar features. Avoid disabling idle states with Hyper-Threading/Simultaneous Multithreading enabled as single-threaded performance is usually negatively impacted.

11.47.1. Enable Idle States (default)
powercfg /setacvalueindex scheme_current sub_processor 5d76a2ca-e8c0-402f-a133-2158492d58ad 0 && powercfg /setactive scheme_current
11.47.2. Disable Idle States
powercfg /setacvalueindex scheme_current sub_processor 5d76a2ca-e8c0-402f-a133-2158492d58ad 1 && powercfg /setactive scheme_current
11.48. Thread Quantums and Scheduling
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

A quantum is the time designated for which a thread can execute before the scheduler evaluates whether another thread with the same priority is scheduled to execute. If a thread finishes its quantum and no other threads at its priority level are ready to execute, the scheduler allows the thread to continue running for an additional quantum. The quantum can be controlled with the registry key below, in addition to defining how much time of the quantum is allocated to background and foreground threads. The value is represented as a 6-bit bitmask such that each of the three pairs of bits determine the quantum's characteristics and distribution of time between background and foreground threads. By default, it is set to 0x2 which corresponds to 0b000010 and has different meanings on client and server editions as explained shortly.

[HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\PriorityControl]
"Win32PrioritySeparation"=dword:00000002
11.48.1. Bitmask Explaination
The leftmost bit pair (XXYYZZ) determine the quantum length. This is represented by PspForegroundQuantum

Value	Description
00/11	Short Intervals (Windows Client), Long Intervals (Windows Server)
01	Long Intervals
10	Short Intervals
The middle bit pair (XXYYZZ) determine whether the quantum length is variable or fixed. If a fixed-length quantum is used, then the rightmost bit pair is ignored as the ratio that determines the time allocated to background and foreground threads within the quantum is fixed. This is represented by PspForegroundQuantum

Value	Description
00/11	Variable-length (Windows Client), Fixed-length (Windows Server)
01	Variable-length
10	Fixed-length
The rightmost bit pair (XXYYZZ) determine the ratio of time in the quantum allocated to background and foreground threads in which, foreground threads can be allocated up to three times as much processor time than background threads. As mentioned previously, this can only be configured with variable-length quantums. This is represented by PsPrioritySeparation

Value	Description
00	1:1
01	2:1
10/11	3:1
Using the information above, the default value of 0x2 corresponds to short, variable-length, 3:1 on Windows Client and long, fixed-length, 3:1 on Windows Server

11.48.2. Win32PrioritySeparation Values
The table below consists of all possible values that are consistent between client and server editions of Windows as 00 or 11 were not used in XXYYZZ of the bitmask which have different meanings on client and server editions. Any value not specified in the table is identical to one that is stated in the table as explained here, hence the values in the table are the only ones that should be used. The time in milliseconds are based on the modern x86/x64 multiprocessor timer resolution.

Although a foreground boost can not be used when using a fixed length interval in terms of the quantum, PsPrioritySeparation still changes, and another thread priority boosting mechanism just happens to use the value of it so in reality, a fixed 3:1 quantum should have a perceivable difference compared to a fixed 1:1 quantum. See the paragraph below from Windows Internals.

As will be described shortly, whenever a thread in the foreground process completes a wait operation on a kernel object, the kernel boosts its current (not base) priority by the current value of PsPrioritySeparation. (The windowing system is responsible for determining which process is considered to be in the foreground.) As described earlier in this chapter in the section “Controlling the quantum,” PsPrioritySeparation reflects the quantum-table index used to select quantums for the threads of foreground applications. However, in this case, it is being used as a priority boost value.

For the majority of readers, I would simply recommend leaving it at default. Although, a mixture of the quantum length and foreground/background time allocation ratio can influence how often a thread switches context depending on whether thread's runtime exceeds its allocated time in the quantum as described previously hence you can benchmark whether it influences performance in your chosen applications if desired. If you are using Windows Server on a desktop system, the value can be set to 0x26 which mimics the same behavior as 0x2 does on Windows Client editions.

Hexadecimal	Decimal	Binary	Interval	Length	PsPrioSep	ForegroundQU	BackgroundQU	TotalQU
0x14	20	0b010100	Long	Variable	0	12 (62.50ms)	12 (62.50ms)	24 (125.00ms)
0x15	21	0b010101	Long	Variable	1	24 (125.00ms)	12 (62.50ms)	36 (187.50ms)
0x16	22	0b010110	Long	Variable	2	36 (187.50ms)	12 (62.50ms)	48 (250.00ms)
0x18	24	0b011000	Long	Fixed	0	36 (187.50ms)	36 (187.50ms)	72 (375.00ms)
0x19	25	0b011001	Long	Fixed	1	36 (187.50ms)	36 (187.50ms)	72 (375.00ms)
0x1A	26	0b011010	Long	Fixed	2	36 (187.50ms)	36 (187.50ms)	72 (375.00ms)
0x24	36	0b100100	Short	Variable	0	6 (31.25ms)	6 (31.25ms)	12 (62.50ms)
0x25	37	0b100101	Short	Variable	1	12 (62.50ms)	6 (31.25ms)	18 (93.75ms)
0x26	38	0b100110	Short	Variable	2	18 (93.75ms)	6 (31.25ms)	24 (125.00ms)
0x28	40	0b101000	Short	Fixed	0	18 (93.75ms)	18 (93.75ms)	36 (187.5ms)
0x29	41	0b101001	Short	Fixed	1	18 (93.75ms)	18 (93.75ms)	36 (187.5ms)
0x2A	42	0b101010	Short	Fixed	2	18 (93.75ms)	18 (93.75ms)	36 (187.5ms)
11.49. Clock Interrupt Frequency (Timer Resolution)
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

The clock interrupt frequency is the rate at which the system's hardware clock generates interrupts which allow the scheduler to perform various tasks such as timekeeping. On most systems by default, the minimum frequency is 64Hz, meaning that a clock interrupt is generated every 15.625ms. A lower frequency results in reduced CPU overhead and power consumption due to fewer interrupts but reduces timing precision and results in potentially less responsive multitasking. The maximum frequency is 2kHz, meaning that a clock interrupt is generated every 0.5ms. A higher frequency results in higher timing precision, potentially higher multitasking responsiveness but increases CPU overhead and power consumption. The minimum, current and maximum resolutions can be viewed in ClockRes.

Applications that require higher precision than the default resolution of 15.625ms are able to raise the clock interrupt frequency through functions such as timeBeginPeriod and NtSetTimerResolution in which, these scenarios typically consist of multimedia playback, gaming, VoIP activity and more which can be seen by running an energy trace (instructions) during runtime. The precision of features that rely on sleep-related functions to pace events are directly influenced by the clock interrupt frequency (1). Using Sleep as an example, Sleep(n) should sleep for n milliseconds in actuality and not n plus/minus an arbitrary value otherwise, it can result in unexpected and inconsistent event pacing which is not ideal for features such as sleep-based framerate limiters. Note that this is an example and many real-world applications do not rely specifically on the Sleep function for event pacing. A typical value that developers appears to raise the resolution to is 1ms which means that the application can maintain a pace of events within a resolution of 1ms. In very rare cases, developers may not raise the resolution at all while their application relies on it for event pacing precision leading to breakage, but this is not common and may be applicable to some obscure programs such as lesser-known games.

The implementation of timer resolution changed in Windows 10 2004+ such that the calling process raising the resolution does not affect the system on a global level meaning, process A raising the resolution to 1ms does not affect process B at the default 15.625ms resolution unlike before. This is a great change in and of itself because it reduces overhead as other processes such as idle background processes don't get serviced by the scheduler often and the calling process receives higher precision as needed. However as an end-user, this results in limitations when wanting to leverage higher resolutions such as 0.5ms. Given that games are not open-source to modify the code along with anticheat limitations preventing DLL injection or binary patching to raise the resolution beyond 1ms the per-process way, the only other option is to resort to the global behavior which is applicable with the registry key below on Windows Server and Windows 11+ as explained in depth here.

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\kernel]
"GlobalTimerResolutionRequests"=dword:00000001
This provides the ability to raise the resolution in a separate process which in turn, results in the desired application such as a game receiving higher precision. However as mentioned previously, the per-process implantation reduces overhead which is no longer the case when the global behavior is restored and background processes are also serviced unnecessarily often. RTSS is an alternative method for framerate limiting and utilizes hybrid-wait which results in greater precision while eliminating the need for restoring the global behavior.

A higher resolution results in higher precision, but in some cases, the maximum supported resolution of 0.5ms provides less precision than something slightly lower such as 0.507ms (1). Therefore, it is sensible to determine what calling resolution provides the highest precision (the lowest deltas) in the MeasureSleep program while requesting different resolutions with the SetTimerResolution program. This should be carried out under load as idle benchmarks may be misleading. The micro-adjust-benchmark.ps1 script can be used to automate the process.

To conclude my view on the topic, I recommend favoring the per-process (non-global) implementation where applicable as it reduces overhead and instead use RTSS for precise framerate limiting. It is worth noting that it can introduce noticeably higher latency (1, 2) therefore I recommend comparing and benchmarking it against micro-adjusting the requested resolution for higher precision with the global behavior. It is possible that frametime stability is unaffected by raising the resolution beyond 1ms due to improvements in the in-game framerate limiter which in that case, no action is required. The primary point I want to convey is to compare all available options, with a preference of using the per-process behavior which is the default on Windows 10 2004+ if you find that raising the resolution further has little to no impact.

11.50. Paging File
Caution

📊 Do NOT blindly follow the recommendations in this section. Do benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance (instructions).

For most readers, I would recommend keeping the paging file enabled which is the default state. There is an argument that it is preferable to disable it if you have enough RAM for your applications as it reduces I/O overhead and that system memory is faster than disk however, many users have reported in-game stuttering in specific games with the paging file disabled despite being nowhere near maximum RAM load. Windows appears to allocate the page file to secondary drives sometimes which can be problematic if one of the drives is a HDD. This can be resolved by allocating the page file to an SSD and its size to "system managed size" then deallocating it on other drives.

11.51. Cleanup and Maintenance
It isn't a bad idea to revisit this step every so often. Setting a reminder to do so can be helpful in maintaining a clean system.

Favor tools such as Bulk-Crap-Uninstaller to uninstall programs as the regular control panel does not remove residual files

Use Autoruns to remove any unwanted programs from launching at startup and check it often, especially after installing a program

Configure Disk Cleanup

Open CMD and enter the command below, tick all the boxes except DirectX Shader Cache then press OK

cleanmgr /sageset:0
Run Disk Cleanup

cleanmgr /sagerun:0
Some locations you may want to review for residual files

C:\ - residual junk
"C:\ProgramData\Microsoft\Windows\Start Menu\Programs" - start menu shortcuts (don't delete windows-related shortcuts)
C:\Windows\Prefetch - prefetch files (this folder should not be populated when superfetch is disabled)
C:\Windows\SoftwareDistribution - Windows Update download cache
C:\Windows\Temp - temporary files
"%userprofile%" - residual junk
"%userprofile%\AppData\Local\Temp" - temporary files
"%userprofile%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs" - start menu shortcuts (don't delete windows-related shortcuts)
User directories - e.g. Downloads, Documents, Pictures, Music, Videos, Desktop
Optionally clean the WinSxS folder to reduce the size of it (1) with the command below in CMD. Note that this can be a lengthy process

DISM /Online /Cleanup-Image /StartComponentCleanup /ResetBase
Optionally delete obsolete system restore points in the System Protection tab by typing sysdm.cpl in Win+R. It can be disabled completely if you don't use it
