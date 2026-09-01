# Parrot OS Live USB 
<img width="1672" height="941" alt="643866830-9398b3df-a39c-427c-8de1-c64df897e752" src="https://github.com/user-attachments/assets/a2149259-3c81-46d6-b78e-b838f03e6a9a" />

# With Encrypted Persistence, and Nuke Password

Want to turn any computer into a hacking machine in just minutes?

I’ll show you exactly how to install Parrot OS onto a USB stick, complete with Encrypted persistence and Nuke Password if you want maximum stealth and security.

You’ll learn how to create a fully portable persistent Parrot OS setup that keeps your files, tools, and configurations even after a reboot.

Perfect for cyber security, pentesting, and forensic work on the go.

Okay, so I’m going to show you how to install Parrot OS onto a USB stick. This is what is known as a live USB, and we’re going to set up persistence.

Then we’re going to go a little bit further and add encrypted persistence to our Parrot OS live USB drive.

Finally, we’re going to configure a Nuke password.

## Step 1: Download Parrot OS

First, head over to the Parrot OS homepage:

https://www.parrotsec.org

Click on Download.

Then click on Security Edition.

This is the full version of the operating system that can be run from a removable storage device.

## Step 2: Flash the Image to the USB

Now we can move on to actually flashing the image to our USB stick.

There are multiple ways that you can do this.

You can use DD, Etcher, Make USB, Rufus, and other methods.

I’m choosing to use Balena Etcher.

I already have Balena Etcher on my machine.

If you don’t have it, go to:

https://etcher.balena.io

Click on Download Etcher.

The AppImage makes it very simple. You don’t even technically have to do an installation. You can just run it as is.

It’ll open up the GUI.

Click on Flash from file.

Locate the Parrot OS image that you just downloaded and double-click on it.

Next, select the target.

Insert your USB stick.

Make sure you select the correct USB stick. You do not want to accidentally erase one of your system drives.

Click Select.

Finally, click Flash.

Wait for the flashing process to complete.

Once the flashing has completed, close Balena Etcher.

## Step 3

If you are on windows follow this step if you are on Linux you can skip it. To configure the persistence you need bash terminal and to do that we are going to boot into the usb and use the bash from there to configure the persistence and everything so first thing you open powershell on windows as Admin and you type this command

```powershell
shutdown /r /fw /ts 0
```

and press enter, this command will reboot the computer and enter the bios automatically and inside the bios you need to go to boot settings and make the usb is the first bootable drive on the list and then save and exit or on some motherboards
you can press F8 and choose the usb directly from there and boot into it

**Note!!!!!!:** you need to turn off secure boot before booting into the USB

after we are booted we choose Try and install and press enter then we will boot into parrot desktop live from there we open the terminal and follow the next steps.

## Step 4: Identify the USB Device

Now we’re going to configure persistence.

Run:

```bash
lsblk
```

This is so that you can get the proper device label of the USB stick.

It’s very important that you find the correct name.

On my system, the USB stick is recognized as sda.

In other words:

/dev/sda

The system does not automount anything that you plug in, so you should not see anything under the mount points.

You can see that we have two partitions:

sda1
sda2

We’re going to create a third partition.

That third partition is going to be our persistence partition.

Keep in mind that yours might not be sda.

It could be sda, sdb, or sdc.

Make sure that you have the correct device label.

## Step 5: Create the Persistence Partition


Now we’re going to create the new partition inside the empty space above our current live partitions by typing.

```bash
sudo fdisk /dev/sda <<< $(printf "p\nn\np\n\n\n\np\nw")
```

Once that completes, run:

```bash
lsblk
```

You should now see a third partition:

/dev/sda3

## Step 6: Encrypt that partition

Now we will encrypt this partition, and we are going to do that using LUKS. So we're going to run the command

```bash
sudo cryptsetup --verbose --verify-passphrase luksFormat /dev/sda3
```
(((Once again, it might be different for you. It might be /dev/sdb3 or /dev/sdc3, but it should definitely have a three at the end)))


now you see that this will overwrite all the data on this partition and you type

```
YES
```

in all capital


And now we have to enter a passphrase. We need to create that passphrase right now. You want to make your passphrase strong and unique, and you want to make sure you remember this because this is how you are going to access the encrypted partition on this USB drive.

Now we're going to open the encrypted partition that we just created by running the command:

