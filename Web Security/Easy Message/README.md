## Easy Message
```
I Have a Message for you.
```
- Link: http://35.240.62.111/easymessage/


#### Solve:

- Step 1

    - First going to the robots.txt to know see if there is something interesting:
        ```
        http://35.240.62.111/easymessage/robots.txt
        ```
      
    - *robots.txt* content:
        ```
        User-agent: *
        Disallow: /?source
        ```
      
    - By going to this url:
        ```
        http://35.240.62.111/easymessage/?source  
        ```
    - We can see the php source:
        ```
        ...
        if ($user == base64_decode('Q3liZXItVGFsZW50') && $pass == base64_decode('Q3liZXItVGFsZW50')
            {
                success_login();
        ...
        ```
    - Decode the base64 chunk *Q3liZXItVGFsZW50*:
        ```
        Q3liZXItVGFsZW50 -> Cyber-Talent
        ```
    - Now we can login with user: Cyber-Talent and password: Cyber-Talent

- Step 2

    - After login we can see this message which is morse code encoded:
        ```
        ..-. .-.. .- --. -.--. .. -....- -.- -. ----- .-- -....- -.-- ----- ..- -....- .- .-. ...-- -....- -- ----- .-. ... ...-- -.--.- 
        ```
    - To decode this message we can go to [cryptii](https://cryptii.com/pipes/morse-code-translator):
        ```
        flag(i-kn0w-y0u-ar3-m0rs3) 
        ```
> **Flag: flag(i-kn0w-y0u-ar3-m0rs3) **