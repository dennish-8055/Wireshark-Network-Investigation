# Wireshark Network Traffic Investigation Report

## 1. Objective

Analyze captured network traffic using Wireshark to understand DNS queries, TCP connection activity, and TLS communication.

## 2. Environment

* **Operating System:** Windows
* **Tool:** Wireshark 4.6.9
* **Capture Interface:** Wi-Fi
* **Capture Format:** PCAPNG

## 3. Investigation Methodology

The following Wireshark display filters were used:

* `dns` — to inspect DNS queries and responses.
* `tcp.flags.syn == 1 && tcp.flags.ack == 0` — to identify initial TCP connection attempts.
* `tcp.flags.syn == 1 && tcp.flags.ack == 1` — to inspect TCP SYN-ACK responses.
* `tls` — to inspect TLS traffic.

## 4. Findings

### 4.1 DNS Analysis

* DNS queries for `dns.google` were observed.
* Packet 406 contained an A-record query for `dns.google`.
* Packet 407 contained the corresponding DNS response.
* The response reported no DNS error and contained the IPv4 addresses `8.8.8.8` and `8.8.4.4`.
* Wireshark reported a response time of approximately 2.09 milliseconds.

### 4.2 TCP Analysis

* TCP SYN packets involving the local host and remote IP addresses were observed.
* The SYN display filter showed 47 packets.
* The SYN-ACK display filter showed 52 packets.
* These observations demonstrate TCP connection attempts and responses. The counts alone do not establish that every connection succeeded or indicate malicious activity.

### 4.3 TLS Analysis

* TLS 1.2 and TLS 1.3 traffic were observed.
* A TLS 1.3 Client Hello containing a visible Server Name Indication (SNI) hostname was identified. The hostname is omitted here for privacy.
* Server Hello and encrypted application-data packets were also observed.
* These observations are consistent with encrypted TLS communication.

## 5. Conclusion

The captured traffic contained DNS queries and responses, TCP connection attempts and responses, and TLS communication. The investigation demonstrated how Wireshark display filters and packet details can be used to examine network activity.

The observations documented in this report did not establish confirmed malicious activity.

## 6. Limitations

* The investigation covers only the traffic included in the capture.
* IP addresses, domains, and packet counts do not independently establish malicious behavior.
* Encrypted TLS application data could not be interpreted from the visible packet information alone.
* This was a basic network traffic investigation, not a complete security incident response exercise.

## 7. Tools and Skills

* Wireshark
* DNS query and response analysis
* TCP flag analysis
* TLS traffic inspection
* Display-filter usage
* Packet-level investigation
* Technical evidence documentation

## 8. Privacy and Responsible Use

* The report omits the specific local IP address and the observed SNI hostname to reduce disclosure of personal network activity.
* Screenshots intended for public sharing should be reviewed for local and remote IP addresses, browsing-related hostnames, timestamps, and other potentially sensitive details.
* Raw packet captures may contain personal or network metadata and should remain private unless appropriately reviewed and sanitized.
* Traffic was captured from my own computer for educational purposes.
