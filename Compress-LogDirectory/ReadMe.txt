Compress-LogDirectory.ps1

Author: Markus Scholtes, 2019
Version: 1.0
Date: 2019-05-13

Powershell script to compress log files (and IIS logs)


This script compresses log files older than the current month to Zip archives in a given directory or in the IIS log directories and deletes the archived files.
Zip archives with the name ZipArchiveYYYY.zip are created in the log directories, where YYYY is the year of change of the archived file.
By default, only files with the extension ".log" are archived. This extension, the month, the archive name and recursive processing of subdirectories can be selected by parameters.

The script uses the built-in commandlet Compress-Archive to compress, so no additional tools are needed but Powershell V5 or up are required.

A regular start via scheduled tasks can be set up at a command prompt for example via (the path to the script has to be adjusted):

schtasks.exe /Create /TN "Archive IIS log files" /TR "Powershell.exe -NoProfile -Command \"^& 'C:\Work\Compress-LogDirectory.ps1' -IIS\"" /SC MONTHLY /D 15 /ST 21:15 /RU SYSTEM /RL HIGHEST /F
(I'm sad that Powershell commandlets do not support monthly triggers so you have to use cmd.exe)


Examples (assume Compress-LogDirectory.ps1 is in the current path):


.\Compress-LogFileDirectory.ps1 -Path "C:\LogFiles" -Filter "*.*" -MonthBack 3 -ArchiveName "zip"

Archives all files in directory C:\LogFiles which are 3 months older than the current month in the archives "zipYYYY.zip" (YYYY = year of change of the respective file).


.\Compress-LogFileDirectory.ps1 -IIS

Archives all files in IIS log directories older than the current month in the archives "ZipArchiveYYYY.zip" (YYYY = year of change of the respective file) in the log directories.
