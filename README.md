# Reliable-Data-Transfer

Computer Networking Lab Project to implement a File Transfer service in Java using ARQ Protocols.
In this project, we are required to implement in Java a Reliable Data Transfer protocol (RDT).  RDT provides reliability and flow control using the Automatic Repeat Request (ARQ) and Sliding Window protocols.
RDT is supposed to be implemented in the OS Kernel at the Data Link Layer.

However, that being too complex, let us implement RDT as a transport-layer File Transfer service over UDP, using the Sliding Window concepts we have learnt in the context of the Data Link Layer. 

*adapted from here:* (http://nsl.cs.sfu.ca/teaching/09/371/prj3_reliableTransferProtocol.html)

### Objective

To implement a File Transfer service in Java using ARQ Protocols:
* Stop-and-Wait
* Go-Back-N
* Selective Repeat

### General Protocol Requirements
---
#### <u> Client File Request Format </u>

`REQUEST filename CRLF`, with no spaces between `REQUEST, filename` and `CRLF`


#### Server Message Format

`RDT sequence_number payload CRLF`, where 
the payload is a byte array of 512, and
the sequence_number represents the consignment number and is an ascending number between 0 and 255 stored in 1 byte

*At the very last consignment, the message format is as follows:*

`RDT sequence_number payload END CRLF`
In the last consignment, the payload is less than, or equals to 512 bytes.

#### Client Acknowledgement Format

`ACK sequence_number CRLF`
The sequence_number represents the consignment that the Client is expecting next, so it will be 1, 2, 3, 4, ... until the Client is notified of the last consignment.

<b> Upon receiving the last consignment, the Client sends an ACK with sequence_number 0, waits for 500ms and terminates the connection. </b>
Negative `ACK` is not required.

#### Requirements for Stop-and-Wait
*Time-Out = 30ms*

