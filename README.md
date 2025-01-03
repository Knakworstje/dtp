# URI Scheme Registration Proposal for DTP and SDTP

## General Information

### Scheme Names:

- `dtp` (Distributed Timeseries Protocol)
- `sdtp` (Secure Distributed Timeseries Protocol)

## Introduction

### Purpose of the Protocols:

The Distributed Timeseries Protocol (DTP) and Secure Distributed Timeseries Protocol (SDTP) are designed to efficiently retrieve and aggregate time-series data from distributed data sources. The protocols enable clients to query and merge data streams from multiple servers based on UNIX timestamps, providing a unified and seamless data retrieval mechanism.

SDTP extends DTP by adding encryption and authentication capabilities, ensuring secure communication and data integrity.
SDTP uses ECDSA (Elliptic Curve Digital Signature Algorithm) together with the elliptic curve secp256r1 (also known as prime256v1) to establish a secure method of communication between the client and SDTP server.

secp256r1 is an elliptic curve used in cryptography, also known as prime256v1, and it is a widely accepted standard for secure communication. It provides strong security with relatively low computational overhead, making it suitable for use in modern protocols.

### Use Cases:

1. Distributed logging systems where time-stamped events are stored across multiple nodes.
2. Data synchronization between distributed systems.
2. Secure and efficient time-series database queries over a trusted or an untrusted network.

## Syntax and Semantics

### URI Syntax:

- DTP: `dtp://<host>[:<port>]/<from-timestamp>/<to-timestamp>`
- SDTP: `sdtp://<host>[:<port>]/<from-timestamp>/<to-timestamp>`

#### Components:

- `<host>`: The hostname or IP address of the server.
- `<port>`: (Optional) The port number where the DTP or SDTP service is hosted.
- `<from-timestamp>`: The start of the timestamp range for the query.
- `<to-timestamp>`: The end of the timestamp range for the query.

### Example URIs:

- `dtp://data.example.com/764317344/1189253299`
- `sdtp://secure-data.example.com/764317344/1189253299`

### Status Codes:
- 1xx
    - 100 Success
    - 101 Blacklisted
- 2xx
   - 200 Internal Error
   - 201 Service Unavailable
- 3xx
   - 300 Invalid Range
   - 301 Authentication Failed
   - 302 Invalid URI
   - 303 Forbidden
   - 304 SDTP Required
   - 305 Invalid Session ID

## Protocol Description

### DTP (Distributed Timeseries Protocol):
1. **Client Request:** The client sends a request to the server, specifying a time range (from-timestamp to to-timestamp).
2. **Server Response:** The server returns a list of data source URIs (e.g., database nodes) containing relevant data.
3. **Data Retrieval:** The client queries the listed data sources in parallel, retrieves the data, and merges it locally.

### SDTP (Secure Distributed Timeseries Protocol):

1. **Session Initialisation:** The client sends a request to the server containing their ECDSA public key.
2. **Server Inititialisation Response:** The server receives the request and sends back their ECDSA public key together with a generated session id and stores these as a key-value pair.
3. **Client Request:** The client sends an encrypted request to the server using the server's private key, specifying a time range (from-timestamp to to-timestamp) and the client attaches their session ID and a signature.
4. **Server Response:** The server verifies the signature and returns a list of data source URIs (e.g., database nodes) containing relevant data.
5. **Client Termination:** The client sends a STER (Session Termination) request with their session key and a signature attached.
6. **Server Termination:** The server verifies the signature and, upon success, removes the key-value pair containing the session ID and client's public key from memory.
7. **Data Retrieval:** The client queries the listed data sources in parallel, retrieves the data, and merges it locally.

## Security Considerations

- **DTP:**

  - Does not provide encryption or authentication.
  - Should only be used in trusted environments.

- **SDTP:**

  - Uses ECDSA for encryption and mutual authentication.
  - Prevents data tampering and eavesdropping.

## Chart
![image](https://github.com/Knakworstje/dtp/blob/main/chart.png)

## Registration Details

### Applications and Use:

- Distributed systems requiring time-series data aggregation.
- Internet of Things (IoT) networks for time-sensitive data synchronization.

### Intended Status:

Permanent registration.

## References

- Github Repository: [Repository](https://github.com/Knakworstje/dtp)
