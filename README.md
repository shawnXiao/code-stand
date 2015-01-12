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
* 连接：blockName~elementName-modifier, 即将 bootstrap 中的 component 作为 block 来处理.即 block 和 element 之间的链接用 `__`, 同 modifier 的连接使用 `_`, 命名使用`-`分隔。
* 整体来说最后页面的 class 应该是可用抽象成一个 JSON 文件，来 cover 到所有的元素。
* CSS 的文件是以 block 为单位的，即存在：menu.css, menu-name.css, menu-name__elem-name.css。

	```html
		<ul class="menu">
  			<li class="menu__tem">…</li>
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
      			<div class="menu~item menu~item_state_current">Products</div>
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
首先需要给编辑器配置上 JSHint 或者 JSLint 插件。
### 基本格式
 1. 关于缩进: 不同的规范有不同的规定，比如在 jQuery Core Style Guide 中就指定了以 tabs 做为缩进。在 Google JavaScript Style Guide 中就以两个空格做为缩进。建议每一层使用四个空格做为缩进。

 2. 语句的终止(statement termination): 尽管在 javascript中 存在这自动加入分号机制(automatic semicolon insertion ASI),但是毕竟是自动档的，也有不靠谱的地方。例如下面 return 的例子，return 返回的是一个对象，在 return 后面进行了换行，根据 ASI 应该在 return 后面加入分号，这也就导致的某些不希望的事情发生。想要省略分号，那需要ASI相当的熟悉才行，所以对于一般的同学还是老老实实的在语句的结尾加上分号吧，防止出错。
 
 	```javascript
 function getData() {
 	return
    	{
        	title: "Maintainable JavaScript",
         	author: "Nicholars C.Zakas"
     	}    
 }
//JS引擎解析的结果
function getData() {
	return;
	{
		title: "Maintainable JavaScript",
		author:"Nicholars C.Zakas"
	}
}
 	```	
 
 	
3. 每一行的长度(line length) 一行 80 个字符的来源是因为老革命的文本编辑器，最大只能显示80列，多了的将不会被显示，建议还是尊重前辈们的意见吧，一行80个字符。

4. 换行(line Breaking): 当一行达到了最大的字符长度，就会涉及到人为换行的问题。建议是在操作符后面进行换行，换行后的新行，比前一行多两个单位的缩进。至于为什么建议要在操作符后进行换行，这里也会涉及到自动加分号机制（ASI）的问题。换行还有一个特殊情况需要考虑，为了考虑到可读性和给包裹行提供上下文，在赋值操作中，新的行应该和赋值的第一部分进行对齐。

	```javascript
//Good:在操作符后进行换行，下面的一行缩进两个级别
callAFunction(document, element, window, 
        "some string value");      
//Bad:下面的一行只有一个级别的缩进
callAfunction(document, element, window,
    "some string value");    
