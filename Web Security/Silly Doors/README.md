## Silly Doors
```
Silly doors are so annoying .
```
- Link: http://ec2-35-158-236-11.eu-central-1.compute.amazonaws.com/silly/


#### Solve:

- Steps

    - After visiting the website, we will see a login page.

    - When viewing the page source, we can see that there is a path to sign up `signup.php`
        ```html
        <a href="signup.php" hidden class="txt3">Sign up now</a>
        ```

    - Now, lets go and sign up and login with the new account.

    - On log in, we can see a profile page presenting the user's name and email, and on the top corner there is a nav bar which contains settings options, let's take a look.

    - There is an option to change the user's password, let's fire up `burpsuite` and take a look at the request:

        ![capture](capture.PNG)

    - As we can see in the screenshot, the request sent has *userid* in it twice, one in the cookies and one in the posted data, lets change both to *0* as we guess that the *admin* is the first user.
    
    - Password changed successfully ! lets now try to log in with *admin:synv*, hmmm it didn't work.

    - How about changing it to *1* instead of *0* ? Yup, that is the one.

> **Flag: FLAG{Y0u_F0unD_My_iD0r!!}**