```bash
sudo cryptsetup luksOpen /dev/sda3 my_usb
```

We have to enter the passphrase that we just created.

So now that the encrypted partition is open, we're going to create a file system inside of it and give it a label.
We're going to run the command:

```bash
sudo mkfs.ext4 -L persistence /dev/mapper/my_usb
```

Once this command has completed, we can move on to the next step, and that is going to be to mount the partition and create the persistence.conf file, which is a configuration file, and that will allow the changes to persist across reboots.
We do this by running the command :

```bash
sudo mkdir -pv /mnt/my_usb
```

Next, we will mount the partition by running:

```bash
sudo mount -v /dev/mapper/my_usb /mnt/my_usb
```

Now we're going to create the persistence.conf configuration file by running the command:

```bash
echo "/ union" | sudo tee /mnt/my_usb/persistence.conf
```

You should get this line as your return ( / union ).

And finally, we're going to unmount the mounted file system by running the command:

```bash
sudo umount -v /mnt/my_usb
```

The last thing that we need to do is close the encrypted partition by running the command:

```bash
sudo cryptsetup luksClose /dev/mapper/my_usb
```

If everything has been done correctly, we should now be able to boot into the live USB encrypted persistence mode.
Reboot the PC now and boot into the USB and once you booted you are going to go down to advanced options and then encrypted persistence and hit enter.

Now you can see we have our splash screen, and at the bottom it is asking us for the password.
We need to enter the password that we created previously to decrypt the encrypted partition
And from this point, you are only limited by your imagination.

Uh, now that we are in the live persistence drive we can create what is commonly referred to as a Nuke password
It's a little bit more complicated, but it is a wonderful feature to have. And this will allow us to insert an alternate password into that prompt so that if you are ever in a compromising situation and somebody is attempting to force you to decrypt your drive, you have the option of entering your nuke password and it will render those key slots useless. It will render all of the data on that encrypted partition useless and make it inaccessible.

So, how do we do this? You have to have a certain package installed on Parrot OS Security Edition.
It is already installed by default. That package is called ```cryptsetup-nuke-password```. If I do an apt search for that, we get back that it is used to erase the Luks keys with a special password on the unlocked prompt. And you see over here that it is already installed. So you don't need to make a connection to the internet.

you're definitely going to want to first back up your Lux key slots and encrypt them and save them in a separate place, a safe place. So in order to do that, I'm going to have to get a second USB stick other than the one that we are using because we are running the system from this one and you don't want to use that one.
So, I'm going to grab a separate USB stick. And this is simply to save the backed up encrypted key slot too and get it off the machine.

plug the 2nd USB and open the terminal, now If I do an lsbk, it looks like mine it's being recognized as sdb and sdb1, it might be different for you!.
And it is not mounted. So, we will have to mount that momentarily.
But first, we're going to run the command:

```bash
sudo dpkg-reconfigure cryptsetup-nuke-password
```

You are brought to end cursesbased prompt and it explains the whole process to you. I'll hit tab until I see okay is highlighted and then hit enter. It's going to ask us to create our nuke password. You want to make sure this password is different than the password that you're using to decrypt the encrypted partition. Otherwise, you can have a big problem.

After the command has been completed successfully now have our Nuke password. YEAH
But this is very important. We now need to back up the Luks key slots and we're obviously going to want to encrypt those.
So, we're using a lot of passwords now, you probably at this point should be considering a password manager or a safe place to keep all of these passwords cuz they all should be different from one another.
So to back up and encrypt the key slots, we're going to start with the command:

```bash
lsblk

sudo cryptsetup luksHeaderBackup --header-backup-file luksheader.backup /dev/sda3
```

Note! quickly double check and make sure that you are using the correct location. (Once again, it might be different for you. It might be sdb3 or sdc3)

Now if I type ls, we will find our backup file luksheader.backup.

The next thing is going to be to encrypt it. We're going to do that by running the command:

```bash
sudo openssl enc -e -aes-256-cbc -in luksheader.backup -out luksheader.backup.enc
```

All right. So, at this point, we have to enter our third password. So, make sure that you are storing these passwords in a safe place and keeping track of them. We have our first password, which is for decryptting the encrypted partition of the USB drive. Our second one was the Nuke password. And now, this one is a password to encrypt our key slots.

