# <p align="center">Header ig or sth like that</p>
![Image of Yaktocat](https://octodex.github.com/images/yaktocat.png)

The correct imports are import(ant).
```
import time
import hmac
import hashlib
import base64
import json
from urllib.parse import urlencode
```
Function for returning a header
```
# --- Returning a header for simple get api requests
def returnGetHeader (API_DATA, urlType, endUrl):
    now = int(time.time() * 1000)
    str_to_sign = str(now) + urlType + endUrl	
    signature = base64.b64encode(hmac.new(API_DATA['secret'].encode('utf-8'), str_to_sign.encode('utf-8'), hashlib.sha256).digest())
    passphrase = base64.b64encode(hmac.new(API_DATA['secret'].encode('utf-8'), API_DATA['passphrase'].encode('utf-8'), hashlib.sha256).digest())
    header = {"KC-API-SIGN": signature,
        "KC-API-TIMESTAMP": str(now),
        "KC-API-KEY": API_DATA['key'],
        "KC-API-PASSPHRASE": passphrase,
        "KC-API-KEY-VERSION": "2",
        "Content_Type": "application/json"
    }

    return header
```
