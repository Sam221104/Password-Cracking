# Password Cracking
## Overview
This repository showcases how to use powerful tools for password cracking, specifically John the Ripper (JTR) and Hashcat. Here, you’ll find information on cracking passwords for various encrypted document types, including PDFs and Office files, as well as some insight into additional tools used in the process.

## Why It Matters:
Understanding password cracking isn’t just for hackers; it’s crucial for everyone concerned with cybersecurity. When passwords are weak or predictable, they can be easily compromised, leading to potential data breaches. By learning about password cracking techniques and tools, individuals can better understand the potential weaknesses in their security practices. This knowledge helps in creating stronger, more resilient passwords and implementing better security measures. For instance, understanding the effectiveness of brute force attacks, mask attacks, and the use of wordlists allows you to set up more complex and harder-to-crack passwords, thereby enhancing your overall data protection. Knowing how these tools work can help you set stronger passwords and protect your sensitive data more effectively.

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
### <code style="color : name_color">John the Ripper</code>

### Cracking a Word Document password 

#### ►  Create a Password-Protected Word Document
* #### Create a Word document and set the password as "Password123" to protect it. This will be one of the target file for the password-cracking process.

<img src="https://github.com/user-attachments/assets/d2e626d0-4247-41d8-9440-624b66dcad18" alt="image" width="700" />
<img src="https://github.com/user-attachments/assets/955d29be-bc5e-4bfc-8e3b-3fb51008f112" alt="image" width="700" />

#### ►  Execute John the Ripper Command
* #### Navigate to the directory where John the Ripper is installed:
  ```
  cd /path/to/john-the-ripper/run
  ```
* #### Execute the following command to create a hash file from the protected DOCX document:
   ```
  office2john.py /path/to/protected_file.docx > hash_file.txt
   ```
* #### Use the wordlist (e.g., rockyou.txt) to crack the password:
   ```
  john --wordlist=/path/to/rockyou.txt hash_file.txt
   ```
* This will initiate the cracking process using the provided wordlist to find the password for the DOCX file.
   <img src="https://github.com/user-attachments/assets/864aa02b-ac76-4a97-8c7e-1cf8e1d9566e" alt="image" width="800"/>

* #### To display the cracked password after running John the Ripper, use the following command:
   ```
   john --show hash_file.txt
   ```
   <img src="https://github.com/user-attachments/assets/8908f2d6-71ac-4b9a-8660-dfec3d05572c" alt="image" width="600"/>

### Cracking a PDF password 
#### ►  Create a Password-Protected PDF file
* #### Create a PDF and set the password as "Password123" to protect it. This will be one of the target file for the password-cracking process.
* #### Navigate to the directory where John the Ripper is installed:
  ```
  cd /path/to/john-the-ripper/run
  ```
* #### Use pdf2john to extract the hash from your PDF file. 
   ```
   perl pdf2john.pl "example.pdf" > pdf_hash.txt
   ```
* #### Use John the Ripper with a _wordlist_ to crack the password.
   ```
   john --wordlist=rockyou.txt pdf_hash.txt
   ```
* #### After John the Ripper has completed the cracking process, display the cracked password:
   ```
   john --show pdf_hash.txt
   ```
   <img src="https://github.com/user-attachments/assets/d108c50b-1ea1-45ca-823c-f3f127404d70" alt="image" width="650"/>

### Cracking a PDF password without _wordlist_
* Cracking a PDF password using John the Ripper with brute force only, without using a wordlist or mask, can be very time-consuming on low-end processors. This method tests all possible combinations without any pre-defined patterns or shortcuts. Without using a wordlist or a mask, the tool must try every conceivable password, which makes it a very time-consuming process, especially for long or complex passwords. The lack of pattern knowledge means that each attempt is random, significantly extending the time required to crack the password.
* #### Use pdf2john to extract the hash from your PDF file. 
   ```
   perl pdf2john.pl "example.pdf" > hash_pdf.txt
   ```
* #### Use the command below to crack the password by brute force:
   ```
   john --incremental=Aplha --min-length=8 --max-length=8 --format=pdf hash_pdf.txt
   ```
     <img src="https://github.com/user-attachments/assets/2df35874-6bbb-4760-96d9-01a69ec03c70" alt="image" width="730"/>
     
