### 例子1：随机验证码

> 设计一个生成随机验证码的函数，验证码由数字和英文大小写字母构成，长度可以通过参数设置。

```python
import string
import random

# code_len=int(input('请输入验证码长度：'))

def code_generate(code_len=4):
    allchar=string.digits+string.ascii_letters
    return ''.join(random.choices(allchar,k=code_len))
code=code_generate() #code=code_generate(code_len)
print(code)
```

### 例子2：判断素数
```python
num=int(input('请输入数字：'))
divisor=[]
def is_prime(num):
    for i in range(2,int(num**0.5+1)):
        if num%i==0:
            divisor.append(i)
            divisor.append(num//i)
    return divisor

if is_prime(num): print(f'{num}的因子是{divisor}')
else: print(f'{num}是素数')
```
