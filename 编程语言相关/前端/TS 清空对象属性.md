
创建一个工具
```ts
export function tools_resetObjectKeys(obj:any) {
    let receiveObj = obj
    Object.keys(receiveObj).forEach((key) => {
        if (typeof (receiveObj[key]) === 'string') {
            obj[key] = '';
        } else if (typeof (receiveObj[key]) === 'number') {
            obj[key] = 0;
        } else if (typeof (receiveObj[key]) === 'object') {
            //数组也是object类型,js的数据类型可以简单分为以下几种，es新加的symbol以及谷歌67中的bigint这里未算进去
            //基本类型（单类型）：除Object。 也就是String、Number、boolean、null、undefined五种。
            //引用类型：object。里面包含的 function、Array、Date。
            Array.isArray(receiveObj[key]) ? receiveObj[key] = [] : receiveObj[key] = {};
            // Array.isArray判断是不是数组的方法
        }
    })
    return receiveObj
}
```

使用
```ts
import { tools_resetObjectKeys } from "@/utils/index";


this.userInfo=tools_resetObjectKeys(this.userInfo)
```