### Cracking a PDF password using masking
   Masking is a technique used in password cracking to specify patterns or structures of passwords. Unlike brute force attacks that try every possible combination, masking focuses on specific patterns or character types, which makes the cracking process more efficient.
   For instance, consider a PDF file encrypted with a password pattern like "SAMS2004". In this case, the mask would specify that the first character is 'S', the last character is '4', and the remaining characters are uppercase letters and digits. This method narrows down the possible combinations based on known or suspected patterns in the password, speeding up the cracking process and reducing the number of guesses required.
* #### Use pdf2john to extract the hash from your PDF file. 
   ```
   perl pdf2john.pl "example.pdf" > pdf_hash3.txt
   ```
* #### Use the command below to crack the password with masking:
   ```
   john --mask='S?u?u?u?d?d?d4' --format=pdf pdf_hash3.txt
   ```
   <img src="https://github.com/user-attachments/assets/97c847cb-1842-4e42-a099-25dce40a08e2" alt="image" width="730"/>
### <code style="color : name_color">Hashcat</code>
* #### Use pdf2john to extract the hash from your PDF file. 
   ```
   perl pdf2john.pl "example.pdf" > hash3.txt
   ```
* #### Use the command below to crack the password with masking:
   ```
   hashcat -m100 -a3 hash3.txt S?u?u?u?d?d?d?d
   ```
   * Mode Specification: -m100 sets the hash mode to SHA1, indicating the type of hash being cracked.
   * Attack Mode: -a3 selects the brute-force attack mode with masks.
   * Mask Explanation: S?u?u?u?d?d?d?d specifies the password pattern:
      * S - An uppercase letter.
      * ?u - Three additional uppercase letters.
      * ?d - Four digits.
* This approach narrows down the search space to match known or suspected patterns in the password, improving efficiency compared to a pure brute-force attack.

   <img src="https://github.com/user-attachments/assets/fce6ada1-a720-49d9-989b-15b590d8f12e" alt="image" width="730"/>
  <img src="https://github.com/user-attachments/assets/b5778976-2c0c-48b9-b81f-70246fc5e84b" alt="image" width="730"/>
### <code style="color : name_color">pdfRip</code>
#### Consider a file like crackme2.pdf, which is encrypted with a 6-digit numeric password. In this case, using pdfrip is advantageous because it specializes in cracking numeric passwords, including brute-force attacks on numeric sequences, dates, and specific queries.
* #### Use the command below to use numeric bruteforce to crack the password
   ```
   pdfrip --num-bruteforce 100000 999999 crackme2.pdf
   ```
   * --num-bruteforce: Specifies that pdfrip should use a numeric brute-force approach.
   * 100000: Sets the minimum password value in the range.
   * 999999: Sets the maximum password value in the range.
   * crackme2.pdf: The target file to be cracked.
     
  <img src="https://github.com/user-attachments/assets/8c596f13-bd8a-4887-83a7-832446037da9" alt="image" width="730"/>

## Similar Tools
* Cain and Abel: Password recovery and cracking for various hash types.
* Hydra: Fast brute-force tool for network login cracking.
* Aircrack-ng: Focuses on WiFi password cracking and network security.
* L0ph: Specializes in password cracking with various techniques.
* CrackStation: Online tool for cracking hashed passwords with large wordlists.
  
## Application and Benefits
* These tools offer a range of powerful methods for cracking passwords on encrypted documents, such as Word, Excel, and PowerPoint files. Here's a detailed look at their benefits and applications:
   * Brute Force Attacks: This method systematically tests all possible combinations of characters. It is effective for short passwords but can be time-consuming for longer ones. Brute force is useful when the password is unknown and no patterns or clues are available.
   * Mask Attacks: Masking allows for the specification of patterns in the password, such as defining certain characters or their positions. This approach significantly speeds up the cracking process compared to pure brute force, especially when you have some idea of the password structure. For example, if you know the password starts with a specific letter and ends with a digit, a mask attack can focus on that pattern, reducing the total number of combinations to test.
   * Wordlists and Masks: Combining wordlists and masks can enhance efficiency. Wordlists contain common passwords or variations, while masks define patterns within those passwords. Using both allows for the testing of known patterns and character combinations, making the attack more targeted and faster
