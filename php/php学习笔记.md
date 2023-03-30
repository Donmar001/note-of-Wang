# PHP学习笔记

### ***php***简介

PHP 是服务器端脚本语言。PHP 能做任何事，PHP 主要是用于服务端的脚本程序，因此可以用 PHP 来完成任何其它的 CGI 程序能够完成的工作，例如收集表单数据，生成动态网页，或者发送／接收 Cookies。但 PHP 的功能远不局限于此。PHP原始为Personal Home Page的缩写，现在已经正式更名为 "PHP: Hypertext Preprocessor"。广泛运用的开源脚本语言。



### php语法

php语言以<?开头，以?>结尾，php是一种脚本语言，可以放在文档的任何位置，每句php语句用;结尾。[^ps]

[^ps]: **注释：**PHP 语句以分号结尾（;）。PHP 代码块的关闭标签也会自动表明分号（因此在 PHP 代码块的最后一行不必使用分号）

-----------------

示例，一个php文件

```php
<!DOCTYPE html>
<html>
<body>

<h1>我的第一张 PHP 页面</h1>

<?php
echo "Hello World!";
?>

</body>
</html>
```

php文件中往往都会有html标签

php中的注释有三种方式，//注释 //*注释/*/ #注释

##### php对大小写的敏感性

在 PHP 中，所有用户定义的函数、类和关键词（例如 if、else、echo 等等）都对大小写不敏感。

```
#三个语句等效
ECHO "Hello World!<br>";
echo "Hello World!<br>";
EcHo "Hello World!<br>";
```

不过在 PHP 中，所有变量都对大小写敏感。 $color、$COLOR 以及 $coLOR为三个不同的变量



#### php变量

###### 规则：

- 变量以 $ 符号开头，其后是变量的名称
- 变量名称必须以字母或下划线开头
- 变量名称不能以数字开头
- 变量名称只能包含字母数字字符和下划线（A-z、0-9 以及 _）
- 变量名称对大小写敏感（$y 与 $Y 是两个不同的变量）

创建变量时和c语言的不同，php中没有创建变量的语句，只在第一次给变量赋值时创建变量，且无需给变量指定变量类型，php会自动根据给定的值指定数据类型

PHP 有三种不同的变量**作用域**：

- local（局部）
- global（全局）
- static（静态）

###### echo与print语句

echo 和 print 之间的差异：

- echo - 能够输出一个以上的字符串
- print - 只能输出一个字符串，并始终返回 1

echo比print稍快，echo不返回值



#### 数据类型

-------------

###### **字符型**

字符串是字符序列，比如 "Hello world!"。字符串可以是引号内的任何文本。您可以使用单引号或双引号。两者等价

```php
<?php 
$x = "Hello world!";
echo $x;
echo "<br>"; 
$x = 'Hello world!';
echo $x;
?>
```

-----------



###### 整数

1. 整数必须有至少一个数字（0-9）

2. 整数不能包含逗号或空格

3. 整数不能有小数点

4. 整数正负均可

5. 可以用三种格式规定整数：十进制、十六进制（前缀是 0x）或八进制（前缀是 0）



```php
<?php 
$x = 12;
var_dump($x);
echo "<br>"; 
$x = -34; // 负数
var_dump($x);
echo "<br>"; 
$x = 0x5C; // 十六进制数
var_dump($x);
echo "<br>";
$x = 077; // 八进制数
var_dump($x);   //[^var_dump()]
?>
```

[^var_dump()]: 返回变量的数据类型和值

---------------------------



###### php浮点数

浮点数是有小数点或指数形式的数字。

```php
<?php 
$x = 10.365;
var_dump($x);
echo "<br>"; 
$x = 2.4e3;
var_dump($x);
echo "<br>"; 
$x = 8E-5;
var_dump($x);
?>
```

--------------

###### 逻辑值

即等价于c语言中的布尔值，有True 和 False 

------------------

###### 数组

```php
<?php 
$cars=array("Volvo","BMW","SAAB");
var_dump($cars);
?>
```

------------

##### php类

