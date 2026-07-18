# Day 049 - Downloading Files with `wget` and `curl`

## 🧠 Introduction

Linux provides several tools for downloading data from the internet.

The two most commonly used are:

- `wget`
- `curl`

Although both can retrieve data from remote servers, they are designed for different purposes.

Generally:

- `wget` is best for downloading files.
- `curl` is best for communicating with web services and APIs.

Every Linux administrator, developer, and DevOps engineer uses these commands regularly.

---

# wget

`wget` is a command-line download utility.

Basic syntax:

```bash
wget URL
```

Example:

```bash
wget https://example.com/file.zip
```

The downloaded file is saved in the current directory.

---

# Saving with a Different Name

Use:

```bash
wget -O backup.zip https://example.com/file.zip
```

Option:

```text
-O = Output filename
```

This allows you to choose the saved filename.

---

# Resuming Downloads

If a large download is interrupted:

```bash
wget -c https://example.com/ubuntu.iso
```

Option:

```text
-c = Continue download
```

Only the missing data is downloaded.

---

# Background Downloads

Download without keeping the terminal occupied:

```bash
wget -b https://example.com/archive.tar.gz
```

Option:

```text
-b = Background mode
```

The download continues even after returning to the shell.

---

# Download an Entire Website

Mirror a website:

```bash
wget --mirror https://example.com
```

This recursively downloads the site's content.

This option is useful for backups or offline browsing.

---

# curl

Unlike `wget`, `curl` is primarily designed for transferring data between systems.

Basic request:

```bash
curl https://example.com
```

Instead of saving a file, `curl` displays the response in the terminal.

---

# Save Output to a File

```bash
curl -o page.html https://example.com
```

Option:

```text
-o = Output filename
```

---

# Follow Redirects

Some websites redirect requests.

Use:

```bash
curl -L https://example.com
```

Option:

```text
-L = Follow redirects
```

Without this option, you may only receive the redirect response.

---

# Display HTTP Headers

View response headers:

```bash
curl -I https://example.com
```

Example output:

```text
HTTP/2 200 OK

Content-Type: text/html

Content-Length: 1256
```

This is useful for debugging web servers.

---

# Download a File

`curl` can also download files:

```bash
curl -O https://example.com/image.png
```

Option:

```text
-O = Keep original filename
```

---

# Sending POST Requests

Many APIs require POST requests.

Example:

```bash
curl -X POST https://example.com/api
```

Send JSON data:

```bash
curl -X POST \
-H "Content-Type: application/json" \
-d '{"name":"Alice"}' \
https://example.com/api/users
```

This is common when interacting with REST APIs.

---

# Comparing wget and curl

| Feature | wget | curl |
|---------|------|------|
| Download files | ✅ | ✅ |
| Resume downloads | ✅ | Limited |
| Recursive downloads | ✅ | ❌ |
| REST API support | Limited | Excellent |
| Custom HTTP methods | Limited | ✅ |
| HTTP headers | Basic | Excellent |
| Upload data | ❌ | ✅ |

Rule of thumb:

- Download files → `wget`
- Work with APIs → `curl`

---

# Real-World Examples

Download Ubuntu:

```bash
wget https://releases.ubuntu.com/latest.iso
```

Resume a download:

```bash
wget -c backup.tar.gz
```

View a website's headers:

```bash
curl -I https://github.com
```

Download an image:

```bash
curl -O https://example.com/logo.png
```

Test a REST API:

```bash
curl https://api.github.com
```

Upload JSON:

```bash
curl -X POST \
-H "Content-Type: application/json" \
-d '{"status":"ok"}' \
https://example.com/api
```

These commands are frequently used by developers and system administrators.

---

# Common Mistakes

### Using wget for APIs

While possible, `wget` is not ideal for API testing.

For APIs, prefer:

```bash
curl
```

---

### Forgetting Redirects

Many websites redirect HTTP requests.

Instead of:

```bash
curl https://example.com
```

use:

```bash
curl -L https://example.com
```

---

### Confusing `-O` and `-o`

```text
-O → Keep the original filename.

-o → Specify your own filename.
```

Example:

```bash
curl -O https://example.com/file.txt

curl -o notes.txt https://example.com/file.txt
```

---

# Why `wget` and `curl` Matter

Imagine you are deploying a web application.

You need to:

- Download software packages
- Test an API
- Verify server responses
- Upload configuration data

Instead of opening a browser, you can perform all these tasks directly from the terminal.

This makes automation possible through shell scripts and CI/CD pipelines.

---

# 🎯 Summary

`wget` and `curl` are essential networking tools.

Common commands:

```bash
wget https://example.com/file.zip

wget -c file.iso

wget -O backup.zip URL

curl https://example.com

curl -O image.png

curl -o page.html URL

curl -I https://example.com

curl -L https://example.com

curl -X POST \
-H "Content-Type: application/json" \
-d '{"name":"Alice"}' \
https://example.com/api
```

Important options:

```text
wget

-c      Resume download

-b      Background download

-O      Output filename

-------------------------

curl

-O      Keep original filename

-o      Custom output filename

-L      Follow redirects

-I      Show HTTP headers

-X      Specify HTTP method

-H      Add HTTP headers

-d      Send request data
```

Mastering `wget` and `curl` enables efficient file downloads, API testing, automation, server diagnostics, and interaction with modern web services.
