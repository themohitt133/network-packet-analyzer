# Analysis Findings

## 1. Overview

The captured traffic was analyzed to identify normal HTTP communication, failed requests, and potentially suspicious request patterns.

## 2. Normal HTTP Traffic

Normal HTTP requests were observed during the controlled testing process.

Example:

```text
GET /
```

This represents a request for the root resource of the local HTTP server.

## 3. Successful Response

The normal request can result in:

```text
200 OK
```

This indicates that the requested resource was successfully returned by the server.

## 4. Failed Request

The following request was used to generate a failed HTTP request:

```text
GET /not-found
```

The expected response is:

```text
404 Not Found
```

This demonstrates how unavailable resources appear in HTTP traffic.

## 5. Suspicious Request

The following request was generated:

```text
GET /.env
```

The `.env` path is considered a potentially sensitive resource because environment files can contain application configuration and secrets.

The request can be filtered in Wireshark using:

```text
http.request.uri == "/.env"
```

## 6. Security Interpretation

The request for `/.env` should be treated as an indicator requiring investigation rather than definitive proof of malicious activity.

Additional evidence would be required to determine whether the request represents:

* Manual testing
* Automated scanning
* Reconnaissance
* An accidental request
* A genuine attack attempt

## 7. Evidence Files

The following files support the analysis:

```text
captures/sample_capture.pcapng
screenshots/packet-capture.png
screenshots/http-analysis.png
screenshots/suspicious-request.png
analysis/http_analysis.txt
```

## 8. Conclusion

The project successfully demonstrates how Wireshark can be used to capture and analyze HTTP traffic and identify request patterns that may require further security investigation.

The controlled environment makes it possible to study these patterns without analyzing unauthorized traffic.

