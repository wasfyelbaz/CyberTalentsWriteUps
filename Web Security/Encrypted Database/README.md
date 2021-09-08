## Encrypted Database
```
The company hired an inexperienced developer, but he told them he hided the database and have it encrypted so the website is totally secure, can you prove that he is wrong ??
```
- Link: http://34.77.37.110//encrypted-database/

#### Solve:

- Steps

    - After connecting to the webpage, and viewing all the links there is no sign of a database.
    
    - Viewing the page source, we will notice a path *secret-admin*
        ```html
        <link rel="stylesheet" href="secret-admin/assets/style.css">
        ```
      
    - Going to the path, we will find a login page, but it's not very useful !
    
    - Viewing the page source again, we will notice a hidden input element.
        ```html
        <input type="hidden" name="db" value="hidden-database/db.json" />
        ```    
      
    - Going to the *hidden-database/db.json*, now we got an *MD5* hash !
      
    - By reverse searching on google, we can have the plain text value.
    
> **Flag: badboy**