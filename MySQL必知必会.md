# MySQL必知必会

# 第一章 了解SQL

## 一些基本概念

表：某种特定类型数据（必须是一种类型的数据或一个清单）的结构化清单，每个表都有一个唯一的名字（同一数据库中表名不重复，不同数据库表名重复）。



列：表由一个或多个列组成，列存储着表中的某部分信息。每个列都有相应的数据类型。



数据类型：所容许的数据的类型。每个表列都有相应的数据类型，它限制（或容许）该列中存储的数据。



模式：定义数据在表中如何存储，如可以存储什么样的数据，数据如何分解，各部分信息如何命名，等等。描述表的这组信息就是所谓的模式，模式可以用来描述数据库中特定的表以及整个数据库（和其中表的关系）。



行：表中的数据按行储存，行是表中的一个记录。行数就是记录的总数。



主键：表中每一行都应该有可以唯一标识自己的一列（或一组列）。**唯一**标识表中每行的这个列（或这组列）称为主键。所以，主键用来表示一个特定的行。没有主键，更新或删除表中特定行很困难，因为没有安全的方法保证只涉及相关的行。**为了方便管理，应该总是定义主键**。表中的任何列都可以作为主键，只要满足：(1)任意两行都不具有相同的主键值(2)每个行都必须有一个主键值

主键值规则：主键通常定义在表的一列上，但这并不是必需的，也可以一起使用多个列作为主键。在使用多列作为主键时，上述两个条件必须应用到构成主键的所有列，所有列值的组合必须是唯一的（但单个列的值可以不唯一）。

主键值规则是MySQL本身强制实施的， 除MySQL强制实施的规则外，应该坚持的几个普遍认可的最好习惯为： 

(1)不更新主键列中的值；

(2)不重用主键列的值；

(3)不在主键列中使用可能会更改的值。（例如，如果使用一个名字作为主键以标识某个供应商，当该供应商合并和更改其名字时，必须更改这个主键。）

# 第二章 MySQL简介

SQL是一种专门用来与数据库通信的语言

MySQL是一种DMBS，所以他是一种数据库软件

DBMS的分类：

(1)基于共享文件系统的DBMS

(2)基于C/S 客户机/服务器的DBMS-MySQL就是这一种

客户机—服务器应用分为两个部分。服务器部分负责所有数据访问和处理的一个软件。这个软件运行在称为数据库服务器的计算机上。

<u>与数据文件打交道的只有服务器软件。关于数据、数据添加、删除和数据更新的所有请求都由服务器软件完成。这些请求或更改来自运行客户机软件的计算机。客户机是与用户打交道的软件。例如，如果你请求一个按字母顺序列出的产品表，则客户机软件通过网络提交该请求给服务器软件。服务器软件处理这个请求，根据需要过滤、丢弃和排序数据；然后把结果送回到你的客户机软件。</u>

运行客服机软件的计算机向运行服务器软件的计算机发出处理数据的请求。

客户机和服务器软件可能安装在两台计算机或一台计算机上。不管它们在不在相同的计算机上，为进行所有数据库交互，客户机软件都要与服务器软件进行通信。

所有这些活动对用户都是透明的。数据存储在别的地方，或者数据库服务器为你完成这个处理这一事实是隐藏的。你不需要直接访问数据文件。事实上，多数网络的建立使用户不具有对数据的访问权，甚至不具有对存储数据的驱动器的访问权。

这样的意义何在？因为为了使用MySQL，你需要访问运行MySQL服务器软件的计算机和发布命令到MySQL的客户机软件的计算机。

 服务器软件为MySQL DBMS。你可以在本地安装的副本上运行，也可以连接到运行在你具有访问权的远程服务器上的一个副本。

 客户机可以是MySQL提供的工具、脚本语言（如Perl）、Web应用开发语言（如ASP、ColdFusion、JSP和PHP）、程序设计语言（如C、C++、Java）等

## 命令行实用程序

在cmd输入mysql打开命令行实用程序，它用于快速测试和执行脚本，基本都是用它

(1)命令输入在mysql>之后；

