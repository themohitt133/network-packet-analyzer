# Network & Packet Analyzer — Project Documentation

## 1. Introduction

Network & Packet Analyzer is a cybersecurity and network analysis project developed using Wireshark.

The project focuses on capturing network traffic, analyzing HTTP requests and responses, and identifying potentially suspicious request patterns in a controlled laboratory environment.

## 2. Problem Statement

Network traffic contains valuable information about communication between systems. Manually identifying unusual or suspicious HTTP requests from packet captures can be difficult for beginners.

This project demonstrates a practical method for capturing and inspecting network traffic and identifying request patterns that may require further investigation.

## 3. Project Objectives

* Capture network packets using Wireshark.
* Generate controlled HTTP traffic.
* Analyze HTTP requests and responses.
* Inspect HTTP methods and requested resources.
* Identify failed HTTP requests.
* Detect potentially suspicious request paths.
* Preserve packet captures as evidence.
* Document the analysis process and findings.

## 4. Tools Used

### Wireshark

Used for capturing and analyzing network packets.

### Linux

Used as the testing environment and for executing commands.

### Python HTTP Server

Used to create a controlled local HTTP service.

### curl

Used to generate HTTP requests against the local test server.

## 5. System Architecture

```text
Local Test Client
       |
       | HTTP Requests
       ↓
Python HTTP Server
       |
       ↓
Network Traffic
       |
       ↓
Wireshark Capture
       |
       ↓
Packet Analysis
       |
       ├── HTTP Request Analysis
       ├── HTTP Response Analysis
       └── Suspicious Request Detection
       |
       ↓
Analysis Report
```

## 6. Testing Environment

The project was performed in a controlled virtual-machine/laboratory environment.

The HTTP server was hosted locally using:

```text
127.0.0.1:8000
```

This environment was used to avoid analyzing unauthorized third-party traffic.

## 7. Traffic Generation

A Python HTTP server was started using:

```bash
python3 -m http.server 8000
```

HTTP requests were generated using curl.

Example:

```bash
curl http://127.0.0.1:8000/
```

Additional requests were generated for controlled analysis:

```bash
curl http://127.0.0.1:8000/index.html
curl http://127.0.0.1:8000/not-found
curl http://127.0.0.1:8000/.env
```

## 8. Packet Capture

Wireshark was used to capture the generated traffic.

The relevant network interface was selected and packet capture was started before generating the HTTP requests.

The resulting capture was saved as:

```text
captures/sample_capture.pcapng
```

## 9. HTTP Analysis

HTTP traffic was isolated in Wireshark using:

```text
http
```

The following information was inspected:

* HTTP request method
* Requested URI
* Host
* Source address
* Destination address
* HTTP response status
* User-Agent
* Timestamp

## 10. Suspicious Request Analysis

The following request was generated for controlled testing:

```text
GET /.env
```

The request can be identified in Wireshark using:

```text
http.request.uri == "/.env"
```

A request for a sensitive-looking configuration file can be considered an investigation-worthy indicator because such files may contain application configuration or secrets.

However, the presence of this request alone does not prove malicious activity.

## 11. HTTP Status Analysis

A normal request such as:

```text
GET /
```

may return:

```text
200 OK
```

A request for a non-existent resource such as:

```text
GET /not-found
```

may return:

```text
404 Not Found
```

These responses were used to demonstrate the difference between successful and failed HTTP requests.

## 12. Evidence

The project stores the following evidence:

```text
captures/sample_capture.pcapng
screenshots/packet-capture.png
screenshots/http-analysis.png
screenshots/suspicious-request.png
analysis/http_analysis.txt
```

These files document the packet capture and analysis process.

## 13. Security Considerations

Packet captures can contain sensitive information.

Examples include:

* Credentials
* Cookies
* Session tokens
* IP addresses
* HTTP request data
* Private communications

Only controlled and authorized traffic should be captured.

Real-world packet captures containing sensitive information should not be uploaded to a public repository.

## 14. Limitations

This project focuses primarily on HTTP traffic analysis.

A suspicious HTTP request does not automatically mean that an attack has occurred.

For a complete investigation, additional sources may be required, including:

* Web server logs
* Authentication logs
* DNS logs
* Firewall logs
* Endpoint logs
* Application logs

## 15. Future Improvements

Potential improvements include:

* Automated PCAP analysis
* Automatic suspicious-request detection
* IP address analysis
* HTTP status-code statistics
* Command-line interface
* User-provided PCAP input
* Automatic report generation
* JSON/CSV export
* Web-based analysis dashboard

## 16. Ethical Use

This project is intended for educational purposes, authorized security testing, and controlled laboratory environments.

Network traffic should only be captured and analyzed when appropriate authorization has been obtained.

