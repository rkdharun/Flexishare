## Architecture

The architecture of Flexi revolves around a Client-Server model, where each device can assume the role of either a server or a client, but not both simultaneously. When a device is designated as a server, it generates a QR code with ip and port information.

This architecture ensures efficient and organized communication between devices. Device acting as the client contains a QR scanner to ensure quick connections

## Protocol

Flexi utilizes the TCP/IP protocol for reliable communication between devices. The packets transmitted within the application are in binary format, consisting of a header and a body. The header contains essential information about the packet, such as its type and additional metadata. The body of the packet contains the actual data being transmitted, which typically includes Selected content. 

## Security

Flexi uses TLS over TCP to ensure secure communication between devices. TLS provides end-to-end encryption, preventing unauthorized access to the data being transmitted. This security mechanism ensures that the shared content is protected from malicious attacks and other security threats, allowing for safe and secure data transfer across devices. By utilizing TLS over TCP, Flexi guarantees that the data is transmitted securely and reliably, enhancing the overall user experience.

## Packet Types

Flexi utilizes a variety of packet types for different purposes. These packet types include the request packet, data packet, and others, each serving a specific function within the application. Below, we provide a detailed description of each packet type and its intended usage in Flexi.

### What are the packets Required for Flexi

Once the server and client are connected,  data is transmitted between the client and the server using a single type of packet known as the **DataPacket**. This packet is responsible for transferring  data from the client to the server and vice versa. 

Finally we have **InvalidRequest** which is used to indicate that the packet sent by client is invalid so it provides a way to indicate that the packet status. This packet should only sent from server to client not from client to server.

#### Packet Length

The **Packet Length** field specifies the length of the packet, which is the sum of the length of the header and the length of the body. This field is used to determine the size of the packet, allowing for efficient and organized data transmission within the application. This field is First field in all of the packets.

### InvalidRequest

The **InvalidRequest** is used to indicate that the packet is invalid. This packet contains the following fields:

#### Header

- **Packet Length**: This field specifies the length of the packet, for invalid packet it is length of error code and error message.
- **Packet Type**: This field specifies the type of packet, which is set to 0x00 for the Invalid Packet.

#### Body

- **Error Code**: This field specifies the error code.
- **Error Message**: This field contains the error message.

#### Structure

| Field           | Bytes  | value |
|-----------------|--------| ----- |
| Packet Length   | 4      |       |
| Packet Type     | 1      | 0x00  |
| Error Code      | 1      |       |
| Error Message   | varies |       |

#### Possible Error Codes

| Error Code | Error Message |
|------------|---------------|
| 0x01       | Coding Error  |
| 0x02       | TLS Error     |

### Authentication

The **Authentication** is used to indicate the authentication process to the client. This packet contains the following fields:

#### Header

- **Packet Length**: This field specifies the length of the packet, for AuthPacket it is length of the auth token.
- **Packet Type**: This field specifies the type of packet, which is set to 0x01 for the AuthPacket.

#### Body

- **AuthStatus**: This field specifies the status of the authentication process. it can be one of the following values.
    - 0x00: Auth Failed
    - 0x01: Auth Success

#### Structure

| Field           | Bytes | value |
|-----------------|-------| ----- |
| Packet Length   | 4     |       |
| Packet Type     | 1     | 0x01  |
| AuthStatus      | 1     |       |

### DataPacket

The **SyncingPacket** is used to transfer  data between the client and the server. This packet contains the following fields:

#### Header

- **Packet Length**: This field specifies the length of the packet, for SyncingPacket it is length of  data and type of  data.
- **Packet Type**: This field specifies the type of packet, which is set to 0x02 for the SyncingPacket.

#### Body
- **MimeLength**: This field specifies the length of the clipboard data type.
- **MimeType**: This field contains the type of clipboard data, which can be text, image, or other data, asper mime type.
- **PayloadLength**: This field specifies the length of the clipboard data.
- **Payload**: This field contains the actual clipboard data.

#### Structure

| Field           | Bytes | value |
|-----------------|-------| ----- |
| Packet Length   | 4     |       |
| Packet Type     | 1     | 0x02  |
| MimeLength      | 4     |       |
| MimeType        | varies|       |
| PayloadLength   | 4     |       |
| Payload         | varies|       |
| MimeLength      | 4     |       |
| MimeType        | varies|       |
| PayloadLength   | 4     |       |
| Payload         | varies|       |
| ...             | ...   | ...   |

#### Supported Data Types
    -All file types and formats are supported 
    
