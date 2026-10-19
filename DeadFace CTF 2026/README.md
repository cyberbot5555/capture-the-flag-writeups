# DeadFace CTF 2026 - Mobile Challenge Writeup

📄 **A detailed PDF version of this writeup is available here: [Writeup PDF](./writeup.pdf)** 
*(Note: Rename your uploaded PDF file to `writeup.pdf` or update this link accordingly)*

## Challenge Information

| Challenge Name | Locked... or Not? |
| :--- | :--- |
| **Category** | Mobile |
| **Points** | 150 |
| **Difficulty** | Easy |
| **Author** | Md Solayman Hossain Shawon (CYB3R_BOT) |
| **Date Solved** | 19-10-2026 |
| **Status** | Solved |

> [!NOTE]
> **Executive Summary**
> The "Locked... or Not?" challenge required analyzing an Android application to find a hidden flag. The investigation began by inspecting the provided `df-securenotes.apk.zip` archive. After extracting the APK file, it was opened using **JADX-GUI** to examine the decompiled source code. During the analysis of the `MainActivity`, a Base64-encoded string containing the flag was discovered. Decoding this string revealed the final flag. This challenge demonstrates how static analysis can uncover sensitive information embedded directly within an application's source code.

## Objective

The primary goal was to analyze the provided Android application using static analysis techniques, identify the Base64-encoded string in the `MainActivity`, and decode it to retrieve the challenge flag.

## Tools Used

| Tool | Purpose |
| :--- | :--- |
| `unzip` | Used to inspect the APK archive contents and extract the APK file. |
| `jadx-gui` | A Dex to Java decompiler used to inspect the application's source code. |
| `base64` | A command-line utility used to decode the identified Base64-encoded string. |
| Kali Linux | The operating system used for the analysis. |

## Methodology & Step-by-Step Walkthrough

### Step 1: Inspect the APK Archive
First, I extracted the APK file from the provided ZIP archive using the `unzip` command.

```bash
unzip df-securenotes.apk.zip
