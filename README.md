# URI Scheme Registration Proposal for DTP and SDTP

## General Information

### Scheme Names:

- `dtp` (Distributed Timestream Protocol)
- `sdtp` (Secure Distributed Timestream Protocol)

### Contact Information:

- **Name:** Daan Alexander Verhulst
- **Email:** daanverhulst2010@gmail.com

## Introduction

### Purpose of the Protocols:

The Distributed Timestream Protocol (DTP) and Secure Distributed Timestream Protocol (SDTP) are designed to efficiently retrieve and aggregate time-series data from distributed data sources. The protocols enable clients to query and merge data streams from multiple servers based on timestamps, providing a unified and seamless data retrieval mechanism.

SDTP extends DTP by adding TLS encryption and authentication capabilities, ensuring secure communication and data integrity.

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

## Protocol Description

### DTP (Distributed Timestream Protocol):

1. **Client Request:** The client sends a request to the server, specifying a time range (from-timestamp to to-timestamp).
2. **Server Response:** The server returns a list of data source URIs (e.g., database nodes) containing relevant data.
3. **Data Retrieval:** The client queries the listed data sources in parallel, retrieves the data, and merges it locally.

### SDTP (Secure Distributed Timestream Protocol):

1. **Encryption:** All communication is encrypted using TLS.
2. **Authentication:** The client must present a valid authentication key or token to access data.

## Security Considerations

- **DTP:**

  - Does not provide encryption or authentication.
  - Should only be used in trusted environments.

- **SDTP:**

  - Uses TLS for encryption and mutual authentication.
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

- Github Repository: [text](https://github.com/Knakworstje/dtp)