**对象**是存储数据和有关如何处理数据的信息的数据类型。在 PHP 中，必须明确地声明对象。首先我们必须声明对象的类。对此，我们使用 class 关键词。类是包含**<u>属性</u>**和**<u>方法</u>**的结构。然后我们在对象类中定义数据类型，然后在该类的实例中使用此数据类型

```php
<?php
class Car
{
  var $color;
  function Car($color="green") {
    $this->color = $color;
  }
  function what_color() {
    return $this->color;
  }
}
?>
```

-------------------------

##### php null值

特殊的 NULL 值表示变量无值。NULL 是数据类型 NULL 唯一可能的值。NULL 值标示变量是否为空。也用于区分空字符串与空值数据库。

可以通过把值设置为 NULL，将变量清空

```php
<?php
$x="Hello world!";
echo $x;
$x=null;
echo $x;
var_dump($x);
?>
```



#### 字符串函数

**strlen()**函数 ：函数返回字符串的长度，以字符计[^作用]

[^作用]: 常用于循环和其他函数，在确定字符串何时结束很重要时。（例如，在循环中，我们也许需要在字符串的最后一个字符之后停止循环）

**str_word_count()**函数： 函数对字符串中的单词进行计数：

**strrev()**函数： 反转字符串

**strops()**函数： 用于检索字符串内指定的字符或文本，如果找到匹配，则会返回首个匹配的字符位置。如果未找到匹配，则将返回 FALSE。

**str_replace()**函数：用一些字符串替换字符串中的另一些字符

```php
<?php
echo strlen("Hello world!");
echo str_word_count("Hello world!"); // 输出 2
echo strrev("Hello world!"); // 输出 !dlrow olleH
echo strpos("Hello world!","world");  //以上代码的输出是：6。字符串的首字符为0
echo str_replace("world", "Kitty", "Hello world!"); // 输出 Hello Kitty!
?>
```



#### php的宏（常量）

设置常量使用函数define()，有三个变量

1. 首个参数定义常量的名称
2. 第二个参数定义常量的值
3. 第三个参数规定常量是否对大小写不敏感。默认时false

```php
<?php
define("wangchaodong", "i am troye sivan");       //默认常量对大小写敏感
echo wangchaodong;
?>
```

常量是自动全局的，而且可以贯穿整个脚本使用。



#### php中的运算符

其中php的算数运算符+ - * / %及赋值运算符= += -= *= /= %=与c语言相同，参考c语言

###### php字符串运算函数

| 运算符 | 名称     | 示例                                      |
| ------ | -------- | ----------------------------------------- |
| .      | 串接     | $txt1 = "Hello" $txt2 = $txt1 . " world!" |
| .=     | 串接赋值 | $txt1 = "Hello" $txt1 .= " world!"        |



#### php 比较运算符

与c语言相似的有 <u>==</u>  <u>!=</u>  <u>></u>  <u><</u>  <u>>=</u>  <u><=</u>

不同的有

| 运算符 | 名称               |
| ------ | ------------------ |
| ===    | 全等（完全相同）   |
| <>     | 不等于             |
| !==    | 不全等（完全不同） |



#### php逻辑运算符

| 运算符 | 名称 |
| ------ | ---- |
| and    | 与   |
| or     | 或   |
| xor    | 异或 |
| &&     | 与   |
| \|\|   | 或   |
| !      | 非   |



#### php 数组运算符

| 运算符 | 名称   |
| ------ | ------ |
| +      | 联合   |
| ==     | 相等   |
| ===    | 全等   |
| !=     | 不相等 |
| <>     | 不相等 |
| !==    | 不全等 |

---



#### php foreach()循环

语法

```php
foreach ($array as $value) {
  code to be executed;
}
```

每进行一次循环迭代，当前数组元素的值就会被赋值给 $value 变量，并且数组指针会逐一地移动，直到到达最后一个数组元素。

下面的例子演示的循环将输出给定数组（$colors）的值：

```php
<?php 
$colors = array("red","green","blue","yellow"); 

foreach ($colors as $value) {
  echo "$value <br>";
}
?>
```



#### php函数

php的强大之处在于其内建，封装好的内部函数

