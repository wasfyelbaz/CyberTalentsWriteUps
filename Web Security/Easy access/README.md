## Easy access
```
Only superpower makes you see unlimited view.
```
- Link: http://ec2-35-158-236-11.eu-central-1.compute.amazonaws.com/easy-access/ 


#### Solve:

- Steps

    - After connecting to the webpage, and viewing the page source we can see a comment with credentials.
        ```html
        </head>
        <!---user:bob,pass:password-->
        <body style="height:auto;margin:0 auto;padding:0 auto ;">
        ```

    - When we login with these credentials, we will see a message saying that only admins can see the flag !
    
    - Back at the login page, if we tried to type a *single quote* in the user field, a sql error will appear.
    
    - Now we knew that this form is vulnerable to sql injection, we can type something like this in both fields to login:
        ```
        ' or 1=1 -- -
        ```
      
    - Login successfully and now we can see the flag.
    
> **Flag: flag{!njection_3v3ry_wh3r3}**