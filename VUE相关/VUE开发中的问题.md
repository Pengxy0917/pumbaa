# VUE开发中的问题


---
##关于v-show的问题
在tab里面 规定了v-show="" 但是在列表详情页需要隐藏的时候 只能隐藏一次 再次刷新也不可以隐藏 show已经是false了 但是还没有
当时以为是keepAlive的问题 结果发现不是
后来决定把show里面的变量移到router.js 里面的meta
```
meta:{ 
        isShow:true
    }
```
现在就成功了 但是还是出现了问题：由于keepAlive的原因 路由跳转的时候 在原来的界面 tab消失 然后再跳转到详情
keepAlive是必须的 原来详情页是tab的子页面 现在把他拿出去 差不多就好啦

##关于浮动的问题
用户名动态发布时间是float：left 如果没有规定用户名标签的长度 发布时间会随着用户名的长度发生变化 
**解决办法**
```
width:固定长度
```

##关于小图标的问题
在设置底部图标的时候 用到的是i标签 
```
i{
background: url('url') no-repeat//防止图标过小 重复
background-size:cover //将图片扩大或者缩放来适应整个容器 
}
```
##关于使用promise的问题
在写接口的时候
```
//暴露在外面的接口
export defualt(module,{method='get',url,data}) => {
 return new Promise((resolve,reject) => {
  let opt = { url,method }
  method === 'get'? opt.params =data : opt.data=data
  opt = {...module, ...opt}
  axios(opt)
  .then(res => { resolve(res.data) })
```
