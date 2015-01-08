# 向上融科前端代码规范
## 浏览器测试与支持
我们支持的浏览器为：IE8 +, Chrome, FireFox,  Opera, 360浏览器,  QQ 浏览器, 猎豹浏览器。
渐进退化，产品在 Chrome 及国内的 Chromium 内核浏览器上的体验应该做到最好，包括对圆角、阴影、渐变的支持，在 IE8 上可渐进退化，不建议通过 hack 的方式支持 CSS3 属性。
## HTML
### Doctype
使用标准的 HTML5 Doctype: 

```html
    <!DOCTYPE html>
```
### HTML 标签
应在 HTML 标签中指定文档的语言：

```html
<html lang="en-us">
    <!-- ... -->
</html>
```
### Meta 标签
在 Head 标签内应包含下列常用 meta 标签

* 字符编码：
```html
<meta charset="UTF-8">
```

* IE兼容模式：
```html
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```

### 标签使用
* 段落分隔符要使用用 `<p>` 标签，避免使用 `</ br>`。
* 列表元素必须放置在 `<ul>`, `<ol>` 或者 `<dl>` 中。
* 对于超过两层的 div 嵌套，必须在父级的 div 开始和结束的 div 后面添加注释，表示区块。

	```html
		<!-- START: 描述 -->
		<div>
    		<div>
        		<p> 嵌套超过两层，需要加上区块注释 </p>
    		</div>
		</div> <!-- END: 描述 -->
	```
* 不要把 table 作为页面布局使用
* 给每个表单里的字段加上 <label> 标签，其中的 for 属性必须和对应的输入字段对应。

### HTML 属性使用
* 所有的属性值都由双引号进行包裹，而非单引号, 且属性值必须加引号

	```html
		<!-- Not recommended -->
		<a class='maia-button maia-button-secondary'>Sign in</a>
		<!-- Recommended -->
		<a class="maia-button maia-button-secondary">Sign in</a>
	```
* 为了保证易读性，所有的属性按照下面的顺序进行书写
	1. id
	2. class
	3. name
	4. src, for, type, href
	5. title, alt
	6. data-*
	7. angular 相关
	7. aria-*, role
	
  整体思路是 id 标示单独的功能模块，class 为类，即一类可复用组件, 后面为当前标签的配置信息，最后是标签的数据信息，angular, Accessable 等附加属性。

* 不要为 Boolean 属性添加取值

	```html
		<input type="text" disabled>
		<input type="checkbox" value="1" checked>
		<select>
    	<option value="1" selected>1</option>
		</select>
	```

## CSS
### 总体原则
* 从外部文件加载CSS，尽可能减少文件数。加载标签必须放在文件的 HEAD 部分。
* 用 LINK 标签加载，永远不要用@import。
* 不要在文件中用内联式引入的样式，不管它是定义在`style`里还是直接定义在元素上。

### CSS 格式

* 为了代码的易读性，在每个声明块的左花括号前添加一个空格。
* 声明块的右花括号应当单独成行。
* 每条声明语句的 : 后应该插入一个空格。
* 为了获得更准确的错误报告，每条声明都应该独占一行。
* 所有声明语句都应当以分号结尾。
* 对于以逗号分隔的属性值，每个逗号后面都应该插入一个空格（例如，box-shadow）
* 对于属性值或颜色参数，省略小于 1 的小数前面的 0 （例如，.5 代替 0.5；-.5px 代替 -0.5px）
* 十六进制值应该全部小写，例如，#fff。
* 尽量使用简写形式的十六进制值，例如，用 #fff 代替 #ffffff。
* 为选择器中的属性添加双引号，例如，input[type="text"]。
* 避免为 0 值指定单位，例如，用 margin: 0; 代替 margin: 0px;

