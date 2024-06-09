# **Script Summary**

## **Overview**

This PowerShell script performs several key tasks:

1. Decodes a base64 encoded batch file.
2. Creates and executes a temporary batch file.
3. Reads configuration from an **.ini** file.
4. Starts an executable process (**cc-qt.exe**) in a detached manner.
5. Cleans up temporary files and exits gracefully.

**Detailed Breakdown**

**1. Decoding the Base64 Encoded Batch File**

powershell

```
if ($actualHash -eq $expectedHash)
{ $decodedBatch =
[System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String($encodedBatch
-join "")) $batchCommands = $decodedBatch -split "`r`n" 
}
```

- **Purpose**:
   Verifies the integrity of the base64 encoded batch file and decodes it.

- **Process**:
  
  - **Checks**
     if the actual SHA-256 hash matches the expected hash.
  
  - **Decodes**
     the base64 string to obtain the original batch file content.
  
  - **Splits**
     the decoded content into individual commands.

**2. Creating and Executing the Temporary Batch File**

powershell

```
$tempBatchFile = [System.IO.Path]::GetTempFileName() +".bat"
Set-Content -Path $tempBatchFile -Value $batchCommands-Encoding ASCII
Write-Output "Start the process using cmd.exe..."
try { 
    $process = Start-Process -FilePath "cmd.exe" -ArgumentList "/c", $tempBatchFile -Wait -NoNewWindow -PassThru
    if ($process.ExitCode -eq 0) {
        Write-Output "Process completed successfully."
    } else {
        Write-Output "Process completed with exit code $($process.ExitCode)."
    }
} catch {
    Write-Error "Failed to start or wait for process: $_"
} 
Remove-Item -Path $tempBatchFile -ErrorAction SilentlyContinue
```

- **Purpose**:
   Creates a temporary batch file from the decoded content and executes it.

- **Process**:
  
  - **Writes**
     the decoded commands to a temporary batch file.
  
  - **Executes**
     the batch file using **cmd.exe** and waits for it to complete.
  
  - **Checks**
     the exit code to determine if the batch file executed successfully.
  
  - **Cleans**
     up by deleting the temporary batch file.

**3. Reading Configuration from the .ini File**

powershell

```
$iniFilePath = ".\ccback.ini"
function Get-IniContent {
    param (
        [string]$filePath
    )
    $iniContent = @{}
    foreach ($line in Get-Content -Path $filePath) {
        $line = $line.Trim()

        if ($line -match '^\s*([^=]+?)\s*=\s*(.*?)\s*$') {
            $key = $matches[1].Trim()
            $value = $matches[2].Trim()
            $iniContent[$key] = $value
        }
    }
    return $iniContent

}
$iniContent = Get-IniContent -filePath $iniFilePath
$ccqtPath = $iniContent["ccqtPath"]
$dataDir = $iniContent["dataDir"]

Write-Output "End of script...Exiting..."
exit
```

- **Purpose**:
   Reads the **.ini** file to extract configuration parameters.

- **Process**:

- Defines
   a function to read and parse the **.ini** file.

- Extracts
   key-value pairs for **ccqtPath** and **dataDir**.

- Validates
   the existence of these parameters, and exits with an error if not found.

**4. Starting the Executable Process**

powershell

```
Start-Process -FilePath ccqtPath -ArgumentList @("-datadir=dataDir", "-conf=$dataDir\cc.conf")
```

- **Purpose**:
   Starts the **cc-qt.exe** process in a detached manner, allowing the
   script to complete without waiting for the process to finish.

- **Process**:
  
  - **Uses**
     **Start-Process** to run **cc-qt.exe** with specified arguments.
  
  - **Ensures**
     the process runs without opening a new window and without tying its
     execution to the script.

**5. Script Completion**

powershell

```
Write-Output "End of script...Exiting..." exit
```

**Purpose**:
Outputs a completion message and explicitly exits the PowerShell script.
