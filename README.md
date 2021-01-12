# CSSG

# Cobalt Strike Shellcode Generator  

Adds Shellcode - Shellcode Generator to the Cobalt Strike top menu bar

![Alt text](CSSG_gui.png?raw=true)  

CSSG is an aggressor and python script used to more easily generate and format beacon shellcode  

Generates beacon stageless shellcode with exposed exit method, additional formatting, encryption, encoding, compression, multiline output, etc  

**shellcode transforms are generally performed in descending menu order**  

---

**Requirements:**  
The optional AES encryption option uses a python script in the /assets folder  
Depends on the pycryptodome package to be installed to perform the AES encryption  

Install pycryptodome with pip depending on your python environment:  

    python -m pip install pycryptodome
    python3 -m pip install pycryptodome
    py -3 -m pip install pycryptodome
    py -2 -m pip install pycryptodome

You can check that pycryptodome is present after the pip install with a command like:  

    python -m pip list | grep crypto

The generator will use the system's default "python" command to launch the AES encryption script  

---

***Options for the shellcode generator are:***

**Listener:**  
Select a valid listener with the "..." button. Shellcode will be generated form this listener selection  

**Delivery:**  
Stageless (Staged not supported for the shellcode generator)  

**Exit Method:**  
process - exits the entire process that beacon is present in when the beacon is closed  
thread - exits only the thread in which beacon is running when the beacon is closed  

**Local Shellcode Checkbox:**  
May use if you are going to execute the shellcode from an existing Beacon  
Generates a Beacon shellcode payload that inherits key function pointers from a same-arch parent Beacon  

**Existing Session:**  
The parent Beacon session where the shellcode will pull session metadata  
Shellcode should be run from within this Beacon session  

**x86 Checkbox:**  
Check to generate x86 shellcode, x64 is generated by default  

**Or Use Shellcode File:**  
Use an externally generated raw shellcode file in lieu of generating Beacon shellcode  
This allows you to use previously exported shellcode files or output from other tools (Donut, msfvenom, etc)  

**Formatting:**  
raw - raw binary shellcode output, no formatting applied  
hex - hex formatted shellcode output  
0x90,0x90,0x90 - shellcode formatted into a C# style byte array  
\x90\x90\x90 - shellcode formatted into a C\C++ style byte array  
b64 - option to base64 encode the shellcode early in the generation process (before any encryption)  

**XOR Encrypt Shellcode Checkbox:**  
Check to XOR encrypt the shellcode (only one encryption type can be selected at a time)  

**XOR Key(s):**  
Randomly generated and editable XOR key character(s) to use for encryption  
Multiple characters will result in multiple rounds of XOR encryption (i.e. ABCD)  

**AES Encrypt Shellcode Checkbox:**  
Check to AES encrypt the shellcode (only one encryption type can be selected at a time)  
Uses a python script to perform AES Block Cipher AES-CBC encryption  
Shellcode is padded with \0 values to reach block size requirements  
A randomly generated IV is prepended to the encrypted shellcode data  

**AES Key:**  
Randomly generated and editable AES key to use for encryption  
32byte key is generated and preferred for 256bit encryption strength  
Encryption key byte lengths accepted are 16, 24, and 32  

**Encoding/Compression:**  
none - No additional encoding or compression is done to the shellcode  
b64 - base64 encode the shellcode  
gzip then b64 - gzip compress then base64 the shellcode  
gzip - gzip compress the shellcode  
b64 then gzip - base64 then gzip compress the shellcode  

**Multiline Output:**  
Can be used for non-raw/binary output formats  
none - no multiline formatting, shellcode is one long string  
quoted - Shellcode is broken up into lines surround by quotation marks  
chunks.push_back - Shellcode is broken up into lines surrounded by chunks.push_back(" and ");  

**Multiline Length:**  
Number of shellcode characters in each line if a multiline output option is selected  

**Generate Button:**  
Select directory for shellcode output  
Defalut filename will be beacon but can be changed  
Any encryption key used will be displayed in a popup and also written the Cobalt Strike Script Console  
The byte size of the raw beacon shellcode and final formatted beacon shellcode will be displayed in a popup and also written to the Script Console  
Location of files used to generate/build the shellcode are set the .cs file  
