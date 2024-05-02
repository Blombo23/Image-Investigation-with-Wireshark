# Investigation-with-Wireshark

<h2>Description</h2>
Suspicious network activity has been detected coming from a user on the ANZ network. 

A laptop has been flagged up on our security systems due to suspicious internet traffic, and we need you to investigate the network traffic in order to establish what the user accessed and downloaded.

Your task is to examine their network activity and gather what information you can on what images they viewed and what files they accessed. 

You have been provided with a packet capture file (pcap) containing all their recent network activity. There may be a number of artifacts contained within the packet capture file, and you will be expected to identify and report as many as possible. 

You must provide a report on everything you found, and document what processes / steps you followed to achieve this.

<h2>Retrieve a jpeg image </h2>
To find the images, I followed the following process : <br/><br/>
First I filtered the packet capture for http traffic and looked through the remaining packets for the GET request
that downloaded the image. I then right clicked the image and followed its TCP stream.
In the TCP stream I saw what looked like image data. In order to view the data in hex format, I changed the view to
‘raw’, and then searched the hex data for a jpeg’s file signature.<br/><br/>
After finding the file signature “FFD8” the top, and the file footer “FFD9” at the bottom, I copied everything
between those two points into the hex editor HxD and saved it as a jpg image.

<h2>Retrieve a pdf file </h2>
In order to view these PDF's I viewed the TCP stream as usual, and found the file signature for a PDF, which was
the hex data “25 50 44 46”. I noticed in the ascii view that the PDF data went until the very end of the TCP stream,
so I copied all the hex date from the file signature onwards into HxD and saved it as a pdf file.



