---
title: Windows 10 2004 update failure diagnosis (the proper way)

date: 2020-06-15 18:30:00

---

这篇文章记录了 Windows 10 升级至 2004 版本时进度长时间卡在 61% 的排查思路和解决办法。

<escape><!-- more --></escape>

While Windows 10 updating from version 1909 to 2004, the progress stuck(,hang, freeze) at 61%, which is a [known issue](https://docs.microsoft.com/en-us/windows/release-information/status-windows-10-2004) related to Conexant ISST audio drivers.

But in my case, I don't have this driver in my system. And the Microsoft Community Forum just provides random guesses or solutions as usual, such as unplug some external devices or do a [system check](https://support.microsoft.com/en-gb/help/929833/use-the-system-file-checker-tool-to-repair-missing-or-corrupted-system). 

Finally, here is the proper way to diagnose the issue during Windows update I found: [Resolve Windows 10 upgrade errors - Windows IT Pro - Windows Deployment | Microsoft Docs](https://docs.microsoft.com/en-us/windows/deployment/upgrade/resolve-windows-10-upgrade-errors)

1. Download SetupDiag tool from [SetupDiag - Windows Deployment](https://docs.microsoft.com/en-us/windows/deployment/upgrade/setupdiag), which is a tool to collect and analyze the logs from Windows Update.
2. Excute the `SetupDiag.exe`, two files will be generated in the same path, which are `SetupDiagResults.log` and `Logs.zip`.
3. In my case, `SetupDiagResults.log` said *SetupDiag was unable to match to any known failure signatures*, which works *properly* because the update just stuck at 61% without any error report.
4. According to [Log files - Windows IT Pro - Windows Deployment](https://docs.microsoft.com/en-us/windows/deployment/upgrade/log-files), the issue happened at Down-Level, and the log for it is setupact.log, which is collected into `Logs.zip`. And here are the last serval lines of my log:

```
2020-06-13 19:59:05, Info                  MIG    AddDriverFiles: Processing driver: Mobile Intel(R) Processor Family I/O PCI Express Root Port #9 - 9D18, INTEL, INTEL
2020-06-13 19:59:05, Info                  MIG    AddInfAndCatalog: Adding catalog file: C:\WINDOWS\system32\catroot\{f750e6c3-38ee-11d1-85e5-00c04fc295ee}\oem120.cat
2020-06-13 19:59:05, Info                  MIG    DumpDeviceDriversCallback: Adding file: C:\WINDOWS\system32\DRIVERS\pci.sys
2020-06-13 19:59:05, Info                  MIG    AddDriverFiles: Processing device: 4d36e96c-e325-11ce-bfc1-08002be10318
2020-06-13 19:59:05, Info                  MIG    AddDriverFiles: Processing driver: HP Dock Audio, Synaptics, Synaptics
2020-06-13 19:59:05, Info                  MIG    AddInfAndCatalog: Adding catalog file: C:\WINDOWS\system32\catroot\{f750e6c3-38ee-11d1-85e5-00c04fc295ee}\oem26.cat
2020-06-13 20:00:58, Info                  MOUPG  CInstallUI::ShowMessageBox: Showing MessageBox
2020-06-13 20:01:00, Info                  MOUPG  CInstallUI::ConfirmCanceled: User cancel confirmed
2020-06-13 20:01:00, Info                  MOUPG  CInstallUI::OnProgressChanged: Cancel is requested. Returning ERROR_REQUEST_ABORTED
2020-06-13 20:01:00, Error                 MOUPG  CInstallUI::OnProgressChanged(575): Result = 0x800704D3
2020-06-13 20:01:00, Error                 MOUPG  CSetupUIManager::OnProgressChanged(378): Result = 0x800704D3
2020-06-13 20:01:00, Error                 MOUPG  CSetupHost::OnProgressChanged(2306): Result = 0x800704D3
2020-06-13 20:01:00, Error                 MOUPG  CSetupManager::DlpManagerCallback(2063): Result = 0x800704D3
2020-06-13 20:01:00, Info                  MOUPG  Cancel of current task requested...
2020-06-13 20:01:00, Info                  MOUPG  Attempting to cancel current task...
2020-06-13 20:01:00, Info                  MOUPG  MoSetupPlatform: Calling SetupPlatform::INewSystem::RequestCancelOperations...
2020-06-13 20:01:00, Info                  MOUPG  Task cancel request returned: [0x0]
2020-06-13 20:01:00, Error                 MOUPG  SendCallbackMessage: [0x7] -> user callback returned 0x800704D3
2020-06-13 20:01:00, Error                 MOUPG  CDlpTask::Cancel(984): Result = 0xC1800108
2020-06-13 20:01:00, Info                  MOUPG  SendCallbackMessage: [0x7] -> Cancel request returned 0xC1800108
```

As the log shown above, the progress hangs at 19:59:05, which is **Processing driver: HP Dock Audio, Synaptics, Synaptics**. I do connect a HP Thunderbolt 3 dock to my ThinkPad X1 Tablet 3rd Gen. So I disconnected it, uninstalled the device and driver for it, reboot and the update works again as I expected.

PS. I've tried update the system using Windows 10 2004 MSDN image, it stuck at 31% due to the same issue. The proper way to fix this is shown above.

E.O.F.