## Newsletter
```
the administrator put the backup file in the same root folder as the application, help us download this backup by retrieving the backup file name
```

## Solve:

- After visiting the webpage, you'll see a form that requires an email.


- Enter any input to see if there are any restrictions, you will find that you have to enter an email address with the correct format to proceed.


- Try inputting anything again but this time adding a *"@."* after your entry, you'll find that you are able to successfully input a string


- I tried to SQL injection, but it didn't succeed ...


- Trying a different approach
    ```
    `whoami` && @.
    ```
    - Results:
    ```
    www-data
    ```


- Now we know that it works, so we can try to *"ls"*
    ```
    `ls` && @.
    ```
    - Results:
    ```
    emails_secret_1337.txt hgdr64.backup.tar.gz index.php
    ```


- Considering the challenge description, we can understand that the flag is the name of the backup file.

> **Flag: hgdr64.backup.tar.gz**