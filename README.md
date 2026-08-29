# Network & Packet Analyzer

A Wireshark-based network traffic analysis project for capturing packets, inspecting HTTP traffic, and identifying suspicious request patterns in a controlled environment.

## Overview

Network & Packet Analyzer demonstrates practical network traffic analysis using Wireshark, a local HTTP test server, and curl.

The project captures network packets, filters HTTP traffic, analyzes requests and responses, and identifies potentially suspicious request indicators such as repeated requests for sensitive-looking paths.

The project is designed as a controlled cybersecurity learning and portfolio project.

## Objectives

* Capture network packets using Wireshark
* Analyze HTTP traffic
* Inspect HTTP requests and responses
* Identify failed HTTP requests
* Detect suspicious request patterns
* Document packet-level findings
* Preserve packet captures and screenshots as analysis evidence

## Features

* Network packet capture
* HTTP traffic filtering
* HTTP request inspection
* HTTP response analysis
* 404 request analysis
* Suspicious request detection
* Repeated request pattern analysis
* PCAPNG capture storage
* Analysis report generation
* Evidence screenshots

## Tools & Technologies

* Wireshark
* Linux
* Python
* Python HTTP Server
* curl
* PCAPNG

## Project Structure

```text
network-packet-analyzer/
│
├── captures/
│   └── sample_capture.pcapng
│
├── analysis/
│   └── http_analysis.txt
│
├── screenshots/
│   ├── packet-capture.png
│   ├── http-analysis.png
│   └── suspicious-request.png
│
├── lab-server/
│   └── index.html
│
├── README.md
├── LICENSE
└── .gitignore
```

## How It Works

```text
Controlled HTTP Traffic
          ↓
   Wireshark Capture
          ↓
    Captured Packets
          ↓
    HTTP Filtering
          ↓
Request & Response Analysis
          ↓
Suspicious Pattern Detection
          ↓
     Evidence & Report
```

## Controlled HTTP Testing

A local Python HTTP server is used to generate controlled HTTP traffic.

The server runs on:

```text
127.0.0.1:8000
```

Example requests used during the analysis:

```text
GET /
GET /index.html
GET /not-found
GET /.env
```

The requests are generated using curl and captured with Wireshark.

## HTTP Traffic Analysis

Wireshark can be used to filter HTTP traffic with:

```text
http
```

Individual HTTP packets can then be inspected for:

* Request method
* Request URI
* Host
* Source address
* Destination address
* Response code
* User-Agent
* Timestamp

## Suspicious Request Detection

The project demonstrates detection of a potentially suspicious request for:

```text
/.env
```

The following Wireshark display filter can be used:

```text
http.request.uri == "/.env"
```

Requests for sensitive-looking configuration paths can be treated as investigation-worthy indicators.

Repeated requests for the same path may indicate automated probing or reconnaissance.

A single request does not prove malicious intent or compromise. Additional evidence and context are required for a definitive security assessment.

## Example Analysis

### Normal Request

```text
GET /
```

Expected response:

```text
200 OK
```

### Failed Request

```text
GET /not-found
```

Expected response:

```text
404 Not Found
```

### Suspicious Indicator

```text
GET /.env
```

This request is treated as a suspicious indicator because `.env` files may contain application configuration or sensitive information.

The request itself does not establish that sensitive information was successfully accessed.

## Evidence

The project contains:

* Packet capture file
* HTTP analysis report
* Packet capture screenshot
* HTTP analysis screenshot
* Suspicious request screenshot

These artifacts provide evidence of the traffic captured and analyzed during the controlled testing process.

## Security & Privacy

This project uses controlled test traffic generated in a local lab environment.

Real network captures may contain sensitive information such as:

* Credentials
* Cookies
* Session tokens
* Personal IP addresses
* DNS information
* Private communications

Real or sensitive packet captures should not be uploaded to a public repository.

## Limitations

This project currently focuses on Wireshark-based packet capture and analysis.

Packet-level evidence alone cannot determine malicious intent with certainty.

A complete security investigation may require additional data sources such as:

* Web server logs
* Application logs
* Authentication logs
* DNS logs
* Endpoint information
* Firewall logs

## Future Improvements

Possible future improvements include:

* Automated PCAP analysis
* User-provided capture file input
* Command-line analysis interface
* Automated suspicious request detection
* IP-based traffic analysis
* HTTP status-code statistics
* Automatic report generation
* JSON/CSV report output
* Interactive user input and analysis options

## Ethical Use

This project is intended for authorized security testing, network analysis, and educational lab environments.

Do not capture or analyze network traffic without appropriate authorization.

## Author

Mohit Pal

## Commands Used

The following commands were used during the development and testing of this project:

```bash
# Start the local HTTP test server
python3 -m http.server 8000

# Generate a normal HTTP request
curl http://127.0.0.1:8000/

# Generate a request for another resource
curl http://127.0.0.1:8000/index.html

# Generate a failed request
curl http://127.0.0.1:8000/not-found

# Generate a suspicious-path request for controlled testing
curl http://127.0.0.1:8000/.env

# Check the project directory
pwd

# Check project files, including hidden files
ls -la

# Check for Vim swap files
find . -name "*.swp"
```

