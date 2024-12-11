# TwinCAT 4026 Offline Upgrade

## Disclaimer

This is a personal guide not a peer reviewed journal or a sponsored publication. We make
no representations as to accuracy, completeness, correctness, suitability, or validity of any
information and will not be liable for any errors, omissions, or delays in this information or any
losses injuries, or damages arising from its display or use. All information is provided on an as
is basis. It is the reader’s responsibility to verify their own facts.

The views and opinions expressed in this guide are those of the authors and do not
necessarily reflect the official policy or position of any other agency, organization, employer or
company. Assumptions made in the analysis are not reflective of the position of any entity
other than the author(s) and, since we are critically thinking human beings, these views are
always subject to change, revision, and rethinking at any time. Please do not hold us to them
in perpetuity.

## Overview

Quick start guide for upgrading an IPC to 4026 with no internet connection.

## Steps

All steps below assume that TwinCAT Package Manager has been installed on both Engineering and IPC.

1. **Create a Folder for Offline Files**  
   On your engineering laptop, create a folder named `C:\PackagesOffline`.

2. **Download the Required Packages**  
   Use the following commands to download the necessary packages. Only the `TwinCAT.Standard.XAE` package is required if you're using engineering tools.

   - To list available workloads, run:

     ```bash
     tcpkg list -t workload
     ```

   - Typical packages to download:
     ```bash
     tcpkg download TwinCAT.Standard.XAE -o "C:\PackagesOffline"
     tcpkg download TwinCAT.Standard.XAR -o "C:\PackagesOffline"
     tcpkg download TwinCAT.XAE.MigrateCli -o "C:\PackagesOffline"
     # add as many packages or workflows as needed
     ```

3. **Transfer Files to the IPC**  
   Once all packages are downloaded, copy the `C:\PackagesOffline` folder to the IPC.

4. **Set Up the Package Manager**  
   Add the local package source using the following command:

   ```bash
   tcpkg source add -n=Local -s=C:\PackagesOffline --priority=1
   ```

   If you make a mistake while setting the local source, you can remove it with

   ```bash
   tcpkg source remove local
   ```

5. **Install the Migration Package**
   Install the migration CLI tool with this command:

   ```bash
   tcpkg install TwinCAT.XAE.MigrateCli
   ```

6. **\*Reboot and Upgrade**
   Reboot the system, then run the following command to upgrade (note: the command is case-sensitive):

   ```bash
   TcMigrateCmd upgrade --whatIf False
   ```
