# 关于冠亚OMS系统的TOKEN获取
``` python
def DEVOMSLogin(password:str="password", email:str="username"):
    headers = {
        "Content-Type": "application/json; charset=UTF-8",
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36",
    }
    url2=  "https://www.topasia.vip/gatewayApi/6003/sso/login"
    payload2 = {"password": "topasia2021","email": "Jamine@topasia.us"}
    response2 = requests.post(url2, headers=headers, json=payload2, verify=False)
    if response2.status_code == 200:  
      result = response2.json().get('result')  
      signId=result["signId"]
      print(signId)
    else:  
      print("请求失败，状态码:", response2.status_code)
    url =  "https://www.topasia.vip/gatewayApi/6003/sso/getToken"
    payload = {"signId": signId,"type": 0}
    response = requests.post(url, headers=headers, json=payload, verify=False)
    print(response.headers)
    print(response.headers.__dict__)
    token = response.headers.get('Token')
    print(f'DEVOMSLogin_token: {token}')
    return token
```

# 截图
![[Pasted image 20231214114221.png]]
signid：![[Pasted image 20231214113819.png]]
TOKEN：![[Pasted image 20231214113915.png]]
# 简述：
OMS系统登录分为两步，第一步是以账号密码作为请求体发出login请求，会得到signID返回值；第二部以第一步获取的signID作为请求体发出getTOKEN请求，得到该账号的TOKEN

