Download Link: https://assignmentchef.com/product/solved-ece-4122-6122-hmk-4-problem2
<br>
<strong><u>ECE 4122</u></strong><u> students</u> need to do Problem 1.   <strong><u>ECE 6122</u></strong><u> students</u> need to do Problem 2.

<strong><u>Notes:</u></strong>

You can write, debug and test your code locally on your personal computer.  <u>However, the code you</u> <u>submit must compile and run correctly on the PACE-ICE server</u>.

In this homework you will need to develop <strong><em><u>two</u></em></strong> executable programs.  One program for the server and one for the client.

<strong><u>Submitting the Assignment:</u></strong>

See Appendix C.




<u>Grading Rubric</u>

<strong>AUTOMATIC GRADING POINT DEDUCTIONS PER PROBLEM: </strong>

<table width="619">

 <tbody>

  <tr>

   <td width="154"><strong>Element </strong></td>

   <td width="192"><strong>Percentage Deduction </strong></td>

   <td width="272"><strong>Details </strong></td>

  </tr>

  <tr>

   <td width="154">Does Not Compile</td>

   <td width="192">40%</td>

   <td width="272">Code does not compile on PACE-ICE!</td>

  </tr>

  <tr>

   <td width="154">Does Not Match Output</td>

   <td width="192">10%-90%</td>

   <td width="272">The code compiles but does not produce correct outputs.</td>

  </tr>

  <tr>

   <td width="154">Clear Self-Documenting Coding Styles</td>

   <td width="192">10%-25%</td>

   <td width="272">This can include incorrect indentation, using unclear variable names, unclear/missing comments, or compiling with warnings. (See Appendix A)</td>

  </tr>

 </tbody>

</table>

<strong> </strong>

<strong>LATE POLICY </strong>

<table width="619">

 <tbody>

  <tr>

   <td width="154"><strong>Element </strong></td>

   <td width="102"><strong>Percentage Deduction </strong></td>

   <td width="363"><strong>Details </strong></td>

  </tr>

  <tr>

   <td width="154">Late Deduction Function</td>

   <td width="102">score –(20/24)*H</td>

   <td width="363"> H = number of hours (ceiling function) passed deadline  note : Sat/Sun count as one day; therefore H = 0.5*H<sub>weekend</sub></td>

  </tr>

 </tbody>

</table>




<h1>Problem #1 TCP Sockets</h1>

<em><u>Server-70 points</u></em><em>  </em>

Write a console program that takes as a <strong>command line argument</strong> the <strong>port number </strong>on which the <strong>TCP Server</strong> will listen for connection requests.  A separate thread shall be created to handle the data received from each remote client and the remote clients can continue to send and receive data on the connections until either the server or the client closes the connection.  The TCP server needs to maintain a list of all connected clients so that it can send out the appropriate messages. The TCP server needs to be able to receive data from clients without blocking the main application thread.  The program needs to respond to user input while handling socket communications at the same time.

<ul>

 <li>The program should continuously prompt the user for commands to execute like so:</li>

</ul>

<strong>Please enter command: 0</strong>     – prints to the console the last message received (if any)

<strong>Last Message: </strong><em>last message received</em>

<strong>Please enter command: 1</strong>     – prints to the console a list of all connected clients (ip address and port number) like the following:

Numer of Clients: 2 IP Address          Port localhost          51717 localhost          51718

<strong>Please enter command: q    </strong>– closes all sockets and terminates the program

<ul>

 <li>The data being sent back and forth will use the following packet structure:</li>

</ul>

struct tcpMessage

{

unsigned char nVersion;   unsigned char nType;   unsigned short nMsgLen;   char chMsg[1000];

};




The TCP server needs to have the following functionality for received messages:

<ul>

 <li>If <strong>nVersion</strong> is not equal to 1 then the message is ignored.</li>

</ul>




<ul>

 <li>If <strong>nType == 0</strong> then the message should be sent to all other connected clients exactly as received (but <u>not</u> the client that sent the message).</li>

</ul>




