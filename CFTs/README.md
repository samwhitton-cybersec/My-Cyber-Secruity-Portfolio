# Capture The Flag
The CTFs that I have participated in and what I have learnt from ctf related challenges

## PicoCTF
### Corrupted file - Forensics

🔍 Steps Taken

Dump the file to hex
- `xxd file > file.hex`

Open the hex dump for editing
- `nano file.hex`

Inspect the header bytes
Found this at the start of the file:
- `00000000: 5c78 ffe0 0010 4a46 4946 0001 0100 0001  \x....JFIF......`

The correct JPEG “magic number” (file signature) should begin with:
- `FF D8 FF E0`

The `5c78` (\x) prefix indicated escaped characters, likely causing corruption.

Fix the header
- Replaced `5c78 ffe0` with `ffd8 ffe0` in the hex dump.

Rebuild the binary file
- `xxd -r file.hex > file_new.jpeg`

Export the recovered file from the webshell
- `sz file_new.jpeg`

(The sz command uses ZMODEM transfer in the picoCTF webshell to download files to the host.)
Open the recovered image
The image displayed correctly.
The flag was visible in the image.

🧰 Tools Used

- `xxd` – for hex dumping and rebuilding
- `nano` – to edit the hex dump
- `sz` – to transfer the recovered file to the host
- `Image viewer` – to view the file and obtain the flag