###  CSS 命名和组织
在这个规范中 CSS 的命名参照 bootstrap 和 [BEM](http://www.smashingmagazine.com/2012/04/16/a-new-front-end-methodology-bem/) 的风格。

* 在 bootstrap 中元素的命名可以简单的理解为： components-modifier, 例如 btn, btn-danger, btn-warning, dropdown, dropdonw-menu。
* 对于 BEM 来说， 将所有东西都划分为一个独立的模块,一个 header 是 block , header 里嵌套的搜索框是 block,甚至一个 icon 一个 logo 也是 block，block 可以相互嵌套。 BEM 最多只有 B+E+M 三级, modifier 是我们常用的 active, current 等来表示状态。

为了达到易用性和规范性两重标准，我们的 CSS 命名遵从下面的原则：

* 每个页面有一个页面 ID ，用于标示当前页面，这个页面 ID 不建议作为 CSS 选择器使用，除非是在某些特殊情况。每个 module 同样拥有 module ID, module ID 的作用同样不用于 CSS，一个 module 是由若干的 block 所构成， moduel ID 可用于个性化定制 block。
* 一个 block 是独立的实体，不依赖于任何其他任何 block, 可在页面的任何部分进行复用。
* 一个 element 是 block 的一部分，为了完成某个功能而存在。 element 具有上下文依赖性。
* modifier 是由于标示 block 或 element 的样式及大小变化的。
* 为了降低 CSS 继承的复杂度以及 SASS 的嵌套程度，可在 element 前加上 block 标识。
* 在 CSS 不要包含单独的标签名，若要用到该元素请给它起个名。
* 连接：blockName~elementName-modifier, 即将 bootstrap 中的 component 作为 block 来处理.即 block 和 element 之间的链接用 `__`, 同 modifier 的连接使用 `-`, 命名使用`_`分隔。
* 整体来说最后页面的 class 应该是可用抽象成一个 JSON 文件，来 cover 到所有的元素。
* CSS 的文件是以 block 为单位的，即存在：menu.css, menu-name.css, menu-name__elem-name.css。

	```html
		<ul class="menu">
  			<li class="menu__item">…</li>
  			<li class="menu__item">…</li>
		</ul>
	```
	
	```html
	<ul class="menu menu_size_big menu_type_buttons">
  		…
	</ul>
	```
	
	```html
	<div class="menu">
  		<ul class="menu__layout">
    		<li class="menu__layout_unit">
      			<div class="menu__item">Index</div>
   			</li>
    		<li class="menu__layout_unit">
      			<div class="menu__item menu__item_state_current">Products</div>
    		</li>
    		<li class="menu__layout_unit">
      			<div class="menu__item">Contact</div>
    		</li>
  		</ul>
	</div>
	```
	
常用的 block 名称

 block        | 作用 
------------  | ------------- 
attach        | 上传 block ，用于向 server 端上传文件或图像等。  
btn           | 按钮 
checkbox      | 选框 
checkbox-group| 复选框 
control       | 用于包裹 attach, btn 等的 block
dropdown      | 下拉框
icon          | 常用做背景用，例如 icon_social_weibo
image         | 图片标签 


## JavaScript
## SASS
## Angular



参考：

1. [BEM](http://bem.github.io/bem-method/html/all.en.html)
2. [SMACSS](http://smacss.com/book/)
3. [About HTML semantics and front-end architecture](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/)
4. [OOCSS](https://github.com/stubbornella/oocss/wiki)
5. [Modular CSS](http://thesassway.com/advanced/modular-css-typography)
6. [Google StyleGuide](https://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml)
7. [AngularJS StyleGuide - toddmotto](https://github.com/toddmotto/angularjs-styleguide)
8. [AngularJS StyleGuide - johnpapa](https://github.com/johnpapa/angularjs-styleguide)
9. [isobar code stand](http://coderlmn.github.io/code-standards/)
10. [Code Guide by @mdo](http://codeguide.co/)
11. [JavaScript Best Practices](http://www.thinkful.com/learn/javascript-best-practices-1/)
