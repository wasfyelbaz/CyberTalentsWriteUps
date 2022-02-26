## admin gate first
```
Flag is safe in the admin account info
```

## Solve:

- After visiting the website, we will see a login page with test credentials as shown.
    ![Website snapshot](image-1.png)


- After login with these creds, we will see a normal welcome page, let's see what the cookies look like.
    ```
    eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJkYXRhIjoie1widXNlcm5hbWVcIjpcInRlc3RcIixcInJvbGVcIjpcInVzZXJcIn0ifQ.XSPy0jZd8CEtHl2e3C1SjPaewco1tjO3iajbkJy2OFQ
    ```


- As we can se it's a *JWT* token, to decode the token [jwt.io](https://jwt.io/) is the place to go to.
We can now see in the payload section the decoded value of the token.
Before preceding, I recommend to read about *JWT* tokens if you didn't see it before.
    ![Website snapshot](image-2.png)


- First, thing comes in mind is to bruteforce the token key, there is a wonderful jwt key bruteforcing tool called [*jwt-cracker*](https://github.com/lmammino/jwt-cracker). 


- To install *jwt-cracker*
    ```commandline
    > sudo npm install jwt-cracker
    ```


- Usage:
    ```commandline
    > jwt-cracker <token> [<alphabet>] [<maxLength>]
    ```


- In our case, we can just bruteforce with numbers to shorten the way as it took a long time to find the key
    ```
    > jwt-cracker "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJkYXRhIjoie1widXNlcm5hbWVcIjpcInRlc3RcIixcInJvbGVcIjpcInVzZXJcIn0ifQ.XSPy0jZd8CEtHl2e3C1SjPaewco1tjO3iajbkJy2OFQ" "1234567890"
    ```
    ![Website snapshot](image-3.png)


- In just 30 seconds, we were able to crack the key *123456*, now let's go verify the signature on [jwt.io](https://jwt.io/).
    ![Website snapshot](image-4.png)


- Nice, now we need to change the value of the role to admin, then copy the token and replace it with the one in the cookies then refresh, here you go the flag !

> **Flag: J!W!T#S3cr3T@2018**