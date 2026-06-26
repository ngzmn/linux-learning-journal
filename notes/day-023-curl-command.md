# Day 023 - Downloading Files and Working with APIs using curl

## 🧠 Introduction

The `curl` command is one of the most powerful networking tools in Linux.

Its name stands for:

```text
Client URL
```

Unlike `wget`, which focuses mainly on downloading files, `curl` is designed for transferring data using many different protocols.

Supported protocols include:

- HTTP
- HTTPS
- FTP
- SFTP
- SMTP
- LDAP
- MQTT

Developers and DevOps engineers use `curl` every day for:

- Testing APIs
- Downloading files
- Sending JSON data
- Debugging web services
- Automating deployments

---

## Basic Usage

Fetch a webpage:

```bash
curl https://example.com
```

The HTML content appears directly in the terminal.

---

## Downloading a File

Save a file locally:

```bash
curl -O https://example.com/file.zip
```

The `-O` option tells curl to use the original filename.

Example:

```text
file.zip
```

will be created in the current directory.

---

## Custom Output Names

Specify your own filename:

```bash
curl -o backup.zip https://example.com/archive.zip
```

Result:

```text
backup.zip
```

---

## Viewing HTTP Headers

Show response headers:

```bash
curl -I https://example.com
```

Example output:

```text
HTTP/2 200
content-type: text/html
server: nginx
```

This is extremely useful for debugging websites.

---

## Following Redirects

Some URLs redirect automatically.

Example:

```bash
curl http://github.com
```

To follow redirects:

```bash
curl -L http://github.com
```

The `-L` option means:

```text
Follow redirects
```

---

## Sending Data with POST Requests

One of curl's greatest strengths is interacting with APIs.

Example:

```bash
curl -X POST https://api.example.com/users \
     -d "name=John"
```

The `-X` option specifies the HTTP method.

The `-d` option sends data.

---

## Sending JSON Data

Modern APIs often use JSON.

Example:

```bash
curl -X POST https://api.example.com/users \
     -H "Content-Type: application/json" \
     -d '{"name":"John","age":30}'
```

Explanation:

```text
-H = HTTP header
-d = Request body
```

This workflow is common in backend development.

---

## Authenticating Requests

Send an authorization token:

```bash
curl -H "Authorization: Bearer TOKEN" \
     https://api.example.com/profile
```

This is widely used with REST APIs.

---

## Real-World Examples

Check your public IP address:

```bash
curl ifconfig.me
```

Download a Linux ISO:

```bash
curl -O https://releases.ubuntu.com/24.04/ubuntu.iso
```

Inspect website headers:

```bash
curl -I https://google.com
```

Test a local API:

```bash
curl http://localhost:3000/api/status
```

These are common developer tasks.

---

## curl vs wget

### wget

```bash
wget URL
```

Best for:

- Large downloads
- Recursive downloads
- Background downloads

---

### curl

```bash
curl URL
```

Best for:

- APIs
- HTTP requests
- Testing web services
- Sending JSON data

Developers often prefer `curl`, while system administrators may use both tools depending on the task.

---

## Common Mistakes

### Forgetting -L

Example:

```bash
curl http://github.com
```

may return a redirect message.

Instead:

```bash
curl -L http://github.com
```

---

### Confusing -O and -o

```bash
-O
```

uses the original filename.

```bash
-o
```

uses your custom filename.

---

### Incorrect JSON Formatting

Wrong:

```bash
-d {name:John}
```

Correct:

```bash
-d '{"name":"John"}'
```

Proper JSON syntax matters.

---

## 🎯 Summary

The `curl` command transfers data between systems and services.

Common examples:

```bash
curl https://example.com
curl -O URL
curl -o backup.zip URL
curl -I URL
curl -L URL
curl -X POST URL -d "data"
curl -H "Authorization: Bearer TOKEN" URL
```

Important options:

```text
-O  Save with original filename
-o  Save with custom filename
-I  Show headers
-L  Follow redirects
-X  Specify HTTP method
-H  Add headers
-d  Send request data
```

Learning `curl` is essential because modern software development, cloud platforms, and DevOps workflows rely heavily on APIs and HTTP communication.
