# Web Application Security Lab

## Overview

This project demonstrates hands-on web application security testing against **OWASP Juice Shop**, an intentionally vulnerable application. The focus was on reconnaissance, endpoint discovery, and identification of security weaknesses in a controlled local environment.

## Lab Environment

| Component              | Details                          |
|------------------------|----------------------------------|
| Attacker Machine       | Kali Linux                       |
| Target Application     | OWASP Juice Shop                 |
| Deployment             | Docker                           |
| Target URL             | http://localhost:3000            |
| Scope                  | Local intentionally vulnerable application |

## Methodology

1. HTTP response and security header analysis
2. Client-side JavaScript and application resource discovery
3. API endpoint enumeration
4. Authentication and endpoint behavior testing
5. Directory and content enumeration
6. Validation and documentation of findings

## Reconnaissance Results

### Application Identification
The application was identified as OWASP Juice Shop through analysis of the HTTP response and page content.

### JavaScript & API Endpoint Discovery
The main JavaScript bundle was downloaded and reviewed. Multiple `/api/` and `/rest/` endpoints were identified, including routes related to:

- Authentication
- Products
- Basket / Cart
- User management
- Administrative functions

**Evidence:**
- `scans/http-headers.txt`
- `scans/homepage-response.txt`
- `scans/api-endpoint-discovery.txt`
- `scans/main.js`

## Key Security Finding

### Directory Listing / Information Disclosure

**Endpoint:** `http://localhost:3000/ftp/`

The `/ftp/` endpoint returned a publicly accessible directory listing containing multiple files, including:

- `incident-support.kdbx`
- `package.json.bak`
- `package-lock.json.bak`
- `suspicious_errors.yml`
- `encrypt.pyc`
- `announcement_encrypted.md`

**Impact:**  
Exposed directory listings can reveal filenames, backup files, application structure, and potentially sensitive information that may assist further attacks.

**Evidence:**
- `findings/directory-listing.txt`
- `scans/directory-listing.txt`

## Additional Testing Performed

The following tests were also conducted:

- Unauthenticated request to `/rest/user/whoami`
- Invalid login attempts
- Product search endpoint testing
- Basic input testing against the search functionality
- Review of client-side JavaScript for endpoint exposure

Normal application behavior was not treated as a vulnerability where no clear security impact was observed.

## Lessons Learned

- Web applications frequently expose useful information through HTTP responses and client-side JavaScript
- Systematic endpoint discovery helps map the application’s attack surface
- Directory listings can unintentionally expose sensitive or useful files
- Findings should always be validated and supported with reproducible evidence

## Skills Demonstrated

- Web application reconnaissance
- HTTP header and technology analysis
- Client-side JavaScript review
- API endpoint discovery
- Directory enumeration
- Manual verification of findings
- Clear documentation of security issues

## Disclaimer

This project was performed against a locally hosted, intentionally vulnerable OWASP Juice Shop instance for educational and portfolio purposes only. No unauthorized systems were targeted.