(2)命令用;或\g结束，换句话说，仅按Enter不执行命令；

(3)输入help或\h获得帮助，也可以输入更多的文本获得特定命令的帮助（如，输入help select获得使用SELECT语句的帮助）； 

(4)输入quit或exit退出命令行实用程序

## MySQL Administrator-管理器

是一个**图形交互客户机，**用来简化MySQL服务器的管理

## MySQL Query Browser

# 第三章 初步使用MySQL

1.选择数据库命令，输入：

```mysql
USE xx;
```

xx是某个已创建的数据库名字，数据库选择成功后会显示：

```mysql
Database changed
```

必须先用USE 打开数据库，才能读取其中的指令

2.显示数据库列表

```mysql
SHOW DATABASES;
```

一定要注意加分号

3.显示一个数据库内表的列表

```mysql
SHOW TABLES;
```

4.显示一个数据库内可用表的列们

```mysql
SHOW COLUMNS FROM xx;
```

xx是此数据库的某个表的列

**自动增量:**某些表列需要唯一值。例如，订单编号、雇员ID或（如上面例子中所示的）顾客ID。在每个行添加到表中时，MySQL可以自动地为每个行分配下一个可用编号，不用在添加一行时手动分配唯一值（这样做必须记住最后一次使用的值）。这个功能就是所谓的自动增量。**如果需要它，则必须在用CREATE语句创建表时把它作为表定义的组成部分**。我们将在第21章中介绍CREATE语句。

5.DESCRIBE语句 

MySQL支持用DESCRIBE作为SHOW COLUMNS FROM的一种快捷方式。换句话说，

```mysql
DESCRIBE customers;
```

是SHOW COLUMNS FROM customers;的一种快捷方式。

6.SHOW支持的其他语句

(1)SHOW STATUS，用于显示广泛的服务器状态信息；

(2)SHOW CREATE DATABASE和SHOW CREATE TABLE，分别用来显示创建特定数据库或表的MySQL语句；

(3)SHOW GRANTS，用来显示授予用户（所有用户或特定用户）的安全权限；

(4)SHOW ERRORS和SHOW WARNINGS，用来显示服务器错误或警告消息。

(5)更多关于SHOW的用途：使用HELP SHOW;

<u>值得注意的是，客户机应用程序使用与这里相同的MySQL命令。显示数据库和表的交互式列表、允许交互式创建和编辑表、便于数据录入和编辑或允许管理用户账号和权限等的应用全都使用你可以直接执行的相同的MySQL命令完成它们的工作。</u>

这段话没看懂

7.<u>获得和过滤模式信息</u>

```mysql
INFORMATION_SCHEMA;
```

<u>没用会</u>

# 第四章 检索数据

## 1.检索单个列

使用SELECT语句从表中检索一个或多个数据列=用途是从一个或多个表中检索信息。

为了使用SELECT检索表数据，必须至少给出两条信息——想**选择什么，以及从什么地方选择**

```mysql
select prod_name from products;
```

此语句从products表中检索一个名为prod_name的列

多条SQL语句必须以分号（；）分隔。MySQL如同多数DBMS一样，不需要在单条SQL语句后加分号。**但是最好加**

**命令最好区分大小写**

## 2.检索多个列

**要加逗号分割**

```mysql
SELECT prod_id, prod_name, prod_price FROM products;
```

## 3.检索所有列

```mysql
SELECT * FROM products;
```

***是一个通配符，他有一个优点是可以帮助检索未知列**

## 4.检索不同的行

正如所见，SELECT返回所有匹配的行。但是，如果你不想要每个值每次都出现，怎么办？例如，假如你想得出products表中产品的所有供应商ID：

<img src="C:/Users/hmydw/AppData/Roaming/Typora/typora-user-images/image-20210524104236290.png" alt="image-20210524104236290" style="zoom:50%;" />

SELECT语句返回14行（即使表中只有4个供应商），因为products表中列出了14个产品。那么，如何检索出有不同值的列表呢？

