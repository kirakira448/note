>官网：https://echarts.apache.org/zh/index.html
# 初始化
## 安装
```shell
npm install --save echarts
```
## 引入
1. 在plugins文件夹下创建`echarts.js`
```js
// echarts图表库 
import * as echarts from 'echarts'  
export default {
    // echarts挂载到vue全局
    install:(app)=>{
	    // 全局注册。$line:自定义名称，这里表示使用折线图
        app.config.globalProperties.$line=(element,data)=>{
	        /*
	        ** element:用于定位元素
			** data:用于动态传入数据，一般用于替换示例中的series值
	        */
            // 加载echarts图表
            var myChart=echarts.init(document.getElementById(element))
            const option={ 
				// 从官网示例复制
            }
            myChart.setOption(option)
        }
    }
}
```
2.  在`main.js`中引入
```js
//...
import echarts from './plugins/echarts'

//...
app.use(echarts)

//...

```
## 使用
1. 创建使用容器，一定要给一个id，因为在引入时使用了`document.getElementById`
```vue
<div class="line" id="line">
```
2. 调用`getCurrentInstance`方法，并且在加载完成dom后使用，避免找不到元素
```js
import { getCurrentInstance,onMounted } from 'vue' 
import api from "@/api/index.js"

const { proxy } = getCurrentInstance() 
onMounted(()=>{
    api.getLine().then(res=>{
        if(res.data.status===200){
            proxy.$line("line",res.data.result.lines)
        }
    }).catch(error=>{
        console.log(error);
    }) 
})
```

# 使用案例
## 使用地图
1. 在资源文件夹（assets）中导入地图json文件 ![[json.zip]]
2. 在`echarts.js`中引入，示例：引入中国地图
```js
//...
import china from "../assets/json/china.json"

export default {
    install: (app) => {
	    //...
		app.config.globalProperties.$china = (element, data) => {
			var myChart = echarts.init(document.getElementById(element))
			// 注册地图		
			echarts.registerMap("china",china)		
			const optison={		
				// 鼠标点击弹窗		
				tooltip:{		
					triggerOn:"click",  // 点击触发		
					enterable:true,     // 是否出现弹框		
				},
				visualMap:{
                    origin:"vertical",
                    type:"piecewise",
                    pieces:[
                        {min:0,max:0,color:"#fff"},
                        {min:0,max:10,color:"#fdfdcf"},
                        {min:10,max:20,color:"#fe9e83"},
                        {min:20,max:30,color:"#e55a4e"},
                        {min:30,max:40,color:"#4f070d"},
                        {min:40,max:100,color:"#ff0000"},
                    ]
                },		
				series:[{		
					name:"中国地图",		
					type:"map",		
					map:"china",		
					roam:false,     // 鼠标滚轮缩放		
					zoom:1.2,       // 默认地图倍数		
					label:{		
						show:true,  // 是否显示地图上的文本信息		
						fontSize:8  // 文本大小		
					},		
					itemStyle:{		
						areaColor:"rgba(255,255,255,1)",		
						borderColor:"rgba(0,0,0,0.2)"		
					},		
					data:[		
						{name:"内蒙古",value:10},		
						{name:"黑龙江",value:20},		
						{name:"山东",value:30},		
						{name:"河南",value:40},		
					]		
				}]		
			}		
			myChart.setOption(option);		
		}
    }
```
