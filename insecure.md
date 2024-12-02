
Brute Forcing password of user ‘Carlos’
Lab analysis :
- Lab is vulnerable due to a logic flaw in its password brute-force protection
-Valid username and password is provided
 
Lets login with given username and password. After logging in with given valid username and password, I looked around to see the application, there was not anything of interesting.
Lets intercept the request and work in burp suite.
![image](https://github.com/user-attachments/assets/25a2486c-2be0-4d7f-a52e-1bfea1cb6099)

 
Send this request to Repeater ctrl + R
 ![image](https://github.com/user-attachments/assets/126641b5-83a6-4b67-8ff8-420834d963c0)

In repeater, when i tried entering different password for carlos, web app is blocking brute-force attack.
Looking closely, I found after every 3 incorrect attempt website is blocking the attempt for 1 min.
But there is a catch.
If we can create a success full attempt in between the request then the attempt resets.
Incorrect attempt > Incorrect attempt >Incorrect attempt > Block
Incorrect attempt >Incorrect attempt > Correct attempt >Incorrect attempt > Correct attempt >Incorrect attempt >Incorrect attempt
so with this technique, we can bypass the brute force protection.
How can we create correct attempt after certain incorrect incorrect attempt
The answer is : we can create a macro in burpsuite.
macro will create a correct attempt after certain brute force attempt.
Lets get started
 ![image](https://github.com/user-attachments/assets/f8621029-20c8-4bbe-b759-a3d7b868ea9d)

Click on proxy setting
 ![image](https://github.com/user-attachments/assets/756a5a84-1a52-410b-9151-e9d909a6d572)

Then click on sessions and click add
![image](https://github.com/user-attachments/assets/15bf4a69-a98f-4cb3-a3ec-f801cbaeb3ba)

 
Then click on add and Run a macro
 ![image](https://github.com/user-attachments/assets/622bce21-f670-4dbb-b0d9-f02b7295f313)

Then select request with status code 302 : because this is the request where the login attempt is correct.
![image](https://github.com/user-attachments/assets/b2a884c3-82ec-47cf-8b13-fb808b2d8574)
 
Then click OK
![image](https://github.com/user-attachments/assets/1eff8923-4016-4f59-ba2f-7201ba406d03)

 
Then click OK
![image](https://github.com/user-attachments/assets/e7ee59c7-e04f-4476-9afc-fbcf75384e5e)

 
Then go to scope option
![image](https://github.com/user-attachments/assets/b82ea2c1-3d49-4667-bff1-413913828a0e)

 
Select Include all URLs and click ok
Then send the request from repeater to Intruder ctrl + I
![image](https://github.com/user-attachments/assets/63049df9-21c5-49eb-8c48-bd2fcee5ce52)

 
In intruder, set username carlos and set payload position on password field
make sure attack type is sniper
 ![image](https://github.com/user-attachments/assets/99ec5c45-c2bb-47ca-b2a1-0ffaa107e141)

In payload option.
- set payload option 1
- payload type Simple list
- and paste the password list ; password list is provided in lab
- ![image](https://github.com/user-attachments/assets/0eea140f-5ff1-4b12-921b-f64955ebd0f0)

 
Then go to Resource pool
- select create a new resource pool
- set maximum concurrent requests : 1
Then start attack
 ![image](https://github.com/user-attachments/assets/f724073a-2153-47df-be33-7179f0b8770b)

And we can see, after multiple tries , the is no brute force blockage
  ![image](https://github.com/user-attachments/assets/970aea1c-7a14-4057-adff-ad72de3aba7b)
Looking at the status code, we can see we got 302 status code. Which is the required password.
Lets try to login and check if it is correct:

![image](https://github.com/user-attachments/assets/c66fe837-83bb-4f9f-8abe-fc7a2ec41f74)
![Uploading image.png…]()

 

