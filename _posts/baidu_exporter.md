---
title: Guide on Packaging and Import Baidu Exporter to Chrome
date: 2016-10-16

---

# TL;DR

It's been a loooooong time since the last update. Just cause I'm too lazy. X P

Chrome removed Baidu Exporter from Chrome App Store ~~due to some unknown Python transaction~~ recently. Due to security reason Chrome will disable extensions import locally with unknown source. You will get annoying popups every time launching Chrome if unpacked extensions are loaded.

So in this thread I'll provide a better solution to load Baidu Exporter with the latest build using Windows Group Policy. This solution inspired by [ungrown@Github](https://github.com/ungrown), thanks.

<escape><!-- more --></escape>

# Download the extension

Clone or download the latest copy of Baidu Exporter from [here](https://github.com/acgotaku/BaiduExporter).

# Package the extension

This step is unnecessary if you have the complied version.

1. Launch Chrome, open `chrome://extensions`, click `Pack extension` on top-left.

2. Browse the code you just downloaded, click `Pack Extension`.

3. The newly built extension will be found in the source folder with a `*.pem` file, **keep them all**, you will need that `.pem` file if you want to update the extension in the furture.

4. Drag the `*.crx` file to the `chrome://extension` page to install it. Select the `Developer Mode` checkbox to show the hidden extension ID, save it somewhere.

# Apply Chrome policy using Group Policy Editor

See [For MacOS Users](#last) if you are using **MacOS**.

1. Download the zip file of Chrome templates from [here](https://dl.google.com/dl/edgedl/chrome/policy/policy_templates.zip).

2. Extract the following files or folders into `%SystemRoot%\PolicyDefinitions`:
    * `./Windows/admx/chrome.admx`;
    * `./Windows/admx/google.admx`;
    * `./Windows/admx/en-US/`;
    * `./Windows/admx/zh-CN/`.


3. Press `Win+R` and run: `gpedit.msc`. A sub-folder named `Google / Google Chrome` can be found under `Local Computer Policy > Computer Configuration > Administrative Templates`. (Ps. The group policy editor is not embeded with starter and home editions. Follow [this](https://www.itechtics.com/enable-gpedit-windows-10-home/) guide to install it first. (Thanks @metafaniel for refering this issue.))

# Add the extension ID to whitelist

Add the extension ID by the following steps:

1. Navigate to `Administrative Templates / Google / Google Chrome / Extensions` section.

2. Double click to open `Configure extension installation whitelist` on the right side.

3. Enable the policy and click `Show...` to add the extension ID.

The extension will be enabled by default after Chrome relaunched.

<a id="last"></a>
# For MacOS Users

The solution for MacOS came from [tofuliang@Github](https://github.com/tofuliang), thanks.

1. Download the following policy template.

{% gist be3dd598289252698cd37bca04abd0fe com.google.Chrome.mobileconfig %}

2. Add the extension ID to line 19, delete  line 20 and 21 if you don't need it. Save.

3. Double click to import this policy.

4. **Reboot**.

---
# References

* [0.8.5在chrome商店被删 · Issue #277 · acgotaku/BaiduExporter](https://github.com/acgotaku/BaiduExporter/issues/277#issuecomment-253988038)
* [Tutorial: Getting Started - Google Chrome](https://developer.chrome.com/webstore/get_started_simple#step5)
* [Packaging - Google Chrome](https://developer.chrome.com/extensions/packaging)
* [Set Chrome policies for devices - Chrome for business and education Help](https://support.google.com/chrome/a/answer/187202?hl=en)