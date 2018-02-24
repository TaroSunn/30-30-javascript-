
# HTML

## [kbd 标签](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/kbd)
用于表示用户输入，它将产生一个行内元素，以浏览器的默认monospace字体显示。


# Javascript

1. 点击触发事件：
监听键盘事件
```
window.addEventListen('keydown',function(e){
  console.log('Hi')
})
```
2. 点击触发后播放音乐
在键盘事件中的回调函数,需要触发相应事件比如播放音乐的事件,改变css样式的事件
   1. [querySelector](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/querySelector)
      
      一般使用``querySelectory`` 获取相关类名、标签名、id名的元素。也可以获取整个标签
      
      例如：返回``<div class="user-panel main">标签中的<input name="login"/>``标签
      ```
      <div class="user-panel main">
      <input name="login"/> //这个标签将被返回
      </div>

      <script>
      var el = document.querySelector("div.user-panel.main input[name=login]");
      </script>
      ```
      在本例中``audio``获取的是键盘点击对应``audio``标签
    2. [模板字符串](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/template_strings)

        模板字符串使用反引号 (\` \`) 来代替普通字符串中的用双引号和单引号。模板字符串可以包含特定语法``(${expression})``的占位符。占位符中的表达式和周围的文本会一起传递给一个默认函数，该函数负责将所有的部分连接起来，如果一个模板字符串由表达式开头，则该字符串被称为带标签的模板字符串，该表达式通常是一个函数，它会在模板字符串处理后被调用，在输出最终结果前，你都可以通过该函数来对模板字符串进行操作处理。

        例如：
        ```
        var a = 1;
        var b = 2;
        //字符串拼接写法
        console.log("三是" + (a + b) + "不是" + (2 * a + b)); //"三是3不是4"
        //使用模板字符串的写法
        console.log(`三是${a + b}不是${2 * a + b}`); //"三是3不是4"
        ```
        在本例中``${event.keyCode}``,可以动态的获取按键对应的``audio``标签
    3. currentTime
      
        这个属性是设置当前的播放时间,如果不这只为0的话,那么当连续触发播放事件是,会等待当前音频播放完毕


```
function playSound (event){
  const audio = document.querySelector(`audio[data-key='${event.keyCode}']`)
  if(!audio) return
  const key = document.querySelector(`div[data-key='${evetn.keyCode}']`)
  if(!key) return
  audio.currentTime = 0
  audio.play()
  key.classList.add('playing')
}
```

3. 清除样式函数

  当点击元素的属性有``transform``时,移除类名``playing``。当然这里的属性也可以是``box-shadow``、``border-color``。但是这样写会出bug,当长时间按一个键时会自动加上``playing``,并且去不掉。但是去掉这个判断就不会发生这个问题。
```
function removeTransition (event) {
  <!-- if(e.propertyName !=='transform') return -->
  event.target.classList.remove('playing')
}
```
4. 调用清除样式函数

    1. 获取所有类名是``key``的元素,使用``Array.from``把获取到的类数组转成数组
    2. 监听``transitionend``,当元素完成``transition``时,触发清除样式函数 
```
const keys = Array.from(document.querySelectorAll('.key'))
keys.forEach(keys=>key.addEventListener('transitionend',removeTransition))
```

