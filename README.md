# vuePlugs_printjs
vue打印插件
**使用方法**

```
import Print from '@/plugs/print'
Vue.use(Print) // 注册
<template>
<section ref="print">
	打印内容
	<div class="no-print">不要打印我</div>
</section>
</template>
this.$print(this.$refs.print) // 使用
```
<font color=#c00 >注意事项</font>
需使用ref获取dom节点，若直接通过id或class获取则webpack打包部署后打印内容为空
**指定不打印区域**
方法一. 添加no-print样式类
```
<div class="no-print">不要打印我</div>
```
方法二. 自定义类名
```
<div class="do-not-print-me-xxx">不要打印我</div>
this.$print(this.$refs.print,{'no-print':'.do-not-print-me-xxx'}) // 使用
```


# 其他打印方法

```
//打印  domID为div#id
Vue.prototype.$printDom = function (domID) {
  var headhtml = "<html><head><title></title></head><body>";
  var foothtml = "</body>";
  // 获取div中的html内容
  var newhtml = document.all.item(domID).innerHTML;
  // 获取div中的html内容，jquery写法如下
  // var newhtml= $("#" + domID).html();

  // 获取原来的窗口界面body的html内容，并保存起来
  var oldhtml = document.body.innerHTML;

  // 给窗口界面重新赋值，赋自己拼接起来的html内容
  document.body.innerHTML = headhtml + newhtml + foothtml;
  // 调用window.print方法打印新窗口
  window.print();

  // 将原来窗口body的html值回填展示
  document.body.innerHTML = oldhtml;
  // 刷新解决页面无法点击
  window.location.reload();
  return false;
}
```
