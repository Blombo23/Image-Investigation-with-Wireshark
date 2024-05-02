# Images investigation-with-Wireshark 

<h2>Description</h2>
Suspicious network activity has been detected coming from a user on the ANZ network. 

A laptop has been flagged up on our security systems due to suspicious internet traffic, and we need you to investigate the network traffic in order to establish what the user accessed and downloaded.

Your task is to examine their network activity and gather what information you can on what images they viewed and what files they accessed. 

You have been provided with a packet capture file (pcap) containing all their recent network activity. There may be a number of artifacts contained within the packet capture file, and you will be expected to identify and report as many as possible. 

You must provide a report on everything you found, and document what processes / steps you followed to achieve this.

<h2>Analyze a jpeg image </h2>
<b>Task 1:</b><br/>
- anz-logo.jpg and bank-card.jpg are two images that show up in the users network traffic.<br/>
- Extract these images from the pcap file and attach them to your report.<br/>

To find the images, I followed the following process : 
<br/><br/>
First I filtered the packet capture for http traffic and looked through the remaining packets for the GET request
that downloaded the image. I then right clicked the image and followed its TCP stream.
In the TCP stream I saw what looked like image data. In order to view the data in hex format, I changed the view to
‘raw’, and then searched the hex data for a jpeg’s file signature.<br/><br/>
After finding the file signature “FFD8” the top, and the file footer “FFD9” at the bottom, I copied everything
between those two points into the hex editor HxD and saved it as a jpg image.
<br/><br/>

<b>Task 2:</b>
- The user accessed an image called "atm-image.jpg"
- Identify what is different about this traffic and include everything in your report.

I viewed the TCP stream as normal when investigating this traffic, and found two sets of jpeg file signatures
instead of one like in the previous tasks.<br/><br/>
I tried extracting both sets of data, and got two different images. So the thing that is different about this traffic is that a single GET request performed by the user downloaded two images.
<br/><br/>

<b>Task 3:</b>
- The network traffic shows that the user accessed the image "broken.png"
- Extract and include the image in your report.

The TCP stream for the broken.png traffic did not show any file signature for a png image. So while viewing the
ascii form of the data, I recognized that the data was encoded in base64. Decrypting the base64 with an online
tool resulted in png image data, which I copied into the “decoded text” section of HxD and saved as a png file.
<br/><br/>

<b>Task 4:</b>
- The user also accessed a file called "hiddenmessage2.txt"
- What is the contents of this file? Include it in your report

I viewed the TCP stream of this file, and noticed that instead of being plain text it was encoded data and when
viewed as hex it had the same file signature as a jpg image.
So I copied and saved the hex data with HxD as I have for other images, and discovered that the text file was
actually an image.


<h2>Analyze content of a document </h2>
<b>Task 1:</b><br/>
- The user downloaded a suspicious document called "how-to-commit-crimes.docx"<br/>
- Find the contents of this file and include it in your report.<br/>

In order to find the contents of the document, I had to view the TCP stream of the http get request for the file. The
documents contents were visible in the ascii view.


<h2>Analyze a pdf file </h2>
<b>Task 1:</b><br/>
- The user accessed 3 pdf documents: ANZ_Document.pdf, ANZ_Document2.pdf, evil.pdf<br/>
- Extract and view these documents. Include images of them in your report.<br/><br/>

In order to view these PDF's I viewed the TCP stream as usual, and found the file signature for a PDF, which was
the hex data “25 50 44 46”. I noticed in the ascii view that the PDF data went until the very end of the TCP stream,
so I copied all the hex date from the file signature onwards into HxD and saved it as a pdf file.
<br/>

<b>Task 2:</b>
- The user accessed one more document called securepdf.pdf
- Access this document and include an image of the pdf in your report. Detail the steps to access it.

After investigating the TCP stream for securepdf.pdf I discovered three things:
<br/><br/>
The data there was not for a PDF.
<br/>
The bottom of the file contained the hidden message: Password is “secure”
<br/>
It contained the file signature for a zip file, meaning that the what the user downloaded was actually a zip file.
<br/><br/>
So I copied the hex of the zip file into HxD and saved it as a zip file. I opened this zip file, and found it contained a
pdf file called rawpdf.pdf. When opened, the pdf prompted for a password. The password ‘secure’ shown in the tcp
stream worked, and the PDF opened. It was the first two pages to a guide for internet banking.



