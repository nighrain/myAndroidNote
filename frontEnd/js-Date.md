js-日期函数(Date)总结

### 获取日期

1. Date()
	——返回当日的日期和时间。
2. getDate()
	——从 Date 对象返回一个月中的某一天 (1 ~ 31)。
3. getDay()
	——从 Date 对象返回一周中的某一天 (0 ~ 6)。
4. getMonth()
	——从 Date 对象返回月份 (0 ~ 11)。
5. getFullYear()
	——从 Date 对象以四位数字返回年份。
6. getYear()
	——请使用 getFullYear() 方法代替。
7. getHours()
	——返回 Date 对象的小时 (0 ~ 23)。
8. getMinutes()
	——返回 Date 对象的分钟 (0 ~ 59)。
9. getSeconds()
	——返回 Date 对象的秒数 (0 ~ 59)。
10. getMilliseconds()
	——返回 Date 对象的毫秒(0 ~ 999)
11. getTime()
	——返回 1970 年 1 月 1 日至今的毫秒数。

### 设置日期

1. setDate()
	——设置 Date 对象中月的某一天 (1 ~ 31)。
2. setMonth()
	——设置 Date 对象中月份 (0 ~ 11)。
3. setFullYear()
	——设置 Date 对象中的年份（四位数字）。
4. setHours()
	——设置 Date 对象中的小时 (0 ~ 23)。
5. setMinutes()
	——设置 Date 对象中的分钟 (0 ~ 59)。
6. setSeconds()
	——设置 Date 对象中的秒钟 (0 ~ 59)。
7. setMilliseconds()
	——设置 Date 对象中的毫秒 (0 ~ 999)。
8. setTime()
	——以毫秒设置 Date 对象。

---

### 获取昨天的日期

```js
// getDay(-1,"-") 获取昨天日期
// getDay(0,"-") 获取今天日期
getDay(num,str){
  var today = new Date();
  var nowTime = today.getTime();
  var ms = 24*3600*1000*num;
  today.setTime(parseInt(nowTime+ms));
  var oYear = today.getFullYear();
  var oMoth = (today.getMonth() + 1).toString();
  if (oMoth.length <= 1) oMoth = '0'+oMoth;
  var oDay = today.getDate().toString();
  if(oDay.length <= 1) oDay = '0' + oDay;
  return oYear + str + oMoth + str + oDay;
},
```

---

日期格式化

> 前提知识点
>
>  [JavaScript RegExp.$1](https://www.cnblogs.com/baby-zhude/p/4126474.html)
>
> `RegExp`  是 `javascript` 中的一个内置对象。为正则表达式。
>
> `RegExp.$1` 是 `RegExp` 的一个属性,  `指的是与正则表达式匹配的第一个 子匹配(以括号为标志)字符串` ，以此类推， `RegExp.$2` ， `RegExp.$3` ，.. `RegExp.$99` 总共可以有99个匹配

```js
例子:
var r= /^(\d{4})-(\d{1,2})-(\d{1,2})$/; //正则表达式 匹配出生日期(简单匹配)
r.exec('1985-10-15');
s1=RegExp.$1;
s2=RegExp.$2;
s3=RegExp.$3;
alert(s1+" "+s2+" "+s3)//结果为1985 10 15
```









