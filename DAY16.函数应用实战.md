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
### 例子3：最小公倍数和最大公约数
我写的，为什么这么长
```python
a=int(input('请输入第一个数字：'))
b=int(input('请输入第二个数字：'))

def max_divisor(a,b):
    i=a
    while a%i!=0 or b%i!=0:
        i=i-1
    return i

def min_multiple(a,b):
    num=1
    while (num*a)%b!=0:
        num+=1
    return num*a

if a<=b:
    divisor= max_divisor(a,b)
    multiple= min_multiple(b,a)
else: 
    divisor= max_divisor(b,a)
    multiple= min_multiple(a,b)

print(f'{a}和{b}的最大公约数是{divisor}，最小公倍数是{multiple}')
```
看看人家写的，有算法，好简洁
```python
def lcm(x: int, y: int) -> int:
    """求最小公倍数"""
    return x * y // gcd(x, y)


def gcd(x: int, y: int) -> int:
    """求最大公约数"""
    while y % x != 0:
        x, y = y % x, x
    return x
```
