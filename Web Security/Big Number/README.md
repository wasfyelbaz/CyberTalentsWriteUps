## Big Number
```
a big number is needed to save the world
```
- Link: http://35.240.62.111/bignumber/


#### Solve:

- Steps

    - After connecting to the webpage, it will ask you to enter 3 numbers that exceed the value *999*.

    - If we clicked *source*, the source of the php will appear as shown below:
        ```
        <?php if (isset($_GET['password'])) {
            if (is_numeric($_GET['password'])){
                if (strlen($_GET['password']) < 4){
                    if ($_GET['password'] > 999)
                        die($flag);
                    else
                        print 'Too little';
                } else
                        print 'Too long';
            } else
                print 'Password is not numeric';
        }
        ?> 
        ```
    
    - After taking a look at the source code, I searched about the [*is_numeric*](https://www.php.net/manual/en/function.is-numeric.php) function in php, notice we can put the
    letter *e* as an exponential. Example: *2e2 = 4*
    
    - Now we knew how *is_numeric* function workd, we can put in the box a value that way more biger that 999 like:
        ```
        9e9
        ```
    
> **Flag: FLAG{Yes_Y0u_C4n_Use_Exp0nentiaL}**