**解决办法是使用DISTINCT关键字，顾名思义，此关键字指示MySQL只返回不同的值**。

```mysql
select distinct vend_id from products;
```

**distinct必须放在列明的前边；**

**DISTINCT关键字应用于所有列而不仅是前置它的列。如果给出SELECT DISTINCT vend_id, prod_price，除非指定的两个列都不同，否则所有行都将被检索出来**

## 5.限制结果 limit

显示不多于5行

```
select prod_name from products limit 5;
```

显示指定行范围

```
select prod_name from products limit 5,5;
```

检索出来的第一行为行0而不是行1。因此，LIMIT 1, 1将检索出第二行而不是第一行。

**在行数不够时:**LIMIT中指定要检索的行数为检索的最大行数。如果没有足够的行（例如，给出LIMIT 10, 5，但只有13行），MySQL将只返回它能返回的那么多行。

**MySQL 5的LIMIT语法** LIMIT 3, 4的含义是从行4开始的3行还是从行3开始的4行？如前所述，它的意思是从行3开始的4行，这容易把人搞糊涂。 由于这个原因，MySQL 5支持LIMIT的另一种替代语法。LIMIT4 OFFSET 3意为从行3开始取4行，就像LIMIT 3, 4一样

## 6.使用完全限定的表名

```
select products.prod_name from products;
```

```
select products.prod_name from crashcourse.products;
```

# 第五章 排序检索数据

**上一章select到的数据是没有经过排序的**

关系数据库设计理论认为，如果不明确规定排序顺序，则不应该假定检索出的数据的顺序有意义。

## 子句

SQL语句由子句构成，有些子句是必需的，而有的是可选的。一个子句通常由一个关键字和所提供的数据组成。子句的例子有SELECT语句的FROM子句。

## 1.order by子句

```
select prod_name from products order by prod_name;
```

这条语句除了指示MySQL对prod_name列以字母顺序排序数据的ORDER BY子句外，与前面的语句相同

<img src="C:/Users/hmydw/AppData/Roaming/Typora/typora-user-images/image-20210524111313122.png" alt="image-20210524111313122" style="zoom:50%;" />

可以看到先排了数字，后拍了字母

<u>通过非选择列进行排序</u> 通<u>常，ORDER BY子句中使用的列将是为显示所选择的列。但是，实际上并不一定要这样，用非检索的列排序数据是完全合法的</u>

<u>没看懂上边在说啥</u>

## 2.按多个列排序

为了按多个列排序，只要指定列名，列名之间用逗号分开即可（就像选择多个列时所做的那样）。下面的代码检索3个列，并按其中两个列对结果进行排序——首先按价格，然后再按名称排序。

```
select prod_id, prod_price, prod_name from products order by prod_price, prod_name;
```

<img src="C:/Users/hmydw/AppData/Roaming/Typora/typora-user-images/image-20210524112634136.png" alt="image-20210524112634136" style="zoom:50%;" />

## 3.指定排序方向

数据的默认排序方式是A-Z升序，还可以使用desc关键字Z-A排序

下边是以单个列排序

```
select prod_id, prod_price, prod_name from products order by prod_price desc;
```

下面的例子以降序排序产品（最贵的在最前面），然后再对产品名排序：

```
select prod_id, prod_price, prod_name from products order by prod_price desc, prod_name;
```

**DESC关键字只应用到直接位于其前面的列名。**在上例中，只对prod_price列指定DESC，对prod_name列不指定。因此,prod_price列以降序排序，而prod_name列（在每个价格内）仍然按标准的升序排序。所以，如果想在多个列上降序排序，就要对每个列指定DECS关键字。

与DESC相反的关键字是ASC（ASCENDING），在升序排序时可以指定它。但实际上，ASC没有多大用处，因为升序是默认的（如果既不指定ASC也不指定DESC，则假定为ASC）。

#### 区分大小写和排序顺序

在对文本性的数据进行排序时，A与 a相同吗？a位于B之前还是位于Z之后？这些问题不是理论问题，其答案取决于数据库如何设置