<ul>

 <li>If <strong>nType == 1</strong> then the message is <u>reversed</u> and sent back to <strong>only</strong> the client that sent the message.</li>

</ul>




<em><u>Client-30 points</u></em>

In order to test your server, write a console program that takes as a <strong>command line argument</strong> the <strong>IP Address</strong> and <strong>port number</strong> of the server as shown below:

<strong>./a.out localhost 51717 </strong>

The program should prompt the user for inputs and display any messages received.

Here are example user inputs:

<strong>Please enter command: v #</strong>                                the user enters a “v”, a space, and then a version number. This version number is now used in all new messages.

<strong>Please enter command: t #</strong> <strong>message string</strong>       the user enters a “t”, a space, and then a type number, followed by the message.  Be sure you are able to handle the spaces in the message string.

<strong>Please enter command: q</strong>                                  the user enters a “q” causes the socket to be closed and the program to terminate.




Any messages received from the server should be displayed as followed:

<strong>Received Msg Type:</strong> #<strong>; Msg: </strong><em>message received</em>

<h1>Problem #2 UDP Sockets</h1>

<em><u>UDP Server (60 points)</u></em>

Write a console program that takes as a <strong>command line argument</strong> the <strong>port number </strong>on which the UDP Server will receive messages.  The UDP server collects parts of a larger <strong>composite message</strong> from the clients.  The UDP server collects these message parts from different clients and assembles them in order, based on the <strong>lSeqNum</strong>.  The UDP server keeps a running list of all clients that have sent a message to it and will broadcast the composite message to all clients when commanded.  The UDP server needs to be able to receive data from clients without blocking the main application thread.  The program needs to respond to user input while handling socket communications at the same time.




The program should continuously prompt the user for commands to execute like so:

Please enter command: 0

Please enter command: 1

Please enter command: 2

Composite Msg:  <em>current composite message</em>




The data being sent back and forth will use the following packet structure:

struct udpMessage

{

unsigned char  nVersion;   unsigned char  nType;   unsigned short nMsgLen;   unsigned long  lSeqNum;   char chMsg[1000];

};




The UDP server needs to have the following functionality from the <strong>command prompt</strong>:

<ul>

 <li>If <strong>command</strong> == 0 the server immediately sends to all clients the current composite message and clears out the composite message.</li>

 <li>If <strong>command</strong> == 1 the server immediately clears out the composite message.</li>

 <li>If <strong>command</strong> == 2 the server immediately displays to the console the composite message but takes no other actions.</li>

</ul>







The UDP server needs to have the following functionality when <strong>receiving messages</strong>:

<ul>

 <li>If <strong>nVersion</strong> is not equal to 1 then the message is ignored.</li>

 <li>If <strong>nType == 0</strong> the composite message is immediately cleared and anything in the chMsg buffer is ignored.</li>

 <li>If <strong>nType == 1</strong> the composite message is immediately cleared and the message in chMsg is used as the start of a new composite message</li>

 <li>If <strong>nType == 2</strong> the message in chMsg is added to the composite message based on its <strong>lSeqNum</strong></li>

 <li>If <strong>nType == 3</strong> the server immediately sends to all clients the current composite message and clears out the composite message.</li>

</ul>




If the composite message becomes larger than 1000 then the composite message (up to 1000) is immediately set out to all clients and any remaining characters are used to start a new composite message with a lSeqNum = 0.




<em><u>UDP Client (40 points)</u></em>




In order to test your server, write a console program that takes as a <strong>command line argument</strong> the <strong>IP Address</strong> and <strong>port number</strong> of the server as shown below:

<strong>./a.out localhost 51717 </strong>

The program should prompt the user for inputs and display any messages received.

Here are example user inputs:

<strong>Please enter command: v #</strong>                                the user enters a “v”, a space, and then a version number. This version number is now used in all new messages.

<strong>Please enter command: t #</strong> # <strong>message string</strong>    the user enters a “t”, a space, and then a <strong>type</strong> number, and then a <strong>sequence</strong> number, followed by the <strong>message</strong> (if any).  Be sure you are able to handle the spaces in the message.

