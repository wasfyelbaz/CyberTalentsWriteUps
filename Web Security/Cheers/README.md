## Cheers
```
Go search for what cheers you up
```
- Link: http://ec2-54-93-122-202.eu-central-1.compute.amazonaws.com/ch33r5/


#### Solve:

- Steps

    - After visiting the url, we can see a message saying:
        ```
        Notice: Undefined index: welcome in /var/www/html/ch33r5/index.php on line 14
        ```
      
    - I searched for this error and read a couple of articles on it, and I recommend [stechies](https://www.stechies.com/undefined-index-error-php/) and read about the error:

    - On reading and understanding, we can say that there is a variable *"welcome"* has no value assigned to it, But we can assign a value to it:
        ```
        ec2-54-93-122-202.eu-central-1.compute.amazonaws.com/ch33r5/index.php?welcome=SyncV  
        ```

    - Now we can see that the web page content changed nd it's saying hello to us, but there is another error occurred:
        ```
        Hello !!!
        Notice: Undefined index: gimme_flag in /var/www/html/ch33r5/index.php on line 19
        ```

    - As we did with *welcome* variable, we can do with the *gimme_flag* variable and assign a value to it:
        ```
        http://ec2-54-93-122-202.eu-central-1.compute.amazonaws.com/ch33r5/index.php?welcome=SyncV&gimme_flag=SyncV
        ```
    
    - Now we can see the flag:
        ```
        Hello !!!
        FLAG{k33p_c4lm_st4rt_c0d!ng}
        ```

> **Flag: FLAG{k33p_c4lm_st4rt_c0d!ng}**