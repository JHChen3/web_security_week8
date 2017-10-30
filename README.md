# Project 8 - Pentesting Live Targets

Time spent: 8 hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:
* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each version of the site has been given two of the six vulnerabilities. (In other words, all six of the exploits should be assignable to one of the sites.)

## Blue

Vulnerability #1: SQL Injection

https://user-images.githubusercontent.com/21267287/32150099-5dfab1f2-bce4-11e7-8956-9963b21b817b.gif

In the Salesperson section, there is "?id=X" at the end of the url, by entering a ' after X (X can be from 1 to 9), the blue section will show "Database query failed" while the green and red sections just redirect. This indicates that the blue section has SQLI vulnerability. I use "?id=' OR SLEEP(3)=0--'" to testify it.

Vulnerability #2: Session Hijacking/Fixation

https://user-images.githubusercontent.com/21267287/32150100-5e052de4-bce4-11e7-9b6e-ebe8651f6356.gif

Login to the blue Globitek website, use the tool provided (public/hacktools/change_session_id.php) to get the session id. Then open another browser and set the session id to that session id, you will find that the website on another browser is also logined. 

## Green

Vulnerability #1: Username Enumeration

https://user-images.githubusercontent.com/21267287/32150103-634860fa-bce4-11e7-8445-4de62232ff4b.gif

In the login page, when trying to login using a wrong username, the message is in plain text, but when tring to login using a correct username, the message appeared is bold. By inspecting the page, it is found that one class is "failed", while another class is "failture".

Vulnerability #2: Cross-Site Scripting

https://user-images.githubusercontent.com/21267287/32150104-63530d84-bce4-11e7-93dd-e58eefd8bb9d.gif

In the Contact Us page, the script can be entered in Your Name and Feedback. For example, entering <script>alert('Jin Hui found the XSS!')</script> in both Your Name and Feedback, then go to feedback section in Staff Menu, the alert "Jin Hui found the XSS!" will appear twice.

## Red

Vulnerability #1: Insecure Direct Object Reference

https://user-images.githubusercontent.com/21267287/32150105-6868b936-bce4-11e7-9297-6cde9eae32cd.gif

In the Salesperson section https://104.198.200.7/red/public/salesperson.php?id=X, by setting X to be 10 or 11 will give two people that can't be found in Find a Salesperson section. 

Vulnerability #2: Cross-Site Request Forgery

https://user-images.githubusercontent.com/21267287/32184754-a22d2848-bd73-11e7-9534-5d68f50a9bdc.gif

When trying to edit the information after changing the csrd_token, red section is still able to make a change, while the other two sections show "Error: invalid request".


## Bonus Objective 2: Build on Objective #4 (Cross-Site Scripting)

https://user-images.githubusercontent.com/21267287/32192064-781b0bb8-bd89-11e7-891a-5476b45c62d4.gif

In green section, type in <script>document.location="https://www.google.com"</script> in Feedback in Contact Us, then go to the feedback section in Staff Menu, it should direct the page to google. Additionally, type in <script>alert(document.cookie)</script> may read the cookie data and type in <script>document.cookie="username=abcde"</script> may set the cookie data.


## Notes

Describe any challenges encountered while doing the work
