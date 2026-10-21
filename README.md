# Lab 01 – File Path Traversal: Simple Case

## What Is It?

Path Traversal

If an application does not properly validate user-supplied file paths, an attacker may be able to access sensitive information, including:

1. Application source code and data.
2. Credentials used to access backend systems.
3. Sensitive system files.

## Target Goal

Retrieve the contents of the `/etc/passwd` file from the target server.

## How It Works

- **Normal request:** Requesting `218.png` retrieves an image from `/var/www/images/`.
- **The vulnerability:** The application does not properly validate the requested filename.
- **The attack:** Using `../../../etc/passwd` attempts to navigate up three directory levels to the filesystem root and access the `/etc/passwd` file.
- **The result:** If the application is vulnerable, the server may return the contents of `/etc/passwd`.

## Analysis

The vulnerability occurs because the application uses a user-controlled filename to access files without adequately restricting access to the intended directory.

The `../` sequence represents the parent directory. Repeating it allows navigation up multiple directory levels. By manipulating the filename parameter, an attacker may escape the intended image directory and read files elsewhere on the server.

**Key takeaway:** Always validate file paths and restrict file access to the intended directory to prevent path traversal vulnerabilities.


