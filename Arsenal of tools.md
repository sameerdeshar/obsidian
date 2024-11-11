---
tags:
  - cyberchef
---
In this task, we'll introduce you to tools inside the FlareVM. It has many specialized forensics, incident response, and malware investigation tools.

Below are the tools grouped by their category. 

## Reverse Engineering & Debugging

Reverse engineering is like solving a puzzle backward: you take a finished product apart to understand how it works. Debugging is identifying errors, understanding why they happen, and correcting the code to prevent them.

- **Ghidra** - NSA-developed open-source reverse engineering suite.  
    
- **x64dbg** - Open-source debugger for binaries in x64 and x32 formats.  
    
- **OllyDbg** - Debugger for reverse engineering at the assembly level.  
    
- **Radare2** - A sophisticated open-source platform for reverse engineering.
- **Binary Ninja** - A tool for disassembling and decompiling binaries.  
    
- **PEiD** - Packer, cryptor, and compiler detection tool.

## Disassemblers & Decompilers

Disassemblers and Decompilers are crucial tools in malware analysis. They help analysts understand malicious software’s behaviour, logic, and control flow by breaking it into a more understandable format. The tools mentioned below are commonly used in this category.

- **CFF Explorer** - A PE editor designed to analyze and edit Portable Executable (PE) files.
- **Hopper Disassembler** - A Debugger, disassembler, and decompiler.
- **RetDec** - Open-source decompiler for machine code.

## Static & Dynamic Analysis

Static and dynamic analysis are two crucial methods in cyber security for examining malware. Static analysis involves inspecting the code without executing it, while dynamic analysis involves observing its behaviour as it runs. The tools mentioned below are commonly used in this category.

- **Process Hacker** - Sophisticated memory editor and process watcher.
- **PEview** - A portable executable (PE) file viewer for analysis.
- **Dependency Walker** - A tool for displaying an executable’s DLL dependencies.
- **DIE (Detect It Easy)** - A packer, compiler, and cryptor detection tool.

## Forensics & Incident Response

Digital Forensics involves the collection, analysis, and preservation of digital evidence from various sources like computers, networks, and storage devices. At the same time, Incident Response focuses on the detection, containment, eradication, and recovery from cyberattacks. The tools mentioned below are commonly used in this category.

- **Volatility** - RAM dump analysis framework for memory forensics.
- **Rekall** - Framework for memory forensics in incident response.
- **FTK Imager** - Disc image acquisition and analysis tools for forensic use.

## Network Analysis

Network Analysis includes different methods and techniques for studying and analysing networks to uncover patterns, optimize performance, and understand the underlying structure and behaviour of the network.

- **Wireshark** - Network protocol analyzer for traffic recording and examination.  
    
- **Nmap** - A vulnerability detection and network mapping tool.  
    
- **Netcat** - Read and write data across network connections with this helpful tool.

## File Analysis

File Analysis is a technique used to examine files for potential security threats and ensure proper file permissions.

- **FileInsight** - A program for looking through and editing binary files.
- **Hex Fiend** - Hex editor that is light and quick.
- **HxD** - Binary file viewing and editing with a hex editor.

## Scripting & Automation

Scripting and Automation involve using scripts such as PowerShell and Python to automate repetitive tasks and processes, making them more efficient and less prone to human error.

- **Python** - Mainly automation-focused on Python modules and tools.
- **PowerShell Empire** - Framework for PowerShell post-exploitation.

## Sysinternals Suite

The Sysinternals Suite is a collection of advanced system utilities designed to help IT professionals and developers manage, troubleshoot, and diagnose Windows systems.

- **Autoruns** - Shows what executables are configured to run during system boot-up.
- **Process Explorer** - Provides information about running processes.
- **Process Monitor** -Monitors and logs real-time process/thread activity.

  

Have you checked all the categories? There are a lot, right? Worry not, as we won't tackle all those tools right now—it could take months to finish! We want to present you with the concept of having a single box filled with tools for different purposes, giving you an idea of what could work best for the specific task.


---
**Basic Tools for Initial Investigation in FlareVM**

**1. Procmon (Process Monitor)**  
- Tracks system activity for malware research, troubleshooting, and forensic investigations.
- Monitors file system, registry, and process activity in real-time.
- Example: Checking `lsass.exe` for standard system activity vs. suspicious credential dumping behavior.

**2. Process Explorer**  
- Provides details on active processes, including parent-child relationships, DLLs, and file paths.
- Useful for tracking spawned processes from files (e.g., Word docs or ISO files in malicious contexts).

**3. HxD**  
- Hex editor for examining file contents in hexadecimal and ASCII.
- Key in analyzing binary data to identify file types and structures.

**4. CFF Explorer**  
- Allows generating file hashes, authenticating sources, and verifying file integrity.
- Critical for detecting system file tampering often used to hide malicious code.

**5. Wireshark**  
- Network traffic analyzer that reveals patterns, protocols, and potential attacks.
- Example: Monitoring encrypted connections to identify abnormal activity in TLS sessions.

**6. PEStudio**  
- Provides static analysis of executable files, helping identify potential threats without executing them.
- Reveals details like entropy scores and file metadata for detecting malware indicators.

**7. FLOSS (FLARE Obfuscated String Solver)**  
- Extracts and de-obfuscates hidden strings in malware, such as file paths, IPs, or encryption keys.
- Useful for uncovering concealed malware behaviors without running the program.

These tools collectively cover essential areas like system monitoring, process exploration, hex editing, file integrity checking, network traffic analysis, and string de-obfuscation—key functions for initial malware investigations.

---
