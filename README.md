# CampusCoin Snapshot Backup and Restoration

## Overview

Blockchain technology, while revolutionary, is not without its challenges. One of the most significant issues faced by users is the potential for a corrupted local copy of the blockchain database. Such corruption can occur due to improper shutdowns, hardware failures, or software bugs, leading to a compromised ability to participate in the network. For Windows users of the CampusCoin blockchain, this project provides a robust solution to mitigate the risk of blockchain database corruption.

## Solution: Snapshot Backup and Restoration

This project includes scripts designed to create and restore snapshots of your CampusCoin blockchain data. By regularly backing up your blockchain data, you can ensure that you have a reliable copy to restore from in case of corruption. The provided solution leverages PowerShell scripts and batch files obfuscated with base64 encoding for security and integrity purposes.

## Key Features

- **Regular Backups**: Regularly create compressed snapshots of your blockchain data.
- **Easy Restoration**: Quickly restore your blockchain data from a snapshot in case of corruption.
- **Customizable Configuration**: Define paths and settings in an `.ini` file for easy customization.
- **Integrity Verification**: Ensures the integrity of the backup and restoration process with SHA-256 hash verification.

## Script Overview

### **Backup Script**

1. **Set Paths**: Defines the paths to essential executables and directories.
2. **Query Block Height**: Uses `cc-cli.exe` to query the current block height from `cc-qt.exe`.
3. **Shutdown Application**: Sends a safe shutdown command to `cc-qt.exe`.
4. **Create Backup**: Uses 7-Zip to compress the blockchain data directories.
5. **Verify Backup**: Checks the exit code of 7-Zip to ensure successful backup creation.
6. **Complete Process**: Cleans up temporary files and restarts `cc-qt.exe`.

### **Restore Script**

1. **Read Configuration**: Extracts paths and settings from the `.ini` file.
2. **Query Block Height**: Reads the block height as recorded from the backup logfile.
3. **Shutdown Application**: Sends a safe shutdown command to `cc-qt.exe`.
4. **Remove Old Data**: Deletes the current `Blocks` and `Chainstate` directories.
5. **Extract Backup**: Uses 7-Zip to restore the blockchain data from the backup.
6. **Verify Restoration**: Checks the exit code of 7-Zip to ensure successful restoration.
7. **Complete Process**: Cleans up temporary files and restarts `cc-qt.exe`.

### **Dependencies**

- **7-Zip Console Executable**: Required for creating and extracting compressed archives. Install 7-Zip and download the `7zr.exe` to the 7-Zip program directory.
  
  - [7-Zip Download Page](https://www.7-zip.org/download.html)
  - [7zr.exe](https://www.7-zip.org/a/7zr.exe)

- **CampusCoin Wallet**: The `cc-qt.exe` and `cc-cli.exe` executables are required.
  
  - [CampusCoin Wallet Download](https://github.com/campuscoindev/CC/releases/download/3.0.2.2/cc_w64.zip)

- **PowerShell**: The scripts are written in PowerShell and Batch which require Windows PowerShell for execution.

## License

This project is licensed under the MIT License (Custom). Please refer to the license terms below:

# MIT License (Custom)

## Copyright (c) 2024 ARCH BEARD

### Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to use, copy, modify, merge, publish, distribute, and/or sublicense copies of the Software for use within the CampusCoin project, subject to the following conditions: 1. The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software. 2. Any modification or derivative works of the Software shall only be used within the CampusCoin project. 3. Separate licensing terms are required for use of the Software or any modification or derivative works outside of the CampusCoin project. Please contact ARCH BEARD for licensing inquiries.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## Conclusion

By implementing this snapshot backup and restoration solution, Windows users of CampusCoin can safeguard against the potential pitfalls of blockchain database corruption. This project provides a reliable and efficient method to maintain the integrity of your blockchain data, ensuring smooth and uninterrupted participation in the CampusCoin network.
