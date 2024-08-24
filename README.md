# Password Cracking
## Overview
This repository showcases how to use powerful tools for password cracking, specifically John the Ripper (JTR) and Hashcat. Here, you’ll find information on cracking passwords for various encrypted document types, including PDFs and Office files, as well as some insight into additional tools used in the process.

## Tools and Methods
### 1. John the Ripper (JTR):
* Benefits: JTR is an incredibly versatile and powerful password cracking tool. It excels at using brute force, wordlists, and masks to crack passwords for a variety of encrypted file types, including PDFs and Office documents. The ability to handle different hashing algorithms and attack methods makes JTR a go-to for many cybersecurity professionals.
* Efficiency: When used with masks, JTR can quickly and effectively test password patterns, making it a great choice for both short and complex passwords.

### 2. Hashcat:
*  Benefits: Known for its high performance and support for multiple hashing algorithms, Hashcat is ideal for brute force attacks. Its optimized kernels and extensive options for different attack modes (like mask attacks) make it a powerful tool for cracking hashes.
* Efficiency: Hashcat’s ability to leverage GPU acceleration provides significant speed advantages, especially for longer passwords.

### 3. pdfrip:
* Benefits: While pdfrip specializes in extracting hashes from PDF files, it's particularly useful for handling specific password patterns such as numeric and date-based. It’s a valuable tool when dealing with PDFs but not as versatile for other document types.
* Usage: Best used when dealing with PDFs and specific password patterns.

## How Password Cracking Works
Password-cracking tools operate by deciphering hashed values, which are encrypted representations of passwords. Here’s a brief explanation of how they work:
1. **Hash Extraction:** Tools like John the Ripper, Hashcat, or pdfrip first extract the hash from the encrypted file. For PDFs, this involves using specific utilities to generate a hash representation of the password protected by the encryption.
2. **Hash Cracking:** Once the hash is obtained, the tools use various methods to crack it. This includes:
    * Brute Force Systematically trying every possible combination of characters until the correct password is found.
    * Dictionary Attacks Testing passwords from a precompiled list of common or previously used passwords.
    * Mask Attacks Utilizing patterns or specific formats to reduce the search space and speed up the cracking process.
3. **Hash Comparison:** The tool compares the generated hashes of attempted passwords with the original hash extracted. When a match is found, it reveals the original password.

This process demonstrates the importance of using strong and complex passwords to prevent unauthorized access, as weak or predictable passwords are more easily compromised.
## Practical Implementation on Windows
Here’s a practical look at how these tools were used in my recent password cracking projects. 
For installing the required tools, you can refer to the following links:
* John the Ripper: [John the Ripper Download](https://www.openwall.com/john/)
* Wordlist (rockyou): [Rockyou Wordlist](https://github.com/brannondorsey/naive‐hashcat/releases/download/data/rockyou.txt)
* Hashcat: [Hashcat Download](https://hashcat.net/hashcat/)
* pdfrip: [pdfrip on GitHub](https://github.com/mufeedvh/pdfrip/releases)
* Python 2.7 : [Python2.7](https://www.python.org/download/releases/2.7/)
  
These links will guide you to the official sources where you can download and install each tool.
#### ►  Create a Password-Protected Word Document
* #### Create a Word document and set the password as "Password123" to protect it. This will be one of the target file for the password-cracking process.

<img src="https://github.com/user-attachments/assets/d2e626d0-4247-41d8-9440-624b66dcad18" alt="image" width="400" style="display:inline-block;"/>
<img src="https://github.com/user-attachments/assets/955d29be-bc5e-4bfc-8e3b-3fb51008f112" alt="image" width="700" style="display:inline-block;"/>

#### ►  Execute John the Ripper Command
* ### Navigate to the directory where John the Ripper is installed:
  ```
  cd /path/to/john-the-ripper/run
  ```
* #### Execute the following command to create a hash file from the protected DOCX document:
```
  office2john.py /path/to/protected_file.docx > hash_file.txt
```
```
  john --wordlist=/path/to/rockyou.txt hash_file.txt
```
office2john.py protected_file.docx > hash_file.txt
Next, use the wordlist (e.g., rockyou.txt) to crack the password:

bash
Copy code
john --wordlist=/path/to/rockyou.txt hash_file.txt
This will initiate the cracking process using the provided wordlist to find the password for the DOCX file.
<img src="https://github.com/user-attachments/assets/6b7abfc5-6324-458c-9ac4-44b32f6b7aec" alt="image" width="800"/>


Application and Benefits
In this work, I used these tools to crack passwords on various encrypted documents, including Word, Excel, and PowerPoint files. Key techniques included brute force and mask attacks to effectively tackle different password complexities.
### Similar Tools
* Cain and Abel: Password recovery and cracking for various hash types.
* Hydra: Fast brute-force tool for network login cracking.
* Aircrack-ng: Focuses on WiFi password cracking and network security.
* L0ph: Specializes in password cracking with various techniques.
* CrackStation: Online tool for cracking hashed passwords with large wordlists.
