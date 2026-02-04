### 爬取豆瓣排名前250的电影并输出到txt文件里
```python
import requests
headers = {
    "User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/143.0.0.0 Safari/537.36"
}
#没有headers信息会被豆瓣拒绝
response = requests.get("http://movie.douban.com/top250",headers=headers)
# print(response)
# print(response.text)
f = open('text.txt','w',encoding='utf-8')
f.write(response.text)
f.close()
```