//Bad,在操作符之前换行
callAfunction(document, element, window
        ,"some string value");
	```
 

5. 空行(blank lines): 总的来说，代码应该是一段一段的像文章一样，而不是一坨文本，所以空行可以用来分隔不相关的代码。建议在下面的情况中进行加入空行：
	* 在方法之间；
	* 在方法的本地变量和方法的第一句之间；
	* 在多行和单行注释之前；
	* 在方法的逻辑之间加入空行。

6. 命名(Naming): 在 Javascript 的核心，ECMA中 使用了 camel-case 的命名规范。Camel-case是以小写字母开头，接着的单词以大写开头，比如thisIsMyname, anotherVariable, aVeryLongVariableName。所以建议命名规范就用ES的命名规范camel-case。

	```javascript
	if (isEnabled()) {
    	setName("Shawnxiao");
	}
	if (getName() === "Shawnxiao")  {
    	doSomething();
	}
	```
 
7. 变量和函数(Variables and Functions): 变量的名称大多数应该是符合 camel case 的，并且应该以一个名词开头。以名词开头主要是将变量同函数进行区分，因为函数是多以动词开头的。变量的命名简直就是一门艺术，你要在尽量短的文字中表达出无限的意义。尽量在变量命名时就可以暗示出它的数据类型，比如 count, length 和 size 就常常被认为是 number,而 name, title 和 message 则常被认为是 string。单一的字符，比如 i, j 和 k 则常常在循环中使用。无意义的命名应该尽量的被避免，比如 foo, bar 和 temp。    对于函数和方法的命名第一个单词应该是以动词开头的，下面是一些对于动词的比较通用的规范：

	前缀           | 作用
	------------   | ------------- 
	can			   | 函数返回的是boolean
	has	           |  函数返回的是boolean
	is	           |  函数返回的是boolean
	get	           | 函数返回的是非boolean值
	set	           |  函数被用作存储一个值
 
8. 构造函数(constructor): 对于构造函数的命名，建议使用Pascal命名，即第一个字母是大写的，并且构造函数的名称应该是一个名词。

9. 文字值(literal values): 
	* 字符(string): 建议尽量使用双引号，对于字符串。创建多行字符串的时候，使用加号进行连接。

		```javascript
			//Bad
			var longString = "Here's the story, of a man \
				named shawn";
			//Good
			var longString =  "Here's the story, of a man  " +
                           "named shawn";
		```
 
   * 数值(number): 保留小数前的数字，比如 0.5, 10.2。
   * Null: null 的使用环境可以是：初始化一个可能是对象的值；作为函数的传入/返回值，当期望的传入/返回值是对象的时候。下面的用法应该被避免：
   	* 使用 null 来检测一个参数是否提供；
   	* 使用 null 来检测一个没有初始化的变量。
   * undefined: 没有初始化的变量都有一个 undefined 初始值。建议尽量在代码中少使用undefined.
   * 对象字面量(object literals): 对象字面量和通过创建一个新的实例相比是一种常用的来创建一个已经设定了一些属性的对象。当定义对象字面量的时候，在开括号应该在第一行，接着每一个属性占用一行，并且拥有相同的缩进，最后毕括号单独使用一行。
   * 数组字面量(Array literals): 使用两个方括号包裹初始的数组值，来创建数组。

###注释
1. 单行注释(single-line comments): 单行注释有三种方式使用：
	* 单独成行，解释注释行下面的代码，这行注释应该和下面的代码保持相同的缩进；
	* 在一行代码的末尾，在代码和注释直接至少应该有一个缩进；
	* 注释一部分代码，注意是代码而不是额外的说明（这个常常是一些编辑器自带的功能）。

```javascript
// Good
if (condition) {
    // If you made it here, then all security checks passed
    allwed(); 
}
// Bad:在注释的前面没有空号
if (condition) {
     // If you made it here, then all security checks passed
    allwed(); 
}
// Bad:错误的缩进
if (condition) {
// If you made it here, then all security checks passed
    allwed(); 
}
// Good
var result = something + sth;     // sth will be something
//Bad:在代码和注释之间没有足够的空格
var result = something + sth; // sth will be something
/ / Good
// if (condition) {
//    allwed(); 
//    doOtherThing();
// }
```

2. 多行注释(multiine comments): 建议的使用 java 风格的多行注释。java的风格是，多行注释至少有三行，一行是 / * ，一行或多行以 * 开始的注释，和前一行的 * 对齐，最后一行以 */ 结束。多行注释应该和被描述的代码拥有相同的缩进。

3. 使用注释的场景: 大体的原则是当某些事是不清楚的，不能一眼看出来的。
	* 难以理解的代码：
	* 浏览器特定的 Hack：
	* 文档注释：例如 YUIdoc 生成文档时需要添加多行注释。

### 语句和表达式
1. 大括号的对齐：建议开括号和块语句的第一行在同一行。

```javascript
if (condition) {
    doSomething();
} else {
    doSomethingElse();
}
```

2. 块语句的空格(block statement spacing): 建议在开阔号之前和闭括号之后添加空格。

3. switch 语句：
	* 缩进：jslint 的规则是 case 和 switch 进行对齐。
	* Falling Through: 如果加了注释后，那么适合的 falling through 是可以允许的。
	* default: 作者的意见是当没有默认行为的时候就省略了 default。

```javascript
switch(condition) {
// 明显的fall through
case "first":
case "second":
    //code
   break;
case "third":
    //code
   break;
default:
    //code
}
```

4. for 循环: 尽量避免使用 "continue"。

5. for-in 循环：for-in 循环是用来遍历一个对象的属性。for-in 返回的不仅仅是实例的属性，还返回由原型继承来的属性。能用 hasOwnProperty 情况下，尽量使用。还有一个值得注意的是，for-in循环的使用点是针对对象的，对于数组是不建议的。

###变量、函数和操作符
1. 变量声明: 一种比较通用的风格就是将所有的变量的声明都放在函数的最上面。简而言之就是按照 JS引擎解析的顺序进行。对于var语句，作者的建议是尽量的简化，以减小下载的时间。

2. 函数声明: 函数声明和变量声明一样，会被 Javascript 引擎提升。根据这样的表现，所以建议JavScript 的函数在它使用前进行声明。

3. 函数调用时的空格: 几乎达成共识的是，对于函数调用的风格都是在函数名和开括号之间不要出现空格。

4. 立即函数调用: JavaScript 允许你声明匿名函数，即没用具体名字的函数，并且将函数制定给变量或者是属性。为了使立即调用函数的调用更加的明显，所以在函数的周围放上括号是非常有必要的。

```javascript
//Good
var value = (function () {
    // function body
    return {
         message: "HI"
    }
}());
```

5. 相等(equality): 相等运算在 JavaScript 中因为类型强制转换变得复杂。类型强制转换是为了使某些操作成功而将变量从一种特殊的类型自动转换成另外一种类型，这样也就导致了某些无可预料的结果。类型强制转换经常会发生的地方就是使用了 == 或者 != 的时候，这两个操作符会导致两个比较的不同类型的变量进行比较的时候发生类型转换。为了避免类型转换，建议使用 === 或者 !===

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
