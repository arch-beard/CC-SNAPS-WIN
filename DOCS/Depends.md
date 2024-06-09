# **CampusCoin Snapshot Backup and Restoration Dependencies for Windows**

## **Prerequisites for Successful Backup and Restore**

### 1. **7-Zip Console Executable**

**Description**:  
7-Zip is leveraged for creating and extracting highly compressed 7z archives. While only the separately downloaded 7-Zip Console Executable is utilized, it may be more useful at the Windows desktop level to simply install 7-Zip and then drop the separately downloadable 7-Zip Console Executable into the respective 7-Zip Program Files directory.

- **Download 7-Zip URL**: [7-Zip Download Page](https://www.7-zip.org/download.html)
- **Download the drop-in 7-Zip Console Executable**: [7zr.exe](https://www.7-zip.org/a/7zr.exe)
- **Installation**: Install 7-Zip, then download **7zr.exe** and place it in the 7-Zip program directory (e.g., **C:\Program Files\7-Zip\7zr.exe**).

### 2. **CampusCoin Windows Desktop GUI Client**

**Description**:  
As the Backup and Restoration is designed specifically for use with the CampusCoin blockchain wallet, extracting/installing the **cc-qt.exe** client is required for the scripts to function correctly.

- **Download URL**: [CampusCoin Wallet](https://github.com/campuscoindev/CC/releases/download/3.0.2.2/cc_w64.zip)

- **Installation**: Extract **cc-qt.exe** and **cc-cli.exe** in the same directory, perhaps to your desktop.

- **Initial Sync**: Run **cc-qt.exe** for a minute and walk through the installation questions. You may let it run and sync from the first block to the current block, however, that may take a day or more depending on your connection. You may speed up the process by downloading a more current publicly available snapshot (blocks, chainstate). Such is available at [archive.org](https://archive.org/details/@arch_beard), and a newer copy is also available through [DropBox](https://www.dropbox.com/scl/fi/ajn8vsebu56cfdbnz4qqp/CC-BOOTSTRAP.7z?rlkey=imidm8icnb6a3mqm99wewqzhh&dl=0).
1. **Note**: The blocks and chainstate directories are locked while the CampusCoin application is running. Close (File > Exit) the CampusCoin application before manually placing a newer snapshot. The existing blocks and chainstate folders on your computer (default location is %appdata%\CC) may be deleted and overwritten with an official snapshot, or even your own (once synched and have established a backup). Bring the CampusCoin application back up and allow the sync to complete either from scratch, or from the snapshot.

2. **Important**: The local blockchain replicated datasets (blocks and chainstate) are subject to data corruption in the event of improper shutdown and other causes. With CampusCoin Snapshot Creator and CampusCoin Snapshot Restorer, even in the event of local database corruption, your own snapshot can not only be created on demand but it can easily be restored whenever you need it. This functionality for any blockchain wallet is considered novel for Windows.

### 3. **CampusCoin Configuration File**

**Description**:  
A properly configured **cc.conf** file is required for **cc-cli.exe** to function properly, specifically for **cc-cli.exe** to query and record the block height of the snapshot being created.

- **Configuration example for cc.conf**:

```
staking=0
rpcuser=PICKANAME
rpcpassword=DEFINEPASSWORD
rpcallowip=127.0.0.1
listen=1
server=1
rpcconnect=127.0.0.1
```

- **Verification**: After modifying your **cc.conf**, stop/start the CampusCoin Wallet. You may ensure **cc-cli.exe** is communicating properly by opening a command prompt in the same directory (such as your desktop) and while **cc-qt.exe** is running, type **cc-cli getinfo**.

### 4. **PowerShell**

**Description**:  
The scripts use Windows PowerShell for execution. No local policy change is needed.

- **Command**: The scripts invoke PowerShell using **-ExecutionPolicy Bypass**.

### 5. **Base64 Encoding/Decoding**

**Description**:  
The batch file is obfuscated using base64 encoding for security and integrity purposes. The SHA256 hash of the base64 encoded data is also checked for consistency.

- **Usage**: The code can be enumerated and examined by users.

By ensuring you meet these prerequisites, you'll be well-equipped to manage backups and restorations of your CampusCoin blockchain directories on Windows, maintaining functionality, availability and security.
