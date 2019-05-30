vue中格式化时间

---

-  <https://www.cnblogs.com/xiaolanschool/p/9682275.html>
- data.js 格式化方法使用 *

```js
// 对Date的扩展，将 Date 转化为指定格式的String
// 月(M)、日(d)、小时(h)、分(m)、秒(s)、季度(q) 可以用 1-2 个占位符，
// 年(y)可以用 1-4 个占位符，毫秒(S)只能用 1 个占位符(是 1-3 位的数字)
// (new Date()).Format("yyyy-MM-dd hh:mm:ss.S") ==> 2006-07-02 08:09:04.423
// (new Date()).Format("yyyy-M-d h:m:s.S")      ==> 2006-7-2 8:9:4.18
Date.prototype.Format = function (fmt) {
    var o = {
        "M+": this.getMonth() + 1,                 //月份
        "d+": this.getDate(),                    //日
        "h+": this.getHours(),                   //小时
        "m+": this.getMinutes(),                 //分
        "s+": this.getSeconds(),                 //秒
        "q+": Math.floor((this.getMonth() + 3) / 3), //季度
        "S": this.getMilliseconds()             //毫秒
    };
    if (/(y+)/.test(fmt))
        fmt = fmt.replace(RegExp.$1, (this.getFullYear() + "").substr(4 - RegExp.$1.length));
    for (var k in o)
        if (new RegExp("(" + k + ")").test(fmt))
            fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
    return fmt;
}   

export function formatTimeToStr(times, pattern) {
    var d = new Date(times).Format("yyyy-MM-dd hh:mm:ss");
    if (pattern) {
        d = new Date(times).Format(pattern);
    }
    return d.toLocaleString();
}
```

- vue中过滤器使用 *

```vue
<template>
  <div>
  	<span>{{date | formatDate}}</span>
  </div>
</template>
import {formatDate} from './js/date.js';
  export default {
    date() {
        return {
            date: 1496311370052
        }
    },
  filters: {
   formatDate: function(time) {
        if(time!=null&&time!="")
        {
          var date = new Date(time);
          return formatTimeToStr(date, "yyyy-MM-dd");
        }else{
          return "";
        }
      }
  }
```

v-model中格式化时间（过滤器就失效了）
通过对于数组就遍历得到每项的时间，或者对每个对象的时间，然后进行格式化

```vue
<template>
  <div>
    <ul>
     <li v-for="item in arr">
       <input type="text" v-model="item.createTime" />
     </li>
    </ul>
  </div>
</template>
import {formatDate} from './js/date.js';
  export default {
    date() {
        return {
            date: 1496311370052
        }
    },
   mounted:{
    this. axios.get('/user', {
          params: {
            ID: 12345
          }
        })
    .then(function (res) {
        this.arr = res.body;
            for(var i=0; i<this.arr.length; i++){
              this.arr[i].createTime = formatTimeToStr(this.arr[i].createTime, 'yyyy-MM-dd')
            }
        })
       }
 }
```