**在字典（dictionary）排序顺序中，A被视为与a相同，这是MySQL（和大多数数据库管理系统）的默认行为。**但是，许多数据库管理员能够在需要时改变这种行为（如果你的数据库包含大量外语字符，可能必须这样做）。**这里关键的问题是，如果确实需要改变这种排序顺序，用简单的ORDER BY子句做不到。你必须请求数据库管理员的帮助。**

### 怎样找到一列中的最高或最低值

**使用ORDER BY和LIMIT的组合，能够找出一个列中最高或最低的值。**下面的例子演示如何找出最昂贵物品的值：

```
select prod_id, prod_price, prod_name from products order by prod_price desc limit 1;
```

prod_price DESC保证行是按照由最昂贵到最便宜检索的，而LIMIT 1告诉MySQL仅返回一行。

#### order by子句的位置

**在给出ORDER BY子句时，应该保证它位于FROM子句之后。如果使用LIMIT，它必须位于ORDER BY之后。**

# 第六章 过滤数据-Ⅰ

使用select语句的where子句指定搜索条件

## 1.where子句

```
select prod_name, prod_price from products where prod_price = 2.50;
```

该语句返回prod_price值为2.50的行

在同时使用ORDER BY和WHERE子句时，应该让ORDER BY位于WHERE之后，否则将会产生错误（关于ORDER BY的使用，请参阅第5章）

```
select prod_name, prod_price from products where prod_price = 2.50 order by prod_name desc;
```

## 2.where子句的操作符

=  <> != < <= > >= BETWEEN

<img src="https://i.loli.net/2021/05/25/Y6f3LhI2B9NzTOd.png" alt="image-20210525130558894" style="zoom:50%;" />

### (1)查找已知单个值/匹配检查 =

```
select prod_name, prod_price from products where prod_name = 'fuses';
```

执行匹配时不区分大小写，所以fuses等价于Fuses

**上边的单引号用来限制字符串**

### (2)不匹配检查 <> !=

```
select vend_id, prod_name from products where vend_id <> 1003;
```

**<>不是等于的意思，看的是字符串的不等于情况， !=看的是数字的**

在本例中，两者效果相同

### (3)范围值检查 between xx and xx

```
select prod_name, prod_price from products where prod_price between 2.50 and 10;
```

这是个闭区间，端点值也读的到

### (4)空值检查

当一个列不包含值，称其包含NULL 无值（no value），它与字段包含0、空字符串或仅仅包含空格不同。

```
select prod_name from products where prod_price is null;
```

**这条语句返回没有价格（空prod_price字段，不是价格为0）的所有产品**，由于表中没有这样的行，所以没有返回数据。

```
select cust_id from customers where cust_email is null;
```

NULL与不匹配 在通过过滤选择出不具有特定值的行时，你可能希望返回具有NULL值的行。但是，不行。因为未知具有特殊的含义，数据库不知道它们是否匹配，所以在匹配过滤或不匹配过滤时不返回它们。 因此，在过滤数据时，一定要验证返回数据中确实给出了被过滤列具有NULL的行。

**上边这句话的意思是，NULL和不匹配这两种情况要分开检测**

# 第七章 数据过滤-Ⅱ

多个where子句的组合。这些子句可以两种方式使用：以AND子句的方式或OR子句的方式使用。

操作符（operator） 用来联结或改变WHERE子句中的子句的关键字。也称为逻辑操作符（logical operator）

## where子句的组合

### and操作符

```
select prod_id, prod_price, prod_name from products where vend_id = 1003 and prod_price <= 10 and prod_price > 4;
```

**可以有很多and**

### or操作符

```
select prod_id, prod_price, prod_name from products where vend_id = 1003 or prod_price <= 10;
```

### 计算次序

```
select prod_name, prod_price from products where vend_id = 1002 or vend_id = 1003 and prod_price >= 10;
```

上述指令可能会产生期待外的结果因为and操作符优先级更高。也就是，与and相连的条件会被优先处理（vend_id = 1003 and prod_price >= 10），然后这个处理结果与vend_id = 1002进行or运算

为了解决上述歧义，使用括号

