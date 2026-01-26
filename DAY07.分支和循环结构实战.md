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
### CRAPS赌博游戏

> **说明**：CRAPS又称花旗骰，是美国拉斯维加斯非常受欢迎的一种的桌上赌博游戏。该游戏使用两粒骰子，玩家通过摇两粒骰子获得点数进行游戏。简化后的规则是：玩家第一次摇骰子如果摇出了 7 点或 11 点，玩家胜；玩家第一次如果摇出 2 点、3 点或 12 点，庄家胜；玩家如果摇出其他点数则游戏继续，玩家重新摇骰子，如果玩家摇出了 7 点，庄家胜；如果玩家摇出了第一次摇的点数，玩家胜；其他点数玩家继续摇骰子，直到分出胜负。为了增加代码的趣味性，我们设定游戏开始时玩家有 1000 元的赌注，每局游戏开始之前，玩家先下注，如果玩家获胜就可以获得对应下注金额的奖励，如果庄家获胜，玩家就会输掉自己下注的金额。游戏结束的条件是玩家破产（输光所有的赌注）。

我自己写的，感觉层层叠叠。而且理解错游戏规则了，不管了。
```python
import random
sum=1000
player=False
dealer=False
t=0
continue_game=True
currentbet=0
while continue_game and sum>0:
    player=False
    dealer=False
    currentbet=int(input('Please place your bet:'))
    if sum-currentbet>=0:
        #round_1
        dice1=random.randint(1,6)
        dice2=random.randint(1,6)
        dice_r1=dice1+dice2
        print(f'第1轮掷骰点数为{dice_r1}')
        if dice_r1 in [2,3,7,11,12]:
            if dice_r1 in [7,11]:
                player=True
            elif dice_r1 in [2,3,12]:
                dealer=True
        else:
            dice_re=0
            i=2
            #round_re
            while player==False and dealer==False:
                dice1=random.randint(1,6)
                dice2=random.randint(1,6)
                dice_re=dice1+dice2
                print(f'第{i}轮掷骰点数为{dice_re}')
                if dice_re==7:dealer=True
                elif dice_re==dice_r1:player=True
                else: 
                    dice_r1=dice_re
                    dice_re=0
                    i=i+1
        if player==True or dealer==True:
            if player==True:
                bet=currentbet
                print('玩家胜')
            if dealer==True:
                bet=(-1)*currentbet
                print('庄家胜')
            sum=sum+bet
            t=t+1
            print(f'你已游戏{t}轮，你剩余筹码为：{sum}元')
            while sum>0:
                choice=input('是否继续？（Y/N）：').upper()
                if choice=='Y':
                    print('游戏继续')
                    break
                elif choice=='N':
                    print('游戏结束')
                    continue_game=False
                    break
                else:print('请输入Y/N')
    else:print(f'余额不足，当前余额{sum}元')
if sum==0:print('余额为0，游戏结束')
```
把标准答案放这里
```python
import random

money = 1000
while money > 0:
    print(f'你的总资产为: {money}元')
    # 下注金额必须大于0且小于等于玩家的总资产
    while True:
        debt = int(input('请下注: '))
        if 0 < debt <= money:
            break
    # 用两个1到6均匀分布的随机数相加模拟摇两颗色子得到的点数
    first_point = random.randrange(1, 7) + random.randrange(1, 7)
    print(f'\n玩家摇出了{first_point}点')
    if first_point == 7 or first_point == 11:
        print('玩家胜!\n')
        money += debt
    elif first_point == 2 or first_point == 3 or first_point == 12:
        print('庄家胜!\n')
        money -= debt
    else:
        # 如果第一次摇色子没有分出胜负，玩家需要重新摇色子
        while True:
            current_point = random.randrange(1, 7) + random.randrange(1, 7)
            print(f'玩家摇出了{current_point}点')
            if current_point == 7:
                print('庄家胜!\n')
                money -= debt
                break
            elif current_point == first_point:
                print('玩家胜!\n')
                money += debt
                break
print('你破产了, 游戏结束!')
```
