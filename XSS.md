
Cross-Site Scripting (XSS) Vulnerability

1. Identifying the XSS Vulnerability

The search box on the website was tested for input sanitization. Entering a basic XSS payload resulted in the payload being executed on the page, confirming the vulnerability.

Payload Used:

<script>alert('XSS');</script>

Upon submitting this payload in the search input field, the website displayed a pop-up box with the alert message, demonstrating that the input was not sanitized.

 


![image](https://github.com/user-attachments/assets/9aa68af3-51d3-4965-ba78-881dc127925a)

 

2. Exploiting the XSS Vulnerability

Stored XSS Example

For testing purposes, I identified a field where the payload could be stored in the database and executed when viewed by other users.
![image](https://github.com/user-attachments/assets/d4280002-2608-4678-b925-c608b26b9c12)


Example:

<script>document.cookie='stolen=' + document.cookie</script>

This payload was submitted into a comment section. When other users accessed the comments, their cookies were sent to my controlled server for simulation purposes (no actual harm caused).

Reflected XSS Example

The search field was exploited with a reflected XSS payload:

"><img src="x" onerror="alert('XSS Discovered')">

This triggered an alert message whenever the payload was processed in the response.













