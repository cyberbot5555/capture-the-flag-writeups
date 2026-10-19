DeadFace CTF 2026 - Mobile Challenge Writeup
This repository contains the writeup for the Locked... or Not? mobile challenge from DeadFace CTF 2026.

📄 A detailed PDF version of this writeup is available here: Writeup PDF (Note: Rename your PDF file to writeup.pdf or update this link accordingly)

Challenge Information
Challenge Name	Locked... or Not?
Category	Mobile
Points	150
Difficulty	Easy
Author	Md Solayman Hossain Shawon (CYB3R_BOT)
Date Solved	19-10-2026
Status	Solved
Executive Summary
The "Locked... or Not?" challenge required analyzing an Android application to find a hidden flag. The investigation began by inspecting the provided df-securenotes.apk.zip archive. After extracting the APK file, it was opened using JADX-GUI to examine the decompiled source code. During the analysis of the MainActivity, a Base64-encoded string containing the flag was discovered. Decoding this string revealed the final flag. This challenge demonstrates how static analysis can uncover sensitive information embedded directly within an application's source code.

Objective
The primary goal was to analyze the provided Android application using static analysis techniques, identify the Base64-encoded string in the MainActivity, and decode it to retrieve the challenge flag.

Tools Used
Tool	Purpose
unzip	Used to inspect the APK archive contents and extract the APK file.
jadx-gui	A Dex to Java decompiler used to inspect the application's source code.
base64	A command-line utility used to decode the identified Base64-encoded string.
Kali Linux	The operating system used for the analysis.
Methodology & Step-by-Step Walkthrough
Step 1: Inspect the APK Archive
First, I extracted the APK file from the provided ZIP archive using the unzip command.

bash
unzip df-securenotes.apk.zip
Step 2: Analyze the Application Using JADX-GUI
I opened the extracted APK in JADX-GUI to decompile the application and inspect its source code.

bash
jadx-gui df-securenotes.apk
Step 3: Identify the Base64-Encoded Flag
Navigating through the decompiled source, I inspected the MainActivity.java file. Inside a method for a "secure backup", I found a hardcoded Base64 string:

java
private String getSecureBackupText() {
    byte[] decodedBytes = Base64.decode("ZGVhZGZhY2V7ZXotbW9iaWxILXRvLXNOYXJOfQ==", 0);
    return new String(decodedBytes, StandardCharsets.UTF_8);
}
Step 4: Decode the Flag
I used the base64 command in the terminal to decode the string.

bash
echo 'ZGVhZGZhY2V7ZXotbW9iaWxILXRvLXNOYXJOfQ==' | base64 -d
The output revealed the flag.

Flag
text
deadface{ez-mobile-to-start}
Lessons Learned
Static Analysis is Powerful: Tools like JADX-GUI can easily decompile Android applications to reveal hardcoded strings, credentials, and other sensitive information.

Encoding ≠ Encryption: Base64 is an encoding scheme for representing binary data as text, not a security mechanism. It can be decoded by anyone and should never be used to protect secrets.

Client-Side is Not Safe: Sensitive information such as API keys, passwords, or flags should never be stored directly in client-side application code, as it can be extracted by an attacker.

Remediation
Avoid Hardcoding Secrets: Never embed sensitive data like passwords or API keys directly in the source code.

Use Proper Encryption: If sensitive data must be stored on the client, use strong, industry-standard encryption with secure key management.

Store Secrets Server-Side: Keep sensitive information and business logic on a trusted server. Enforce authentication and authorization there, not on the client.

Integrate Security Checks: Use static analysis and secret-scanning tools in your CI/CD pipeline to catch hardcoded secrets before they are released.

References
JADX - Dex to Java Decompiler

Android Developers - App Manifest Overview

RFC 4648 - The Base16, Base32, and Base64 Data Encodings
