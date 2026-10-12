# Installation

This page covers getting the tool running. Once you're set up, see the [User Guide](user-guide.md).

**Contents**

1. [Download](#1-download)
2. [Unblock the file](#2-unblock-the-file)
3. [Enable macros](#3-enable-macros)
4. [Set up the phrase library](#4-set-up-the-phrase-library)
5. [Open the tool](#5-open-the-tool)
6. [Updating](#updating)
7. [Troubleshooting](#troubleshooting)

---

## 1. Download

Download the latest archive `SDS Helper.zip` from the repository's [Releases](../../../releases) page. This contains the macro-enabled Word file `Template-SDS.dotm`, documentation and supporting data used by the application.

Once downloaded, extract the .zip archive.

> **Note:** Only use files from the official Releases page. Macro-enabled files can run code on your computer, so don't run copies from unknown sources.

## 2. Unblock the file

Since 2022, Microsoft Office blocks macros in files that were downloaded from the internet. If you skip this step, Word will show a red banner saying *"Microsoft has blocked macros from running because the source of this file is untrusted"* and the form won't work.

Choose **one** of the following.

### Option A: Unblock the individual file (recommended)

1. Make sure the file is **closed** in Word.
2. Right-click the file in File Explorer and choose **Properties**.
3. On the **General** tab, tick **Unblock** (near the bottom).
4. Click **OK**.

Alternatively, in PowerShell:

```powershell
Unblock-File -Path "C:\path\to\Template-SDS.dotm"
```

### Option B: Save the file to a Trusted Location

Files in a Trusted Location are not subject to the internet-download block.

1. Open Word and go to **File → Options → Trust Center → Trust Center Settings…**
2. Select **Trusted Locations** and click **Add new location…**
3. Choose the folder where you'll keep the tool, then click **OK**.
4. Save the downloaded file into that folder.

> **Tip:** if you can't see an **Unblock** option in the file's Properties, the file isn't flagged as downloaded. Macros may then be blocked by a Trust Center setting or by an IT policy. See [Troubleshooting](#troubleshooting) for further information.

## 3. Enable macros

When you first open the file, Word may show a yellow **Security Warning** bar. Click **Enable Content** to allow the macros to run.

Keep your global macro setting on **Disable all macros with notification**. Don't switch to *Enable all macros*, since that applies to every file you open.

## 4. Set up the phrase library

The tool reads its hazard (H, EUH) and precautionary (P) phrases from an Excel spreadsheet, `SDS Phrases.xlsx`, to populate the lists on the form. Because the phrases are read from the spreadsheet rather than built into the macro, wording or guidance changes only require editing the spreadsheet. An example spreadsheet has been included in this repositiory under `data/SDS Phrases.xlsx`.

The macros looks for `SDS Phrases.xlsx` in the `data` folder for where the template was opened. If this spreadsheet has changed location, a prompt will appear asking the user to locate `SDS Phrases.xlsx`.

## 5. Open the tool

Open the file in File Explorer as you would any other Word document. There is a **short delay** while it loads, after which the form appears.

## Updating

To update to a new version:

1. Check the release notes on the [Releases](../../../releases) page for changes.
2. Download the new file and unblock it (step 2 above).
3. Replace the old copy.
4. If the release notes mention a new phrase library, replace `SDS Phrases.xlsx` too.

## Troubleshooting

| Symptom | Likely cause | What to try |
| --- | --- | --- |
| Red banner: *"Microsoft has blocked macros from running…"* | The file is flagged as downloaded from the internet | [Unblock the file](#2-unblock-the-file) or move it to a Trusted Location, then reopen it |
| No **Unblock** checkbox in Properties | The file isn't flagged, so macros are being blocked for another reason | Check your Trust Center settings. If it's a work PC, an IT policy may block macros from internet-sourced files. Ask your IT team for help |
| Unblock has no effect | The file was open in Word when you changed it | Close the file, unblock it, and reopen it |
| Yellow **Security Warning** bar, and no form | Macros haven't been enabled for this file | Click **Enable Content** |
| The lists of hazard or precautionary statements are empty | The tool most likely can't find the phrases spreadsheet | Check the [phrase library setup](#4-set-up-the-phrase-library) |
| The file takes a few seconds to open | Normal. The template takes a moment to load | Wait for the form to appear |

Still stuck? [Open an issue](../../../issues) and include your Word version and a description of what you were doing and what you see.
