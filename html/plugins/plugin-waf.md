﻿﻿Cloudopt Next comes with a recommended Waf plug-in, Waf can effectively prevent SQL injection attacks, XSS attacks, Mongodb injection attacks, and also supports a key to open the CSRF defense mechanism.

Cloudopt-next-web has been deeply integrated with cloudopt-next-waf without additional plug-ins.

````json
{
  "waf":{
    "plus": true,
    "csrf": false,
    "xss": true,
    "sql": true,
    "mongodb": true
  }
}
````

| Name     | Description|
|:--------:|:-------|
| plus| Add security-related settings in HTTP Heards.      |
| csrf| Enable the CSRF defense mechanism to prevent access.      |
| Xss| Turn on XSS defense.     |
| sql| Turn on SQL injection defense.      |
| mongodb| Turn on Mongodb Injection Prevention.      |

