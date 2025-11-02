# Capture The Flag
The CTFs that I have participated in and what I have learnt from ctf related challenges

## PicoCTF
### Corrupted file - Forensics

Identified that the unknown file was a JPEG file using `xxd` tool.
- Dump the file to hex: `xxd file > file.hex`

Edited the file using a text editor, I used `nano`
- Command: `nano file.hex`

Noticed that there was a `\x` in the file extension hex line:
- `00000000: 5c78 ffe0 0010 4a46 4946 0001 0100 0001  \x....JFIF......`
- Edited the first byte: `5c79 ffe0` to the full magic number for JPEG files `ffd8 ffe0`

Next rebuild the file.
- `xxd -r file.hex > file_new.jpeg`
