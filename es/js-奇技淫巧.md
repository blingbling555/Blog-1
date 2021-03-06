# js 奇迹淫巧

## 1 js浮点数计算

time: 2018.12.01

`0.1 + 0.2 = 0.30000000000000004`

****

首先看计算机如何存储数：计算机是以二进制存储数据，在10进制编码之后，运算也会转为2进制进行运算，那么我们写的十进制是如何转二进制的呢？  

1. 整数 `除二取余` : `13` 对应的二进制数为 `1101`
2. 小数 `乘二取整` : `0.1` 对应的二进制数为 `0.000110011001100`无限循环，在某个精度点就舍弃

> 问：为什么整数就是 `除二取余` 呢？  
> 答：十进制转二进制，现在是满二进一，除二取余数，表示已经出不尽了；反过来二进制转十进制，整数部分一次乘以 `2^0, 2^1, ...` ，小数部分依次乘以 `2^-1, 2^-2, ...`。小数部分是从 `-1` 开始，整数部分是从 `0` 开始。  
> 问：为什么小数就是 `乘二取整` 呢？  
> 答：只是最终的一个规律，十进制转二进制，同整数部分一样，直接除，只不过是除的是 `2^-1` ， 所以直接就是乘2了；取整，因为小数会再向下借一位  
> 例子：二进制 `0.00011` 如何转十进制？  
> 答：整数部分：`0*2^0 = 0`，小数部分：`0*2^-1 + 0*2^-2 + 0*2^-3 + 1*2^-4 + 1*2^-5 = 1/16 + 1/24 = 5/48 ~ 0.1`

所以，首先要明确的是，小数 0.1 , 0.2 之类的不能整除5的(0.5*2=1，能取整)，都不能在计算机中完整存储，会在某个精度被舍弃

****

来看 `0.1 +0.2` 怎么计算 : `0.0001100110011 + 0.0011001100110 = 0.0100110011001`，转成10进制为 `1/4 + 1/32 + 1/64 + 1/512 + ... ~ 0.30000000000000004`

****

现在问题来了，那为什么 `0.1+0.1=0.2`、`0.1+0.3=0.4` ？  
既然存储都不能完整存储，算出来也不是没有小数的，他们为什么又能完整表示呢？

答：这是语言的处理问题，不仅仅是 javascript ， c 系语言也是一样的。

****

```javascript
// 小数相加
var arr = [0.2, 0.1];
const numberPlus = (arr)=> {
	return arr.reduce(function (pre, value) {
				let len1 = pre.toString().split('.')[1] || '';
				let len2 = value.toString().split('.')[1] || '';
				let maxLen = Math.pow(10, Math.max(len1.length, len2.length))
				return (pre * maxLen + value * maxLen) / maxLen
	})
}
```

## 2 退出循环

1. for 语句： `break;`
2. forEach 一类： `throw new Error('error')`

> 问：为什么 forEach 不能使用 break 跳出循环？  
> 答：设计的目的就不是用于跳出循环，它是用于遍历所有的项，如果想跳出，最好使用 for 循环。  
> 问：使用 `return ;` 在 forEach 循环中，属于跳出循环吗?  
> 答：不属于。每轮循环还是会走，只是说走到满足条件执行 `return ;` 时，回调函数返回空，然后还是会继续循环下去。
