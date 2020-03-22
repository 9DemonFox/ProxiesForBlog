## 检验代理是否可用
    Util/utilFunction.py
```buildoutcfg
def get_proxy():
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.149 Safari/537.36'
    }
    count = 1
    while True:
        try:
            response_dict = requests.get("http://127.0.0.1:5000/get/").json()
            proxy = "http://" + response_dict['proxy']
            response = requests.get(url='http://weibo.com/login.php',
                                    headers=headers,
                                    proxies={"http": proxy},
                                    timeout=5
                                    )
            if response.status_code == 200:
                return proxy
            else:
                print("状态码错误:{}".format(response.status_code))
                continue
        except Exception as e:
            print(e)
            print("{}尝试{}次".format(proxy, count))
            count += 1
            continue
```
根据上述代码改写请求函数
## 根据场景配置代理
> Util/utilFunction.py 修改校验函数 2020年3月22日11:07:01  
> Config/setting.py 中新增配置检测可用ip是否可用的间隔 2020年3月22日11:06:58
