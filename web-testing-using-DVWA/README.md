## Setup
I installed and set up DVWA (Damn Vulnerable Web Application) on my local machine. DVWA is an intentionally vulnerable application similar to WebGoat, designed for security testing and training. I ensured that the application was running locally and that I could log in successfully.
<img width="750" height="667" alt="image" src="https://github.com/user-attachments/assets/1e300a87-646c-461a-a0ba-2b36c1693b8f" />
<img width="450" height="343" alt="image" src="https://github.com/user-attachments/assets/ad275efd-9d42-46d3-b789-867597efd204" />

## Perform Basic Vulnerability Analysis
Using Burp Suite, I analyzed DVWA for common vulnerabilities. I focused on identifying three specific vulnerabilities:
 - SQL Injection
 - Cross-Site Scripting (XSS)
 - Cross-Site Request Forgery (CSRF)
<img width="750" height="478" alt="image" src="https://github.com/user-attachments/assets/d946dbf1-f848-4e49-ab2c-af8e72b42def" />

## SQL Injection
I tested the SQL Injection vulnerability by inputting the payload `1 OR '1'='1'` in the User ID field. Burp Suite captured the request, and the application processed it, confirming that it was vulnerable to SQL Injection.
<img width="750" height="377" alt="image" src="https://github.com/user-attachments/assets/3e5d0448-3007-46ed-8b63-a742b00e8756" />

## Cross-Site Scripting (XSS)
Next, I tested for XSS (Reflected). I injected a script payload into the input field: `<script>XSS by Rani</script>`. The application reflected the script back into the response without sanitization, confirming the vulnerability.
<img width="750" height="362" alt="image" src="https://github.com/user-attachments/assets/ba7aef04-7a2f-4654-aa65-b97e3fe6c9dc" />

## Cross-Site Request Forgery (CSRF)
Finally, I tested CSRF by crafting a malicious URL that automatically changes the admin password without user interaction. When accessed by an authenticated user, the password was changed successfully.
<img width="750" height="479" alt="image" src="https://github.com/user-attachments/assets/67698381-645f-4084-a5d2-c2adb3bce6bf" />
<img width="750" height="475" alt="image" src="https://github.com/user-attachments/assets/d0447bfc-d56c-4ad8-83f6-8fff41a44c1b" />
<img width="750" height="91" alt="image" src="https://github.com/user-attachments/assets/ce1f6ce9-b70b-4993-8702-88ca9ca78ffd" />
<img width="750" height="272" alt="image" src="https://github.com/user-attachments/assets/4e9e3746-1acd-4352-bddd-87e43d9ebf82" />

## Report
SQL Injection:
Discovery: Found by injecting '1 OR '1'='1' into input fields.
Danger: Attackers can manipulate the database, extract sensitive data, or bypass authentication.
Mitigation: Use prepared statements (parameterized queries) and input validation.

Cross-Site Scripting (XSS):
Discovery: Found by injecting <script>XSS by Rani</script> into a form field.
Danger: Allows attackers to execute arbitrary JavaScript in the victim’s browser, leading to session hijacking or data theft.
Mitigation: Sanitize and encode user input before reflecting it in responses.

Cross-Site Request Forgery (CSRF):
Discovery: Found by crafting a malicious URL that triggers a password change.
Danger: Attackers can trick authenticated users into performing unwanted actions on their behalf.
Mitigation: Implement CSRF tokens, enforce SameSite cookie policies, and verify request origins.

Conclusion:
This exercise demonstrated the exploitation of three common vulnerabilities: SQL Injection, XSS, and CSRF. Each of these issues poses significant risks if left unmitigated. By implementing secure coding practices such as input validation, parameterized queries, output encoding, and CSRF protection mechanisms, applications can be safeguarded against these attacks.