<strong>Please enter command: q</strong>                                  the user enters a “q” causes the socket to be closed and the program to terminate.




Any messages received should be displayed as followed:

<strong>Received Msg Type:</strong> <strong>1, Seq: 33, Msg: </strong><em>message received</em>




<strong> </strong>

<h2>Appendix A: Coding Standards</h2>

<em><u>Indentation</u></em>:

When using <em>if/for/while</em> statements, make sure you indent 4 spaces for the content inside those.  Also make sure that you use spaces to make the code more readable.

For example:

for (int i; i &lt; 10; i++)

{     j = j + i;

}




If you have nested statements, you should use multiple indentions. Each { should be on its own line (like the <em>for</em> loop) If you have <em>else</em> or <em>else if</em> statements after your <em>if</em> statement, they should be on their own line.

for (int i; i &lt; 10; i++)

{

if (i &lt; 5)    {        counter++;         k -= i;     }           else

{                            k +=1;    }         j += i;

}




<em><u>Camel Case:</u> </em>

This naming convention has the first letter of the variable be lower case, and the first letter in each new word be capitalized (e.g. firstSecondThird). This applies for functions and member functions as well! The main exception to this is class names, where the first letter should also be capitalized.

<em><u>Variable and Function Names</u>:</em>

Your variable and function names should be clear about what that variable or function is. Do not use one letter variables, but use abbreviations when it is appropriate (for example: “imag” instead of

“imaginary”). The more descriptive your variable and function names are, the more readable your code will be.  This is the idea behind self-documenting code.

<em>                 </em>

<em><u>File Headers</u>: </em>

Every file should have the following header at the top

/*

Author: &lt;your name&gt;

Class: ECE4122 or ECE6122

Last Date Modified: &lt;date&gt;




Description:




What is the purpose of this file?




*/

<em><u>Code Comments:</u> </em>




<ol>

 <li>Every function must have a comment section describing the purpose of the function, the input and output parameters, the return value (if any).</li>

 <li>Every class must have a comment section to describe the purpose of the class.</li>

 <li>Comments need to be placed inside of functions/loops to assist in the understanding of the flow of the code.</li>

</ol>







<strong> </strong>

<h2>Appendix B: Accessing PACE-ICE Instructions</h2>

<strong><em><u>ACCESSING LINUX PACE-ICE CLUSTER (SERVER)</u></em></strong>

To access the PACE-ICE cluster you need certain software on your laptop or desktop system, as described below.




<strong><u>Windows Users:</u></strong>

<u>Option 0 (Using SecureCRT)- THIS IS THE EASIEST OPTION!</u>

The Georgia Tech Office of Information Technology (<em>OIT) </em>maintains a web page of software that can be downloaded and installed by students and faculty. That web page is:   http://software.oit.gatech.edu

From that page you will need to install SecureCRT.

To access this software, you will first have to log in with your Georgia Tech user name and password, then answer a series of questions regarding export controls.

Connecting using SecureCRT should be easy.

<ul>

 <li>Open SecureCRT, you’ll be presented with the “Quick Connect” screen.</li>

 <li>Choose protocol “ssh2”.</li>

 <li>Enter the name of the PACE machine you wish to connect to in the “HostName” box (i.e. <em> </em></li>

</ul>

<em>  coc-ice.pace.gatech.edu</em>)

<ul>

 <li>Type your username in the “Username” box.</li>

 <li>Click “Connect”.</li>

 <li>A new window will open, and you’ll be prompted for your password.</li>

</ul>




<u>Option 1 (Using Ubuntu for Windows 10):</u>

Option 1 uses the Ubuntu on Windows program. This can only be downloaded if you are running  Windows 10 or above. If using Windows 8 or below, use Options 2 or 3. It also requires the use of simple bash commands.

<ol>

 <li>Install Ubuntu for Windows 10 by following the guide from the following link:</li>

</ol>




<u>https://msdn.microsoft.com/en-us/commandline/wsl/install-win10</u>

<ol start="2">

 <li>Once Ubuntu for Windows 10 is installed, open it and type the following into the command line:</li>

</ol>




<em>ssh **YourGTUsername**@coc-ice.pace.gatech.edu </em>where **YourGTUsername** is replaced with your alphanumeric GT login. Ex: bkim334

<ol start="3">

 <li>When it asks if you’re sure you want to connect, type in:</li>

</ol>

<em>yes </em>

and type in your password when prompted (Note: When typing in your password, it will not show any characters typing)

<ol start="4">

 <li>You’re now connected to PACE-ICE. You can edit files using vim by typing in:</li>

</ol>




<em>vi filename.cc                </em>OR <em>                  nano vilename.cpp </em>

For a list of vim commands, use the following link:   <u>https://coderwall.com/p/adv71w/basic-vim-commands-for-getting-started</u>

<ol start="5">

 <li>You’re able to edit, compile, run, and submit your code from this command line.</li>

</ol>




<u>Option 2 (Using PuTTY):</u>

Option 2 uses a program called PuTTY to ssh into the PACE-ICE cluster. It is easier to set up, but doesn’t allow you to access any local files from the command line. It also requires the use of simple bash commands.

<ol>

 <li>Download and install PuTTY from the following link: <u>putty.org</u></li>

 <li>Once installed, open PuTTY and for the Host Name, type in:</li>

</ol>

<em>coc-ice.pace.gatech.edu </em>and

for the port, leave it as 22.

<ol start="3">

 <li>Click Open and a window will pop up asking if you trust the host. Click Yes and it will then ask you for your username and password. (Note: When typing in your password, it will not show any characters typing)</li>

</ol>




<ol start="4">

 <li>You’re now connected to PACE-ICE. You can edit files using vim by typing in: <em>vim filename.cc </em></li>

</ol>

<em>            </em>OR <em>                  nano vilename.cpp </em>

<em> </em>

For a list of vim commands, use the following link:

<u>https://coderwall.com/p/adv71w/basic-vim-commands-for-getting-started</u>

<ol start="5">

 <li>You’re able to edit, compile, run, and submit your code from this command line.</li>

</ol>







<strong><u>MacOS Users:</u></strong>. <strong> </strong>

<u>Option 0 (Using the Terminal to SSH into PACE-ICE):</u>

This option uses the built-in terminal in MacOS to ssh into PACE-ICE and use a command line text editor to edit your code.

<ol>

 <li>Open Terminal from the Launchpad or Spotlight Search.</li>

</ol>




<ol start="2">

 <li>Once you’re in the terminal, ssh into PACE-ICE by typing:</li>

</ol>




<em>ssh **YourGTUsername**@ coc-ice.pace.gatech.edu </em>where **YourGTUsername** is replaced with your alphanumeric GT login. Ex: bkim334

<ol start="3">

 <li>When it asks if you’re sure you want to connect, type in:</li>

</ol>

<em>yes </em>

and type in your password when prompted (Note: When typing in your password, it will not show any characters typing)

<ol start="4">

 <li>You’re now connected to PACE-ICE. You can edit files using vim by typing in:</li>

</ol>




<em>vi filename.cc                </em>OR <em>                  nano filename.cpp </em>

For a list of vim commands, use the following link:  <u>https://coderwall.com/p/adv71w/basic-vimcommands-for-getting-started</u>

<ol start="5">

 <li>You’re able to edit, compile, run, and submit your code from this command line.</li>

</ol>




<strong><u>Linux Users:</u></strong>

If you’re using Linux, follow Option 0 for MacOS users.




<h2>Appendix B: Submitting Assignment</h2>

<u>Step-By-Step Submitting a Tar.gz</u>

<strong><em><u>PLEASE NOTE:</u></em></strong> All the following instructions are run on PACE. If you are struggling with any of the steps, please come see the TAs during office hours. Better to start and test early than wait until the last minute.

Below is a step-by-step tutorial on how to create the .tgz file for Homework 4 for ECE 4122/6122. Please know, if you are in 4122 you do not need to submit anything for Problem 2. Additionally, if you do not use a header file for a solution, you do not need to submit a header file. Please adjust these instructions accordingly. The tarball should contain a folder with your buzzid containing subfolders for each problem you are assigned with the corresponding .cpp and .h files. Each problem will have a SERVER and CLIENT folder with corresponding code.

Please make sure that each problem is in its own subfolder with the naming conventions:

&lt;FirstName_LastName&gt;_Hmk4Prob# (where # is either 1 or 2) in addition to the SERVER and CLIENT folders:










Create a subdirectory named <em>buzzid </em>in the current working directory by executing the following command in the shell:

$ mkdir <em>buzzed </em>

(In this case my <em>buzzid </em>is tlagrow3)







Create a text file named <strong>manifest.</strong>




Please make sure that the <strong>manifest</strong> file is a plain text file and not a rich text file. Microsoft word will generate a rich text file. The easiest method to create a plain text file is to use a command line editor such as vi, vim, or nano.

(If you want a tutorial, these can be usefule: vi:

<a href="http://heather.cs.ucdavis.edu/%7Ematloff/UnixAndC/Editors/ViIntro.html">http://heather.cs.ucdavis.edu/~matloff/UnixAndC/Editors/ViIntro.html</a><a href="http://heather.cs.ucdavis.edu/%7Ematloff/UnixAndC/Editors/ViIntro.html">,</a> vim: <a href="https://openvim.com/">https://openvim.com/</a><a href="https://openvim.com/">,</a> nano: <a href="https://www.howtogeek.com/howto/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/">https://www.howtogeek.com/howto/42980/the-beginners-guide-to-nano-the-linux-command</a><a href="https://www.howtogeek.com/howto/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/">line-text-editor/</a><a href="https://www.howtogeek.com/howto/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/">)</a>




The editor will open:










You will need to insert test into this file. Press the ‘i’ key on the keyboard to insert text:










Populate the <strong>manifest</strong> file with the following:




<em>buzzid</em>/&lt;FirstName_LastName&gt;_Hmk4Prob1/SERVER/*.cpp  <em>buzzid</em>/&lt;FirstName_LastName&gt;_Hmk4Prob1/SERVER/*.h  <em>buzzid</em>/&lt;FirstName_LastName&gt;_Hmk4Prob1/CLIENT/*.cpp  <em>buzzid</em>/&lt;FirstName_LastName&gt;_Hmk4Prob1/CLIENT/*.h  <em>buzzid</em>/&lt;FirstName_LastName&gt;_Hmk4Prob2/SERVER/*.cpp  <em>buzzid</em>/&lt;FirstName_LastName&gt;_Hmk4Prob2/SERVER/*.h  <em>buzzid</em>/&lt;FirstName_LastName&gt;_Hmk4Prob2/CLIENT/*.cpp  <em>buzzid</em>/&lt;FirstName_LastName&gt;_Hmk4Prob2/CLIENT/*.h







(<strong><em><u>PLEASE NOTE</u></em></strong>: this is subject to change with depending on your class section. The wildcard (*) character will grab all the .cpp and .h files you generated for each problem.)







To save the file, hold the Shift key and press ‘ZZ’. This command will save the text and exit in the vim text editor. To check that the file saved, you can use the command ‘$cat &lt;filename&gt;’ to print out all the lines:







Now you need to construct the correct file structure for the submission. This means that you need to put all the homework files into your <em>buzzid </em>folder. Execute the following lines in the shell:




$ cp -a &lt;FirstName_LastName&gt;_* <em>buzzid  </em>

<em> </em>







Many people have had issue with this step. You need to make sure the naming conventions are consistent to avoid potential problems.




It is now time to tarball your submission. If all the other steps have gone smoothly, execute the following command:




$ tar -zcvf <em>buzzid</em>-hmk4.tgz $(cat manifest)




This command will generate a new tgz file with all of the specified files and folders in the manifest text document:










You can now check the new tgz file just generated with the following command:




$ tar -ztvf <em>buzzid</em>-hmk4.tgz










If your file has the same structure as above, you are all good to submit!








