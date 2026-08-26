Part 1 – Upload a File to an FTP Server
Step 1: Locate the File
I opened PC-A and selected the Desktop tab.

I then opened the Command Prompt.

To see the available commands, I entered:

?

Next, I used the following command to display the files stored on the PC:

C:\> dir

The directory showed the file:

sampleFile.txt

The file size was 26 bytes.

This confirmed that the file I needed to upload was available on PC-A.

Step 2: Connect to the FTP Server
I connected to the FTP server by entering:

C:\> ftp 209.165.200.226

The connection was successful, and the FTP server displayed its welcome message.

I entered the username:

student

Then I entered the password:

class

After entering the correct credentials, I received the message that I was logged in successfully.

I was then presented with the FTP prompt:

ftp>

Step 3: View FTP Commands
At the FTP prompt, I entered:

ftp> ?

This displayed the available FTP commands.

Some of the commands I used in this lab included:

dir – displays files on the FTP server.
put – uploads a file.
get – downloads a file.
rename – changes a file name.
delete – removes a file.
quit – exits the FTP session.
Step 4: View Files on the FTP Server
I entered:

ftp> dir

The FTP server displayed a list of files stored on the server.

At this point, sampleFile.txt was not yet in the server's directory.

Step 5: Upload the File
I uploaded the file from PC-A by entering:

ftp> put sampleFile.txt

The FTP server showed that the file transfer was in progress.

The transfer completed successfully:

[Transfer complete – 26 bytes]

This confirmed that the file was successfully uploaded.

Step 6: Verify the Uploaded File
I used the dir command again:

ftp> dir

The server directory now contained:

sampleFile.txt

The file size was 26 bytes.

This confirmed that the upload was successful.

Part 2 – Download a File from the FTP Server
In this part, I renamed the uploaded file and then downloaded it back to PC-A.

Step 1: Rename the File
At the FTP prompt, I entered:

ftp> rename sampleFile.txt sampleFile_FTP.txt

The FTP server confirmed that the file was renamed successfully.

The original file name was:

sampleFile.txt

The new file name was:

sampleFile_FTP.txt

Step 2: Verify the New File Name
I entered:

ftp> dir

The directory listing showed:

sampleFile_FTP.txt

This confirmed that the file had been successfully renamed on the FTP server.

Step 3: Download the File
I downloaded the renamed file using:

ftp> get sampleFile_FTP.txt

The server started the file transfer.

The transfer completed successfully:

[Transfer complete – 26 bytes]

This confirmed that the file was downloaded from the FTP server to PC-A.

Step 4: Exit the FTP Client
I entered:

ftp> quit

The FTP client closed the connection to the server.

Step 5: Verify the Downloaded File
Back at the PC command prompt, I entered:

C:\> dir

The directory now showed two files:

sampleFile.txt
sampleFile_FTP.txt

Both files were 26 bytes.

This confirmed that the file had been successfully downloaded from the FTP server.

Part 3 – Delete the File from the FTP Server
Step 1: Connect to the FTP Server Again
I connected to the FTP server again using:

C:\> ftp 209.165.200.226

I entered the same login information:

Username: student
Password: class

After successfully logging in, I received the:

ftp>

prompt.

Step 2: Delete the File
I used the following command to remove the renamed file from the FTP server:

ftp> delete sampleFile_FTP.txt

The FTP server confirmed:

[Deleted file sampleFile_FTP.txt successfully]

The file was successfully removed from the server.

Step 3: Verify the File Was Deleted
I entered:

ftp> dir

The file sampleFile_FTP.txt was no longer listed in the FTP server directory.

This confirmed that the file had been successfully deleted.

Step 4: Exit the FTP Session
Finally, I entered:

ftp> quit

The FTP control connection was closed.

4. Important FTP Commands Used
Command	Purpose
ftp 209.165.200.226	Connects to the FTP server
dir	Displays files on the server
put sampleFile.txt	Uploads a file to the server
rename sampleFile.txt sampleFile_FTP.txt	Renames a file
get sampleFile_FTP.txt	Downloads a file from the server
delete sampleFile_FTP.txt	Deletes a file from the server
quit	Ends the FTP session
?	Displays available FTP commands

5. What I Learned
During this lab, I learned how FTP can be used to transfer files between a client and a server.

First, I located sampleFile.txt on PC-A and connected to the FTP server using the server's IP address. After logging in, I uploaded the file using the put command and verified that it appeared on the server.

I then renamed the file using the rename command and downloaded it back to the PC using the get command. Finally, I logged into the FTP server again and deleted the file using the delete command.

I also learned that FTP uses TCP, with port 21 used for the control connection and port 20 used for data transfer.
