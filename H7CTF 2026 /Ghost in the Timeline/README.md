# Ghost in the Timeline 
I started by checking the file type:

```

file case_disk.img

```

The output identified an ext4 filesystem. This indicated that the image contained a Linux filesystem and could potentially be examined using filesystem-forensics tools.

Next, I searched for readable strings:
```
strings -a case_disk.img | less
```
Among the interesting entries were:

    q3_designs.zip

    notes.txt

    roadmap.pdf

    auth.log

The ZIP archive was particularly interesting because archives can contain additional files or information that is not immediately visible during a basic inspection.
I searched the raw image for the ZIP local-file signature:
```
grep -oba $'PK\x03\x04' case_disk.img
```
ZIP archives commonly use the byte signature PK\x03\x04 at the beginning of a local file entry.

The relevant archive began at byte offset 1538048.

I extracted the identified ZIP region into a separate file:
```
dd if=case_disk.img \
   of=carved.zip \
   bs=1 \
   skip=1538048 \
   count=3477 \
   status=progress
```
I then checked the extracted archive:
```
file carved.zip
unzip -l carved.zip
```
The archive contained a file named secret.txt.

I extracted the file:
```
unzip carved.zip
```
Then inspected its contents:
```
cat secret.txt
```
The file contained an exfiltration manifest and a recovery token.

Flag found:
```
H7CTF{e211b7db9d4f5c9f0812}
```
