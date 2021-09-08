## Back to basics
```
not pretty much many options. No need to open a link from a browser, there is always a different way
```
- Link: http://35.197.254.240/backtobasics


#### Solve:

- Steps

    - Tried to connect with `telnet`, `curl`, `httpie` but it was in vain.

    - Then tried to send a *POST* request with `curl`:
        ```commandline
        >> curl -X POST -d="data=data" http://35.197.254.240/backtobasics/index.php
      
        <!--
        var _0x7f88=["","join","reverse","split","log","ceab068d9522dc567177de8009f323b2"];function reverse(_0xa6e5x2){flag= _0xa6e5x2[_0x7f88[3]](_0x7f88[0])[_0x7f88[2]]()[_0x7f88[1]](_0x7f88[0])}console[_0x7f88[4]]= reverse;console[_0x7f88[4]](_0x7f88[5])
        -->
        ```

    - Nice we received some JavaScript code ! Now we can beautify it using [beautifier](https://beautifier.io/) and then save the code then run it using `nodejs`.
    ```commandline
    >> cat flag.js
    function reverse(_0xa6e5x2) {
        flag = _0xa6e5x2['split']('')['reverse']()['join']('');
        console.log(flag);
    }
    reverse('ceab068d9522dc567177de8009f323b2')
  
    >> nodejs flag.js
    2b323f9008ed771765cd2259d860baec
    ```
    
> **Flag: 2b323f9008ed771765cd2259d860baec**