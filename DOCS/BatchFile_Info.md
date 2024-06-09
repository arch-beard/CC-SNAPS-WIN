# **Backup Batch File Summary**

## **Overview**

The backup batch file encoded to base64 is designed to
create a compressed archive of specified directories and files. The archive is
created using 7-Zip, and the batch file ensures that all necessary directories
exist before starting the backup process. The resulting backup file is saved
with a timestamp and block height in the logfile.  The backup batch also initially generates the ccback.ini file where the user may specify path locations, use standard
defaults, or should ccback.ini exist, automatically move forward using the values contained within to continue with the backup process.

# **Restore Batch File Summary**

## **Overview**

The restore batch file is designed to initially look for existence of
the ccback.ini and use those values toward successful extraction of the contents of the specified backup archive into the blocks and chainstate directory. The batch file ensures that the CC-Qt.exe is safetly stopped, and both target directories are recreated during the extraction process. The extraction is performed using the 7-Zip console executable.

# **Detailed Scripts Summary**

## **Backup Batch File**

1. **Set Paths**:
   
   - **sevenZipPath**: Path to the 7-Zip Console executable.
   - **cccliPath**: Path to the CampusCoin cc-cli.exe.
   - **dataDir**: Path to the main CC blockchain directory.

2. **Query CC-QT.exe through CC-CLI.exe**:
   
   - Asks **CC-QT.exe** the current block height it contains.

3. **Sends the Safe Application Shutdown Command to CC-QT.exe**:
   
   - Ensures a proper and safe shutdown of the CampusCoin application.

4. **Run 7-Zip and Create the Backup**:
   
   - Uses 7-Zip to create a compressed archive of the two source directories.

5. **Check Exit Code**:
   
   - Verifies if the backup was successful by checking the exit code of 7-Zip.

6. **Exit**:
   
   - Exits the batch file, handing off to PowerShell for standard completion and startup of **CC-QT.exe** with defined parameters from **ccbackup.ini**.

## **Restore Batch File**

1. **Query ccabck.ini and Read Paths**:
   
   - **sevenZipPath**: Path to the 7-Zip executable.
   - **ccqtPath**: Path to the **CC-QT.exe**.
   - **dataDir**: Path to the main CC blockchain directory.
   - **cccliPath**: Path to the **CC-CLI.exe**.

2. **Talk to CC-QT.exe through CC-CLI.exe**:
   
   - **CC-CLI.exe**: Reads the current block height from the corresponding backup logfile.
   - Sends the safe application shutdown command to **CC-QT.exe**.

3. **Remove both the Blocks & Chainstate Directories**:
   
   - Old Blocks and Chainstate directories are removed.

4. **Run 7-Zip to Extract Backup**:
   
   - Uses 7-Zip to extract the contents of the backup file to the Blocks and Chainstate directories.

5. **Check Exit Code**:
   
   - Verifies if the restore was successful by checking the exit code of 7-Zip.

6. **Exit**:
   
   - Exits the batch file.

**NOTE**: Both batch files are obfuscated using Base64 for security and integrity purposes and bundled within the PowerShell scripts. Both are human-readable if converted from Base64 to text.
