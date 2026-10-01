# Web Application Security Lab

## Objective

Perform hands-on web application security testing against OWASP Juice Shop, an intentionally vulnerable application, and document reconnaissance results and identified security issues.

## Lab Environment

- Attacker: Kali Linux
- Application: OWASP Juice Shop
- Deployment: Docker
- Target: `http://localhost:3000`
- Scope: Local intentionally vulnerable application

## Methodology

1. HTTP response and security-header reconnaissance
2. Application and JavaScript resource discovery
3. API endpoint discovery
4. Authentication and endpoint behavior testing
5. Web directory/content enumeration
6. Validation and documentation of security findings

## Reconnaissance

The application was identified as OWASP Juice Shop through its HTML response.

The main JavaScript bundle was downloaded and reviewed for application endpoints. Multiple `/api/` and `/rest/` endpoints were identified, including authentication, product, basket, user, and administrative routes.

Evidence:

- `scans/http-headers.txt`
- `scans/homepage-response.txt`
- `scans/api-endpoint-discovery.txt`
- `scans/main.js`

## Security Finding

### Directory Listing / Information Disclosure

**Endpoint:**
`http://localhost:3000/ftp/`

The `/ftp/` endpoint returned an accessible directory listing containing multiple files and directories.

Examples observed included:

- `incident-support.kdbx`
- `package.json.bak`
- `package-lock.json.bak`
- `suspicious_errors.yml`
- `encrypt.pyc`
- `announcement_encrypted.md`

### Impact

Exposed directory listings can disclose filenames, backup files, application structure, and potentially sensitive information that may assist further attacks.

### Evidence

- `findings/directory-listing.txt`
- `scans/directory-listing.txt`

## Additional Testing

The following tests were also performed:

- Unauthenticated `/rest/user/whoami` request
- Invalid login request
- Product search endpoint testing
- Basic input testing against the product search endpoint
- JavaScript/API endpoint discovery

These tests were documented without treating normal application behavior as vulnerabilities where no evidence of a security issue was observed.

## Lessons Learned

- Web applications expose useful information through HTTP responses and client-side JavaScript.
- Endpoint discovery can reveal the application's attack surface.
- Directory listings can expose files that should not be publicly accessible.
- Security findings should be validated and supported with reproducible evidence.

## Disclaimer

This project was performed against an intentionally vulnerable OWASP Juice Shop instance running locally for educational and portfolio purposes. No unauthorized systems were targeted.
