# Investigation-with-Wireshark

<h2>Description</h2>
Suspicious network activity has been detected coming from a user on the ANZ network. 

A laptop has been flagged up on our security systems due to suspicious internet traffic, and we need you to investigate the network traffic in order to establish what the user accessed and downloaded.

Your task is to examine their network activity and gather what information you can on what images they viewed and what files they accessed. 

You have been provided with a packet capture file (pcap) containing all their recent network activity. There may be a number of artifacts contained within the packet capture file, and you will be expected to identify and report as many as possible. 

You must provide a report on everything you found, and document what processes / steps you followed to achieve this.

<h2>Retrieve a jpeg image </h2>
Task : <br/>
- anz-logo.jpg and bank-card.jpg are two images that show up in the users network traffic.<br/>
- Extract these images from the pcap file and attach them to your report.<br/><br/>
To find the images, I followed the following process : 
<br/><br/>
First I filtered the packet capture for http traffic and looked through the remaining packets for the GET request
that downloaded the image. I then right clicked the image and followed its TCP stream.
In the TCP stream I saw what looked like image data. In order to view the data in hex format, I changed the view to
‘raw’, and then searched the hex data for a jpeg’s file signature.<br/><br/>
After finding the file signature “FFD8” the top, and the file footer “FFD9” at the bottom, I copied everything
between those two points into the hex editor HxD and saved it as a jpg image.


<h2>Retrieve content of document </h2>
Task : <br/>
- The user downloaded a suspicious document called "how-to-commit-crimes.docx"<br/>
- Find the contents of this file and include it in your report.
<br/><br/>
In order to find the contents of the document, I had to view the TCP stream of the http get request for the file. The
documents contents were visible in the ascii view.
<br/><br/>

<h2>Retrieve a pdf file </h2>
Task : <br/>
- The user accessed 3 pdf documents: ANZ_Document.pdf, ANZ_Document2.pdf, evil.pdf<br/>
- Extract and view these documents. Include images of them in your report.<br/><br/>
In order to view these PDF's I viewed the TCP stream as usual, and found the file signature for a PDF, which was
the hex data “25 50 44 46”. I noticed in the ascii view that the PDF data went until the very end of the TCP stream,
so I copied all the hex date from the file signature onwards into HxD and saved it as a pdf file.

<h2>Retrieve an hidden image from a text file </h2>
Task : <br/>
- The user also accessed a file called "hiddenmessage2.txt"<br/>
- What is the contents of this file? Include it in your report
<br/><br/>
I viewed the TCP stream of this file, and noticed that instead of being plain text it was encoded data and when
viewed as hex it had the same file signature as a jpg image.
So I copied and saved the hex data with HxD as I have for other images, and discovered that the text file was
actually an image.