After you set your password you do get a warning that there is a deprecated key derivation used. Do not worry about that. Now we should have two files, one encrypted, one not.
So now if you run ``` ls -lh ```we have two different files. The first file is our our backup. The second one is the encrypted version of that backup.

So now that we have that done, we are going to permanently delete from the universe our original unencrypted backup key slots.
We're going to do that by using shred by the following command:

```bash
sudo shred -v luksheader.backup

sudo rm luksheader.backup
```

And there we go. So now with our encrypted backup key slots, we're going to want to remove them from this machine and store them in a safe place. Why do we want to do that? We want to do that because if you do not have access to them in a place outside of the machine that you are running this on, how are you ever going to get access to those key slots to restore them?
I am going to go ahead and move that encrypted backup over to my removable storage.
First I'm going to mount the 2nd USB by running the command:

```bash
sudo mount /dev/sdb1 /media
```

and we are going to move our encrypted luks key into the USB by running the command:

```bash
sudo mv luksheader.backup.enc /media
```

Now we are going to test and learn how we going to use that key by rebooting the machine and going to boot into Parrot OS and we want to choose the encrypted persistence option inside of the advanced modes.

And once we find ourselves back at the prompt where we are asked to enter our password, instead of entering the normal password that would decrypt the encrypted partition, we will enter our Nuke password.

And don't expect much when you do this. You're not going to get some popup message on your screen or flashy things. You are actually not going to see anything different at all. But underneath the hood, what should be taking place is that that partition is now going to be useless. So from this point forward, when you attempt to enter your decryption password, it should have no effect.

And there's just so many different use cases for this. You know, you are traveling and you have to go through airport security. Or you're over at your ex-girlfriend's house and you think she might be setting you up or something crazy you know XD. There are just so many different use cases for this and all you have to do is enter that nuke password and you are now guaranteed that nobody is going to get access to anything that was residing on that encrypted partition. And the most beautiful part is that once you have retrieved your encrypted backed up key slots, all you have to do is restore them to the device and now you can have access to the encrypted partition again.

To restore the encrypted partition boot into the USB just click on try or install. Or in other words, we do not have to go inside of advanced modes and open up persistence or encrypted persistence. In fact, we're not able to open up encrypted persistence at the moment. So we're just going to click on try or install. That is going to essentially boot us into what is typically referred to as a live boot.

After you boot into the Desktop open the Terminal and type:

```bash
lsblk
```

for this particular machine for this USB stick. The encrypted partition is sitting on dev sda3

Now we are going to have to retrieve our encrypted backed up key slots. If you remember from previously we backed up those key slots. We encrypted them and we copied them over to a separate USB stick.
plug the USB stick and run the command:

```bash
lsblk
```

we see that that USB stick is sitting on sdb, specifically sdb1, and it is not mounted. So, let us go ahead and quickly mount that by running:

```bash
sudo mount /dev/sdb1 /media
```

Now I should be able to run ```ls``` on /media and see everything on my USB stick.
Let us now first go ahead and copy the headers over to the machine and i will do that by running:

```bash
sudo cp /media/luksheader.backup.enc /home/live
```

( or if you are already in the home directory ~ just type . instead of /home/live )

and just to get rid of this USB stick situation now type the command:

```bash
sudo umount /media
```

So now what we have to do is we have to decrypt the headers. Remember we encrypted it with a completely different password for extra protection. So we are going to enter in a very long command that is going to decrypt our encrypted backup header by typing:

```bash
sudo openssl enc -d -aes-256-cbc -in luksheader.backup.enc -out luksheader.backup
```

So now if we do an ```ls```, we have our backed up luks header file, and the next thing to do is going to be to restore that luks header back to that partition that we removed it from and that partition for me is sda3. This could be different for you remember that, we're going to run the command:

```bash
sudo cryptsetup luksHeaderRestore --header-backup-file luksheader.backup /dev/sda3
```

Actually what you should be getting is a prompt asking you to type in ```YES``` in all capital letters

And the only thing that we need to do is now shut this down and reboot and attempt to boot back into the encrypted persistence to make sure everything is working as it should.

And YES that is it now you restored everything and you are ready to continue from where you stopped before entering the Nuke Password.
I hope you learn something new from this and thank you for reading

And I'm just going to end with this. Encryption is the thing that probably best protects our privacy so encrypt everything. Protect yourself. Protect your privacy. And dont forget to backup everything offline on removable storage 
