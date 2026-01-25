### 百钱百鸡问题
> **说明**：百钱百鸡是我国古代数学家张丘建在《算经》一书中提出的数学问题：鸡翁一值钱五，鸡母一值钱三，鸡雏三值钱一。百钱买百鸡，问鸡翁、鸡母、鸡雏各几何？翻译成现代文是：公鸡 5 元一只，母鸡 3 元一只，小鸡 1 元三只，用 100 块钱买一百只鸡，问公鸡、母鸡、小鸡各有多少只？
```python
for a in range(0,101):
    for b in range(0,101):
        if 5*a+3*b+(100-a-b)/3==100:
            print(f'a={a}, b={b}, c={100-a-b}')
```
我一开始想用while，没搞定，让deepseek研究研究。
**错误案例**：
```python
while 5*a+3*b+(100-a-b)/3!=100:
    for a in range(0,101):
        for b in range(0,101):

print(f'a={a}, b={b}, c={100-a-b}')
```
菜菜的很安心。DS说while语句使用了未初始化的a，b，然后就算定义了也不能用。正确写法如下。
双while循环
```python
a = 0
while a <= 20:  # 公鸡最多20只
    b = 0
    while b <= 33:  # 母鸡最多33只
        c = 100 - a - b
        if c % 3 == 0 and 5 * a + 3 * b + c // 3 == 100:
            print(f'公鸡: {a}只, 母鸡: {b}只, 小鸡: {c}只')
        b += 1
    a += 1
```
如果非要for&while嵌套
```python
a = 0

while a <= 20:
    for b in range(0, 34):  # while和for可以嵌套！
        c = 100 - a - b
        if c % 3 == 0 and 5 * a + 3 * b + c // 3 == 100:
            print(f'公鸡: {a}只, 母鸡: {b}只, 小鸡: {c}只')
            break  # 跳出for循环
    a += 1
```
