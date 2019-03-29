## 第1题 给一个半径，求圆的面积和周长。圆周率为3.14

```python
#1. input
r = float(input("please input a r value: "))

#2. run
area = 3.14*r**2
c = 2*3.14*r

#3. output
print("area is :", area)
print("c is :", c)
```


## 第2题 输入两个数，比较大小后，从小到大升序打印
```python
#1. input
num1 = float(input("please input a number :"))
num2 = float(input("please input a number :"))

print(num1,num2)
#2. run
if num1 >= num2:
    print(num2, num1)
else:
    print(num1, num2)
```

## 第3题 输入一个成绩分数，判断学生成绩等级，A至E，其中，90分以上为'A'，80~89分为'B'， 70~79分为'C'，60~69分为'D'，60分以下为'E'  
```python
score = float(input("please input your score :"))

if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
elif score >= 60:
    print("D")
else:
    print("E")
```

## 第4题 死循环输入数字，输入后打印出之前输入的最大值和之前所有数字的平均数，如果输入的不是数字，而是quit字符串或者空格，则结束循环，退出程序。
```python
# 1. 输入数据

## 设置变量 全部输入数字累计之和tatalVal， 最大数maxNum， 循环次数 runCount

tatalVal = 0
maxNum = 0
runCount = 1

# 2. 进行计算和输出
while True:
    ## 第一步 从控制台中获取一个输入的数字字符串
    strNum = input("please input a number: ")

    ## 第二步 判断该字符串如果等于 “” “ ” “quit” 则退出while循环
    if strNum == "" or strNum == " " or strNum == "quit":
        print("game is over!")
        break

    ## 第三步 将strNum转换成int型数值 num
    num = int(strNum)

    ## 第四步 将num 和之前所有的数值和相加，更新tatalVal
    tatalVal = tatalVal + num

    ## 第五步 将全部数值之和 除以当前循环次数，算出平均值 avgNum
    avgNum = tatalVal / runCount

    ## 第六步 判断当前输入的 num 是否比之前的最大值大，如果大则进行maxNum重置为num
    if num > maxNum:
        maxNum = num

    ## 输出之前计算出的，平均值 avgNum 和 maxNum 和 循环次数runcount 
    print("avgNum = ", avgNum)
    print("maxNum = ", maxNum)
    print("runCount is : ", runCount)
    runCount = runCount + 1

```

## 第5题 用 `*` 打印一个边长为 n 的正方形，n 为整数。  
比如，当 n 为 3 时，打印的效果如下:  
```bash
    * * *
    * * *
    * * *
```

```python
# 1. 输入一个数字作为正方形的边长长度
num = int(input("please input a number: "))

# 2. 循环打印 num 行， 每行 连续打印 num 遍 “* ” 字符串 
for i in range(num):
    print("* "*num)
```

## 第6题 输入一个正整数n，求0到这个数以内的所有 奇数的和 与 偶数的和。
```python
#1. 输入一个数字作为求值的范围
num = int(input("please input a number: "))

## 初始化两个变量，奇数和oddNum， 偶数和evenNum
oddNum = 0
evenNum = 0

#2.  进行计算和输出

##  第一步设定循环内容，从1 到 num 个数
for i in range(1, num+1):
    ## 第二步 判断每一个数，如果被2整除没有余数，则证明是偶数，否则为奇数
    if i % 2 == 0:
        ## 第三步 i 若是偶数，则将i 与偶数和 求和
        evenNum = evenNum + i
    else:
        ## 第四步 i 若是奇数，则将i 与奇数和 求和
        oddNum = oddNum + i

#3. 输出运算的最终结果 oddNum 和 evenNum

print("oddval = ", oddNum)
print("evenNum = ", evenNum)
```


## 第7题

方法一:   求1到n的阶乘结果之和
```python
# 1 1*1

# 2 1*1*2

# 3 1*1*2*3

# 4 1*1*2*3*4

# 5 1*1*2*3*4*5

## 1. 输入一个数字作为阶乘的范围
num = int(input("please input a number: "))



### 第一步 初始化阶乘之和 tatalFac
tatalFac = 0

## 2. 进行求阶乘之和运算
for i in range(1, num+1):
    ### 第二步 求出每一个数字的阶乘
    fac = 1
    for j in range(1, i+1):
        fac = fac * j
    
    ### 第三步 将求出的阶乘之和 阶乘之和 tatalFac 求和
    tatalFac = tatalFac + fac

##3. 输出运算结果
print(tatalFac)
```

方法二： 求1道5的阶乘之和：  
```python
# 1 1*1

# 2 1*1*2

# 3 1*1*2*3

# 4 1*1*2*3*4

# 5 1*1*2*3*4*5

## 第一步 初始化阶乘之和tatalFac
tatalFac = 0
fac = 1

## 第二步 循环5次，i 之一次为 1 到 5
for i in range(1, 6):
    
    ## 第三步 分别求出 1 到 5 的阶乘值 fac
    fac = fac * i

    ## 第四步 将每个阶乘值与 阶乘和tatalFac 求和
    tatalFac = tatalFac + fac

## 输出最后的运算结果
print(tatalFac)
```

## 第8题 输入一个整数，判断他是否是素数。  
```python
#1. 输入一个数字，作为是否是素数的判断的对象

num = int(input("please input a number: "))

#2. 运算并输出结果

## 第一步 i 的值为 2到 num减一 
for i in range(2, num):

    ## 第二步 判断 num 是否可以被 除了1 和 他本身 整除
    if num % i == 0:
        ## 第三步 如果 num 可以被 i 整除，证明num 不是一个素数，结束循环
        print(i)
        print(num, " is not prime number !")
        break

## 第四步 最后 如果num 没有被 i 整除 则证明num 是一个素数
else:
    print(num, "is a prime number")

```
