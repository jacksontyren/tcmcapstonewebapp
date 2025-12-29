# Web Application Penetration Test – TCM Security Capstone

<img src="REPLACE_WITH_SCREENSHOT_URL" height="80%" width="80%">

<h2>Overview</h2>
<p>
This capstone project involved conducting a web application penetration test as part of the TCM Security <i>Practical Ethical Hacking</i> course. The objective was to simulate a real-world external attacker by identifying, exploiting, and documenting security weaknesses within a vulnerable web application. The engagement followed a structured offensive security methodology, emphasizing manual testing, exploit validation, and professional reporting.
</p>

<h2>Scope and Objectives</h2>
<li><strong>In Scope:</strong> Public-facing web application, authentication mechanisms, user input handling</li>
<li><strong>Out of Scope:</strong> Denial-of-Service attacks, social engineering</li>
<li><strong>Objectives:</strong> Identify exploitable vulnerabilities, demonstrate real-world impact, and provide remediation guidance</li>

<h2>Tools and Technologies Used</h2>
<li>Burp Suite (Proxy, Repeater, Intruder)</li>
<li>Browser Developer Tools</li>
<li>Manual HTTP request manipulation</li>
<li>Linux command-line utilities</li>
<li>OWASP Top 10 methodology</li>
<!-- <li>Custom payload crafting for exploit validation</li> -->

<br />

<h2>Penetration Testing Methodology</h2>
<p>
The assessment followed a structured offensive security workflow aligned with industry practices:
</p>
<li><strong>Reconnaissance:</strong> Application mapping, endpoint discovery, parameter identification</li>
<li><strong>Enumeration:</strong> Authentication flows, session handling, access control logic</li>
<li><strong>Vulnerability Identification:</strong> Injection flaws, broken authentication, misconfigurations</li>
<li><strong>Exploitation:</strong> Proof-of-concept exploitation and impact validation</li>
<li><strong>Post-Exploitation:</strong> Privilege escalation analysis and attack chaining opportunities</li>

<br />

<h2>Key Findings</h2>
<p>
The following vulnerability categories were identified and successfully validated during testing:
</p>
<li>Injection vulnerabilities (SQL Injection / Command Injection)</li>
<li>Broken authentication mechanisms</li>
<li>Insecure Direct Object References (IDOR)</li>
<li>Improper input validation</li>
<li>Sensitive information disclosure</li>

<br />

<p>
  <h2>Manual Testing Findings</h2>
<h3>Finding 1 — Allows Weak Passwords</h3>

Observation: A successful signup was performed using the username alex and password alex, indicating weak password acceptance. 

<br>


Finding 2 — Allows HTML Injection

Observation: A message parameter in the URL accepted and rendered unvalidated HTML content in the page. 

<br>


Finding 3 — Reflected Cross-Site Scripting (XSS)

Observation: A script payload placed in the URL was reflected back in the server response to the client. 

<br>


Finding 4 — Stored Cross-Site Scripting (XSS)

Observation: A script payload placed in a ratings field persisted and executed on refresh. 

<br>


Finding 5 — SQL Injection (SQLi)

Observation: SQL injection was validated in the coffee parameter through manual testing:

Attempted boolean logic injection patterns (e.g., or 1=1 style tests)

Confirmed union-based injection with 7 columns

Enumerated table names and column names via INFORMATION_SCHEMA 


SQLMap Validation & Data Extraction (Evidence of SQLi)

Command

sqlmap -r request2.txt -T users --dump


What this confirms

SQLMap identified coffee as injectable using:

boolean-based blind injection

time-based blind injection

UNION-based injection (7 columns) 


Result

Dumped the users table containing usernames, roles (admin/user), and password hashes.

Passwords were noted as cracked offline (post-exploitation step). 

<br>


Finding 6 — Unsafe File Upload

Observation: A captured POST request was modified to upload a PHP webshell file. The workflow included navigating to an admin function (admin/admin.php) and creating a new entry to support the upload flow. 

<br>

Finding 7 — Remote Code Execution (RCE) via Uploaded Webshell

Observation: After uploading a webshell, remote commands could be executed through the uploaded file. The write-up notes altering an uploaded filename (example: changing an image name to a PHP-executable name) to enable execution, and then confirming execution by refreshing and accessing the uploaded asset path. 


</p>
<br>
<br>

<h2>Risk Assessment</h2>
<p>
Each finding was evaluated based on exploitability, potential impact, and overall risk to the application. Vulnerabilities ranged from low to high severity, with higher-risk issues demonstrating unauthorized access and data exposure potential.
</p>

<br />

<h2>Remediation Recommendations</h2>
<li>Implement strong server-side input validation and output encoding</li>
<li>Enforce proper authentication and session management controls</li>
<li>Apply principle of least privilege to application roles</li>
<li>Harden application configurations and error handling</li>
<li>Align development practices with OWASP Top 10 mitigation guidance</li>

<br />

<h2>Reporting and Documentation</h2>
<p>
A formal penetration testing report was produced as part of the capstone, including an executive summary, technical findings, proof-of-concept evidence, risk ratings, and remediation recommendations. This mirrors professional deliverables used in real-world penetration testing engagements.
</p>

<br />

<h2>Conclusion</h2>
<p>
This project demonstrates hands-on experience conducting a complete web application penetration test using industry-standard tools and methodologies. The engagement reinforced offensive security fundamentals, manual testing techniques, and professional reporting practices essential for penetration testing and red team roles.
</p>
