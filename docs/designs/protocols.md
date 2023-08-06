## Architecture

The architecture of Flexi revolves around a Client-Server model, where each device can assume the role of either a server or a client, but not both simultaneously. When a device is designated as a server, it generates a QR code with ip and port information.

This architecture ensures efficient and organized communication between devices. Device acting as the client contains a QR scanner to ensure quick connections

## Protocol

Flexi utilizes the TCP/IP protocol for reliable communication between devices. The packets transmitted within the application are in binary format, consisting of a header and a body. The header contains essential information about the packet, such as its type and additional metadata. The body of the packet contains the actual data being transmitted, which typically includes Selected content. 

## Security

Flexi uses TLS over TCP to ensure secure communication between devices. TLS provides end-to-end encryption, preventing unauthorized access to the data being transmitted. This security mechanism ensures that the shared content is protected from malicious attacks and other security threats, allowing for safe and secure data transfer across devices. By utilizing TLS over TCP, Flexi guarantees that the data is transmitted securely and reliably, enhancing the overall user experience.

## Packet Types

    - **File packet**
    - **Clipboard packet**
    - **Invalid Request packet**

##FilePackets


    
