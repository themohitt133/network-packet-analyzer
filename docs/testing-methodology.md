# Testing Methodology

## 1. Purpose

The purpose of testing was to generate controlled HTTP traffic and analyze the resulting packets using Wireshark.

## 2. Environment

Testing was performed inside a controlled virtual-machine/laboratory environment.

The HTTP service was hosted locally at:

```text
127.0.0.1:8000
```

## 3. Test Procedure

### Step 1 — Start HTTP Server

```bash
python3 -m http.server 8000
```

### Step 2 — Start Wireshark

Wireshark was opened and the active network interface was selected.

Packet capture was started before generating test traffic.

### Step 3 — Generate Normal Request

```bash
curl http://127.0.0.1:8000/
```

Purpose:

Verify normal HTTP communication.

### Step 4 — Generate Resource Request

```bash
curl http://127.0.0.1:8000/index.html
```

Purpose:

Observe a request for a specific resource.

### Step 5 — Generate Failed Request

```bash
curl http://127.0.0.1:8000/not-found
```

Purpose:

Generate and analyze a 404 response.

### Step 6 — Generate Suspicious-Path Request

```bash
curl http://127.0.0.1:8000/.env
```

Purpose:

Generate a controlled request for a sensitive-looking resource path.

### Step 7 — Filter HTTP Traffic

Wireshark display filter:

```text
http
```

### Step 8 — Filter Suspicious Request

Wireshark display filter:

```text
http.request.uri == "/.env"
```

## 4. Observations

The packet capture was inspected to identify:

* HTTP request methods
* Requested resources
* Response status codes
* Source and destination information
* Request timestamps
* Repeated or unusual request paths

## 5. Expected Results

| Test            | Expected Observation                |
| --------------- | ----------------------------------- |
| GET /           | Successful HTTP request             |
| GET /index.html | Resource request                    |
| GET /not-found  | 404 response                        |
| GET /.env       | Suspicious-looking resource request |

## 6. Test Conclusion

The controlled tests successfully generated different HTTP request patterns that could be captured and inspected using Wireshark.

The methodology demonstrates the basic workflow used in network traffic analysis.