```
select prod_name, prod_price from products where (vend_id = 1002 or vend_id = 1003) and prod_price >= 10;
```

## IN操作符

圆括号在WHERE子句中还有另外一种用法。IN操作符用来指定条件范围，范围中的每个条件都可以进行匹配。IN取合法值的由逗号分隔的清单，全都括在圆括号中。下面的例子说明了这个操作符

```
select vend_id, mprod_name, prod_price from products where vend_id in (1002,1003) order by prod_name;
```

**IN操作符可以完成与OR相同的功能**

### in操作符的优点

(1)在使用长的合法选项清单时，IN操作符的语法更清楚且更直观。

(2)在使用IN时，计算的次序更容易管理（因为使用的操作符更少）。 

(3)IN操作符一般比OR操作符清单执行更快。

(4)IN的最大优点是可以包含其他SELECT语句，使得能够更动态地建WHERE子句。第14章将对此进行详细介绍。

(5)IN是WHERE子句中用来指定要匹配值的清单的关键字，功能与OR相当。

## NOT操作符

WHERE子句中的NOT操作符有且只有一个功能，那就是否定它之后所跟的任何条件。

```
select prod_name, prod_price from products where vend_id not in (1002,1003) order by prod_name;
```

# 第八章 用通配符进行过滤

前面介绍的所有操作符都是针对已知值进行过滤的。如果搜索产品名中包含文本anvil的所有产品？用简单的比较操作符肯定不行，必须使用通配符。

## like 操作符

通配符	**用来匹配值的一部分**的特殊字符

搜索模式	由字面值、通配符或两者组合构成的搜索条件

**LIKE指示MySQL，后跟的搜索模式利用通配符匹配而不是直接相等匹配进行比较。**

### 百分号通配符

最常使用的通配符是百分号（%）。在搜索串中，%表示任何字符出现任意次数。例如，为了找出所有以词jet起头的产品，可使用以下SELECT语句：

```
select prod_id, prod_name from products where prod_name like 'jet%';
```

**此例子使用了搜索模式'jet%'。在执行这条子句时，将检索任意以jet起头的词。**%告诉MySQL接受jet之后的任意字符，不管它有多少字符。

#### 区分大小写

根据MySQL的配置方式，搜索可以是区分大小写的。如果区分大小写，'jet%'与JetPack将不匹配。

通配符可在搜索模式中任意位置使用，并且可以使用多个通配符。

搜索模式'%anvil%'表示匹配任何位置包含文本anvil的值，而不论它之前或之后出现什么字符。

```
select prod_id, prod_name from products where prod_name like '%anvil%';
```

通配符也可以出现在搜索模式的中间。下面的例子找出以s起头e结尾的所有产品

```
select prod_id, prod_name from products where prod_name like 's%e';
```

重要的是要注意到，除了一个或多个字符外，%还能匹配0个字符。%代表搜索模式中**给定位置的0个**、1个或多个字符。

#### 注意尾空格：

尾空格可能会干扰通配符匹配。例如，在保存词anvil 时，如果它后面有一个或多个空格，则子句WHERE prod_name LIKE '%anvil'将不会匹配它们，因为在最后的l后有多余的字符。解决这个问题的一个简单的办法是在搜索模式最后附加一个%。一个更好的办法是使用函数（第11章将会介绍）去掉首尾空格。

#### %不能匹配NULL

虽然似乎%通配符可以匹配任何东西，但有一个例外NULL。WHERE prod_name LIKE '%'不能匹配用值NULL作为产品名的行。

### 下划线通配符

```
select prod_id, prod_name from products where prod_name like '_ ton anvil';
```

此WHERE子句中的搜索模式给出了后面跟有文本的两个通配符。结果只显示匹配搜索模式的行：第一行中下划线匹配1，第二行中匹配2。.5 ton anvil产品没有匹配，因为搜索模式要求匹配1个通配符而不是2个。

**与%能匹配0个字符不一样，_总是匹配一个字符，不能多也不能少**

## 使用通配符的技巧

# 用正则表达式进行搜索