[php内建函数](https://www.w3cschool.cn/php/php-tutorial.html)

自定义函数必须要义function关键字开头

其参数设置，return值设定，及默认值设置与c语言相同



### 数组

数组是特殊的变量，它可以同时保存一个以上的值。

创建函数的方法，使用函数array()

在php中数组有三种类型

* **索引数组** -带有数字索引数组
* **关联数组** -带有指定键的数组
* **多维数组** -包含一个或者多个数组都、的数组



##### php索引数组

索引是自动分配的

```php
$cars=array("porsche","BMW","Volvo");
```

索引从0开始



也可以手动分配索引

```php
$cars[0]="porsche";
$cars[1]="BMW";
$cars[2]="Volvo";
```

[^count() 函数]: 用来统计数组中元素个数

##### php关联函数

```php
//方法一
$age=array("Bill"=>"35","Steve"=>"37","Elon"=>"43");

//方法二
$age['Bill']="63";
$age['Steve']="56";
$age['Elon']="47";
```

**遍历**关联函数的方法

```php
<?php
$age=array("Bill"=>"63","Steve"=>"56","Elon"=>"47");

foreach($age as $x=>$x_value) {
  echo "Key=" . $x . ", Value=" . $x_value;
  echo "<br>";
}
?>
```

##### php多维数组

多维数组指的是包含一个或者多个数组的数组，php可以有三、四设置五级数组，不过一般为了方便理解与管理都不超过三维

eg：二维数组

```php
$cars = array
  (
  array("Volvo",22,18),
  array("BMW",15,13),
  array("Saab",5,2),
  array("Land Rover",17,15)
  );
```

访问该二维数组的方法

```php
//方法一
<?php
echo $cars[0][0].": 库存：".$cars[0][1].", 销量：".$cars[0][2].".<br>";
echo $cars[1][0].": 库存：".$cars[1][1].", 销量：".$cars[1][2].".<br>";
echo $cars[2][0].": 库存：".$cars[2][1].", 销量：".$cars[2][2].".<br>";
echo $cars[3][0].": 库存：".$cars[3][1].", 销量：".$cars[3][2].".<br>";
?>
    
    
//方法二
<?php
for ($row = 0; $row < 4; $row++) {
  echo "<p><b>Row number $row</b></p>";
  echo "<ul>";
  for ($col = 0; $col < 3; $col++) {
    echo "<li>".$cars[$row][$col]."</li>";
  }
  echo "</ul>";
}
?>
```

---------

#### 数组中元素的排序

数组中常用的排序函数有

- sort() - 以升序对数组排序
- rsort() - 以降序对数组排序
- asort() - 根据值，以升序对关联数组进行排序
- ksort() - 根据键，以升序对关联数组进行排序
- arsort() - 根据值，以降序对关联数组进行排序
- krsort() - 根据键，以降序对关联数组进行排序



### PHP全局变量 - 超全局变量

超全局变量在 PHP 4.1.0 中引入，是在全部作用域中始终可用的内置变量。超全局变量在 PHP 4.1.0 中引入，是在全部作用域中始终可用的内置变量。

超全局变量

- $GLOBALS
- $_SERVER
- $_REQUEST
- $_POST
- $_GET
- $_FILES
- $_ENV
- $_COOKIE
- $_SESSION

-----

#### $GLOBALS

$GLOBALS 这种全局变量用于在 PHP 脚本中的任意位置访问全局变量（从函数或方法中均可）。PHP 在名为 $GLOBALS[index] 的数组中存储了所有全局变量。变量的名字就是数组的键。

```php
<?php 
$x = 75; 
$y = 25;
 
function addition() { 
  $GLOBALS['z'] = $GLOBALS['x'] + $GLOBALS['y']; 
}
 
addition(); 
echo $z; 
?>
```



#### $_SERVER

$_SERVER 这种超全局变量保存关于报头、路径和脚本位置的信息

```php
<?php 
echo $_SERVER['PHP_SELF'];
echo "<br>";
echo $_SERVER['SERVER_NAME'];
echo "<br>";
echo $_SERVER['HTTP_HOST'];
echo "<br>";
echo $_SERVER['HTTP_REFERER'];
echo "<br>";
echo $_SERVER['HTTP_USER_AGENT'];
echo "<br>";
echo $_SERVER['SCRIPT_NAME'];
?>
```

| 元素/代码                     | 描述                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| $_SERVER['PHP_SELF']          | 返回当前执行脚本的文件名。                                   |
| $_SERVER['GATEWAY_INTERFACE'] | 返回服务器使用的 CGI 规范的版本                              |
| $_SERVER['SERVER_ADDR']       | 返回当前运行脚本所在的服务器的 IP 地址                       |
| $_SERVER['SERVER_NAME']       | 返回当前运行脚本所在的服务器的主机名（比如 www.w3school.com.cn） |
| $_SERVER['SERVER_SOFTWARE']   | 返回服务器标识字符串（比如 Apache/2.2.24）                   |
| $_SERVER['SERVER_PROTOCOL']   | 返回请求页面时通信协议的名称和版本（例如，“HTTP/1.0”）。     |
| $_SERVER['REQUEST_METHOD']    | 返回访问页面使用的请求方法（例如 POST）                      |

[_SERVER](https://www.w3school.com.cn/php/php_superglobals.asp)

---------------

##### $_REQUEST

PHP $_REQUEST 用于收集 HTML 表单提交的数据

```php
<html>
<body>

<form method="post" action="<?php echo $_SERVER['PHP_SELF'];?>">
Name: <input type="text" name="fname">
<input type="submit">
</form>

<?php 
$name = $_REQUEST['fname']; 
echo $name; 
?>

</body>
</html>x
```

#### php $_POST

PHP $_POST 广泛用于收集提交 method="post" 的 HTML 表单后的表单数据。$_POST 也常用于传递变量

```php
<html>
<body>

<form method="post" action="<?php echo $_SERVER['PHP_SELF'];?>">
Name: <input type="text" name="fname">
<input type="submit">
</form>

<?php 
$name = $_POST['fname'];
echo $name; 
?>

</body>
</html>
```



#### $ _GET

PHP $_GET 也可用于收集提交 HTML 表单 (method="get") 之后的表单数据。

$_GET 也可以收集 URL 中的发送的数据。

```php
<html>
<body>

<a href="test_get.php?subject=PHP&web=W3school.com.cn">测试 $GET</a>

</body>
</html>
```

当用户点击链接 "测试 $GET"，参数 "subject" 和 "web" 被发送到 "test_get.php"，然后您就能够通过 $_GET 在 "test_get.php" 中访问这些值了。

test_get.php

```php
<html>
<body>

<?php 
echo "在 " . $_GET['web'] . " 学习 " . $_GET['subject'];
?>

</body>
</html>
```



-----------------

## GET vs. POST

GET 和 POST 都创建数组（例如，array( key => value, key2 => value2, key3 => value3, ...)）。此数组包含键/值对，其中的键是表单控件的名称，而值是来自用户的输入数据。

GET 和 POST 被视作 $_GET 和 $_POST。它们是超全局变量，这意味着对它们的访问无需考虑作用域 - 无需任何特殊代码，您能够从任何函数、类或文件访问它们。

$_GET 是通过 URL 参数传递到当前脚本的变量数组。

$_POST 是通过 HTTP POST 传递到当前脚本的变量数组。

##### 何时使用 GET？

通过 GET 方法从表单发送的信息*对任何人都是可见的*（所有变量名和值都显示在 URL 中）。GET 对所发送信息的数量也有限制。限制在大约 2000 个字符。不过，由于变量显示在 URL 中，把页面添加到书签中也更为方便。

GET 可用于发送非敏感的数据。

**注释：**绝不能使用 GET 来发送密码或其他敏感信息！

##### 何时使用 POST？

通过 POST 方法从表单发送的信息*对其他人是不可见的*（所有名称/值会被嵌入 HTTP 请求的主体中），并且对所发送信息的数量也*无限制*。

此外 POST 支持高阶功能，比如在向服务器上传文件时进行 multi-part 二进制输入。

不过，由于变量未显示在 URL 中，也就无法将页面添加到书签。