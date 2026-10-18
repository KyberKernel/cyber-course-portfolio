
# steganography

<img width="1600" height="347" alt="image" src="https://github.com/user-attachments/assets/8f0da34b-f7e5-4d06-80ee-4c0e586b51bd" />

## Task 1: hide a sentence, delete the file, get it back

I started from cat2.jpg and made two copies of it: cover.jpg, which became the cover image, and clean_copy.jpg, which I left alone so I'd have an untouched version to compare against later. Then I typed the sentence into secret.txt and embedded it into cover.jpg with steghide, using the passphrase KO_KYBER45_25D. After that I deleted secret.txt. At that point the image was the only place the message existed, so I extracted it again.

<img width="1600" height="347" alt="image" src="https://github.com/user-attachments/assets/dc3a1067-c5cc-4511-8a17-54698afc270e" />

The extracted text was:

```
Hello, this is a secret message!
```

cover.jpg and clean_copy.jpg had the same hash before the embed. After it, cover.jpg had a new hash and clean_copy.jpg kept the old one. The hashes differ. steghide info listed secret.txt as encrypted and compressed, 33 bytes.

## Task 2: find the cat image with a message in it

Two cat photos, cat1.jpg and cat2.jpg, and the passphrase Varia123. They look identical.

<img width="1500" height="495" alt="image" src="https://github.com/user-attachments/assets/094d2ef3-9a93-4151-bdb6-b56de5e81157" />

I ran steghide info on both files with the passphrase. cat1.jpg showed a hidden file:

```
"cat1.jpg":
  format: jpeg
  capacity: 113.5 KB
  embedded file "secret.txt":
    size: 26.0 Byte
    encrypted: rijndael-128, cbc
    compressed: yes
```

cat2.jpg showed only the capacity. Extracting from cat1.jpg gave me this:

```
This is a secret message!
```

The same command on cat2.jpg failed:

```
steghide: could not extract any data with that passphrase!
```

<img width="1600" height="347" alt="image" src="https://github.com/user-attachments/assets/7249af25-4897-46e3-bc7a-9171965e2ad7" />

## Task 3: hide the spreadsheet in an audio file

I made a WAV file called office_ambience.wav to use as the cover, since an audio file attached to an email or upload draws less attention than a spreadsheet would. I embedded the workbook into it with steghide, using the passphrase KO_KYBER45_25D, deleted the loose spreadsheet and pulled it back out of the audio. The exercise was set up as an authorized penetration test.

```
steghide embed -cf office_ambience.wav -ef TechNova_Solutions.xlsx -p KO_KYBER45_25D
```

<img width="1600" height="347" alt="image" src="https://github.com/user-attachments/assets/25ea5f8a-a749-4a1d-86d7-8370fe299a46" />

steghide info on the WAV showed this:

```
format: wave audio, PCM encoding
embedded file "TechNova_Solutions.xlsx": size 6.5 KB
encrypted: rijndael-128, cbc
compressed: yes
```

SHA-256 of the original workbook and of the one extracted from the audio:

```
492e22467b96f9c0cc05f09b7ad37350d018b2815e0e8266d05696624d1d82c7  original.xlsx
492e22467b96f9c0cc05f09b7ad37350d018b2815e0e8266d05696624d1d82c7  extracted/TechNova_Solutions.xlsx
```

cmp found no differences either.
