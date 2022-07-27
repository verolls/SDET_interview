# MySQL数据库基本操作

## CREAT DATABASE：创建数据库

格式：

```sql
CREATE DATABASE [IF NOT EXISTS] <数据库名>
[[DEFAULT] CHARACTER SET <字符集名>] 
[[DEFAULT] COLLATE <校对规则名>];
```

含义：

- <数据库名>：创建数据库的名称。MySQL 的数据存储区将以目录方式表示 MySQL 数据库，因此数据库名称必须符合操作系统的文件夹命名规则，不能以数字开头，尽量要有实际意义。注意在 MySQL 中不区分大小写。
- IF NOT EXISTS：在创建数据库之前进行判断，只有该数据库目前尚不存在时才能执行操作。此选项可以用来避免数据库已经存在而重复创建的错误。
- [DEFAULT] CHARACTER SET：指定数据库的字符集。指定字符集的目的是为了避免在数据库中存储的数据出现乱码的情况。如果在创建数据库时不指定字符集，那么就使用系统的默认字符集。
- [DEFAULT] COLLATE：指定字符集的默认校对规则。

注意：

- MySQL 不允许在同一系统下创建两个相同名称的数据库。

举例：

创建一个名为 test_db 的数据库

```sql
CREATE DATABASE test_db;
```

## SHOW DATABASES：查看数据库

格式：

```sql
SHOW DATABASES [LIKE '数据库名'];
```

含义：

- LIKE 从句是可选项，用于匹配指定的数据库名称。LIKE 从句可以部分匹配，也可以完全匹配。
- 数据库名由单引号' '包围。

举例：

列出当前用户可查看的所有数据库：

```sql
SHOW DATABASES;
```

使用 LIKE 从句，查看名字中包含 test 的数据库：

```sql
SHOW DATABASES LIKE '%test%';
```

## USE：选择数据库

USE 语句用来完成一个数据库到另一个数据库的跳转。当用 CREATE DATABASE 语句创建数据库之后，该数据库不会自动成为当前数据库，需要用 USE 来指定当前数据库。

格式：

```sql
USE <数据库名>
```

注意：

- 该语句可以通知 MySQL 把<数据库名>所指示的数据库作为当前数据库。该数据库保持为默认数据库，直到语段的结尾，或者直到遇见一个不同的 USE 语句。 只有使用 USE 语句来指定某个数据库作为当前数据库之后，才能对该数据库及其存储的数据对象执行操作。

举例：

将数据库 test_db 设置为默认数据库

```sql
USE test_db;
```

## ALTER DATABASE：修改数据库

在 MySQL 数据库中只能对数据库使用的字符集和校对规则进行修改，数据库的这些特性都储存在 db.opt 文件中。

格式：

```sql
ALTER DATABASE [数据库名] { 
[ DEFAULT ] CHARACTER SET <字符集名> |
[ DEFAULT ] COLLATE <校对规则名>}
```

含义：

- ALTER DATABASE 用于更改数据库的全局特性。
- 使用 ALTER DATABASE 需要获得数据库 ALTER 权限。
- 数据库名称可以忽略，此时语句对应于默认数据库。
- CHARACTER SET 子句用于更改默认的数据库字符集。

举例：

将数据库 test_db 的指定字符集修改为 gb2312，默认校对规则修改为 gb2312_unicode_ci

```sql
ALTER DATABASE test_db
DEFAULT CHARACTER SET gb2312
DEFAULT COLLATE gb2312_chinese_ci;
```

## DROP DATABASE：删除数据库

当数据库不再使用时应该将其删除，以确保数据库存储空间中存放的是有效数据。删除数据库是将已经存在的数据库从磁盘空间上清除，清除之后，数据库中的所有数据也将一同被删除。

格式：

```sql
DROP DATABASE [ IF EXISTS ] <数据库名>
```

含义：

- <数据库名>：指定要删除的数据库名。
- IF EXISTS：用于防止当数据库不存在时发生错误。
- DROP DATABASE：删除数据库中的所有表格并同时删除数据库。使用此语句时要非常小心，以免错误删除。如果要使用 DROP DATABASE，需要获得数据库 DROP 权限。

注意：

- MySQL 安装后，系统会自动创建名为 information_schema 和 mysql 的两个系统数据库，系统数据库存放一些和数据库相关的信息，如果删除了这两个数据库，MySQL 将不能正常工作。
- 使用 DROP DATABASE 命令时要非常谨慎，在执行该命令后，MySQL 不会给出任何提示确认信息。DROP DATABASE 删除数据库后，数据库中存储的所有数据表和数据也将一同被删除，而且不能恢复。因此最好在删除数据库之前先将数据库进行备份。

举例：

将数据库 test_db_del 从数据库列表中删除

```sql
DROP DATABASE test_db_del;
```

# MySQL数据表基本操作

## CREAT TABLE：创建数据表

创建数据表，指的是在已经创建的数据库中建立新表。

格式：

```sql
CREATE TABLE <表名> ([表定义选项])[表选项][分区选项];
```

含义：

- CREATE TABLE：用于创建给定名称的表，必须拥有表CREATE的权限。
- <表名>：指定要创建表的名称，在 CREATE TABLE 之后给出，必须符合标识符命名规则。表名称被指定为 db_name.tbl_name，以便在特定的数据库中创建表。无论是否有当前数据库，都可以通过这种方式创建。在当前数据库中创建表时，可以省略 db-name。如果使用加引号的识别名，则应对数据库和表名称分别加引号。例如，'mydb'.'mytbl' 是合法的，但 'mydb.mytbl' 不合法。
- <表定义选项>：表创建定义，由列名（col_name）、列的定义（column_definition）以及可能的空值说明、完整性约束或表索引组成。
- 默认的情况是，表被创建到当前的数据库中。若表已存在、没有当前数据库或者数据库不存在，则会出现错误。

注意：

- 要创建的表的名称不区分大小写，不能使用SQL语言中的关键字，如DROP、ALTER、INSERT等。
- 必须指定数据表中每个列（字段）的名称和数据类型，如果创建多个列，要用逗号隔开。

举例：

创建员工表 tb_emp1（数据表属于数据库，在创建数据表之前，应使用语句“USE<数据库>”指定操作在哪个数据库中进行，如果没有选择数据库，就会抛出 No database selected 的错误。）

```sql
CREATE TABLE tb_emp1
```

## ALTER TABLE：修改数据表

修改表指的是修改数据库中已经存在的数据表的结构。可以使用 ALTER TABLE 语句来改变原有表的结构，例如增加或删减列、更改原有列类型、重新命名列或表等。

格式：

```sql
ALTER TABLE <表名> [修改选项]
```

修改选项：

- ADD COLUMN <列名> <类型>
- CHANGE COLUMN <旧列名> <新列名> <新列类型>
- ALTER COLUMN <列名> { SET DEFAULT <默认值> | DROP DEFAULT }
- MODIFY COLUMN <列名> <类型>
- DROP COLUMN <列名>
- RENAME TO <新表名>
- CHARACTER SET <字符集名>
- COLLATE <校对规则名> 

### 修改表名

格式：

```sql
ALTER TABLE <旧表名> RENAME [TO] <新表名>；
```

含义：

- TO 为可选参数，使用与否均不影响结果。

举例：

使用 ALTER TABLE 将数据表 student 改名为 tb_students_info

```sql
ALTER TABLE student RENAME TO tb_students_info;
```

### 修改字段名称

格式：

```sql
ALTER TABLE <表名> CHANGE <旧字段名> <新字段名> <新数据类型>；
```

含义：

- 旧字段名：指修改前的字段名；
- 新字段名：指修改后的字段名；
- 新数据类型：指修改后的数据类型，如果不需要修改字段的数据类型，可以将新数据类型设置成与原来一样，但数据类型不能为空。


举例：

使用 ALTER TABLE 修改表 tb_emp1 的结构，将 col1 字段名称改为 col3，同时将数据类型变为 CHAR(30)

```sql
ALTER TABLE tb_emp1
CHANGE col1 col3 CHAR(30);
```

### 修改字段数据类型

格式：

```sql
ALTER TABLE <表名> MODIFY <字段名> <数据类型>
```

含义：

- 表名：指要修改数据类型的字段所在表的名称；
- 字段名：指需要修改的字段；
- 数据类型：指修改后字段的新数据类型。

举例：

使用 ALTER TABLE 修改表 tb_emp1 的结构，将 name 字段的数据类型由 VARCHAR(22) 修改成 VARCHAR(30)

```sql
ALTER TABLE tb_emp1
MODIFY name VARCHAR(30);
```

### 删除字段

格式：

```sql
ALTER TABLE <表名> DROP <字段名>；
```

含义：

- “字段名”指需要从表中删除的字段的名称。

举例：

使用 ALTER TABLE 修改表 tb_emp1 的结构，删除 col2 字段

```sql
ALTER TABLE tb_emp1
DROP col2;
```

### 数据表末尾添加字段

格式：

```sql
ALTER TABLE <表名> ADD <新字段名><数据类型>[约束条件];
```

含义：

- <表名> 为数据表的名字；
- <新字段名> 为所要添加的字段的名字；
- <数据类型> 为所要添加的字段能存储数据的数据类型；
- [约束条件] 是可选的，用来对添加的字段进行约束。

举例：

使用 ALTER TABLE 语句添加一个 INT 类型的字段 age

```sql
ALTER TABLE student ADD age INT(4);
```

### 数据表开头添加字段

格式：

```sql
ALTER TABLE <表名> ADD <新字段名> <数据类型> [约束条件] FIRST;
```

含义：

- FIRST 关键字一般放在语句的末尾。

举例：

使用 ALTER TABLE 语句在表的第一列添加 INT 类型的字段 stuId

```sql
ALTER TABLE student ADD stuId INT(4) FIRST;
```

### 数据表中间位置添加字段

格式：

```sql
ALTER TABLE <表名> ADD <新字段名> <数据类型> [约束条件] AFTER <已经存在的字段名>;
```

注意：

- AFTER 的作用是将新字段添加到某个已有字段后面。
- 只能在某个已有字段的后面添加新字段，不能在它的前面添加新字段。

举例：

使用 ALTER TABLE 语句在 student 表中添加名为 stuno，数据类型为 INT 的字段，stuno 字段位于 name 字段的后面

```sql
ALTER TABLE student ADD stuno INT(11) AFTER name;
```

## DROP TABLE：删除数据表

在删除表的同时，表的结构和表中所有的数据都会被删除，因此在删除数据表之前最好先备份，以免造成无法挽回的损失。

格式：

```sql
DROP TABLE [IF EXISTS] 表名1 [ ,表名2, 表名3 ...]
```

含义：

- 表名1, 表名2, 表名3 ...表示要被删除的数据表的名称。DROP TABLE 可以同时删除多个表，只要将表名依次写在后面，相互之间用逗号隔开即可。
- IF EXISTS 用于在删除数据表之前判断该表是否存在。如果不加 IF EXISTS，当数据表不存在时 MySQL 将提示错误，中断 SQL 语句的执行；加上 IF EXISTS 后，当数据表不存在时 SQL 语句可以顺利执行，但是会发出警告（warning）。

注意：

- 用户必须拥有执行 DROP TABLE 命令的权限，否则数据表不会被删除。
- 表被删除时，用户在该表上的权限不会自动删除。

举例：

删除数据表 tb_emp3

```sql
 DROP TABLE tb_emp3;
```

## 数据表中添加字段


# MySQL操作表中数据

## MySQL查询语句书写顺序

```sql
STEP0: SELECT 选择某些列进行数据展示 [DISTINCT] 需要对结果做独一无二的限定
STEP1: FROM 考虑选择某数据表 [AS] 取别名
STEP2: WHERE 在选中的数据表后进行一定条件的筛选
STEP3：GROUP BY 筛选完后的数据可能需要进行分组
STEP4：HAVING 分完组后的数据可能需要进行组内筛选
STEP5：ORDER BY 组也分完了，数据也根据分组筛选完毕，需要进行排序准备待展示了
STEP6：LIMIT 排序过后，限制展示条数

参考：https://blog.csdn.net/weixin_43876778/article/details/113811672
```

## SELECT：查询数据表
在 MySQL 中，可以使用 SELECT 语句来查询数据。查询数据是指从数据库中根据需求，使用不同的查询方式来获取不同的数据，是使用频率最高、最重要的操作。

### 查询表中所有字段：

格式：

```sql
SELECT * FROM 表名;
```

举例：  

从 tb_students_info 表中查询所有字段的数据
```sql
SELECT * FROM tb_students_info;
```

### 查询表中指定字段：

格式：

```sql
SELECT <字段名1>,<字段名2>,…,<字段名n> FROM <表名>;
```

举例：  

从 tb_students_info 表中获取 id、name 和 height 三列
```sql
SELECT id,name,height FROM tb_students_info;
```

## DISTINCT：去重
在 MySQL 中使用 SELECT 语句执行简单的数据查询时，返回的是所有匹配的记录。如果表中的某些字段没有唯一性约束，那么这些字段就可能存在重复值。为了实现查询不重复的数据，MySQL 提供了 DISTINCT 关键字。

### 对指定字段中重复的数据进行去重：

格式：

```sql
SELECT DISTINCT <字段名> FROM <表名>;
```

注意：

- DISTINCT 关键字只能在 SELECT 语句中使用。
- 在对一个或多个字段去重时，DISTINCT 关键字必须在所有字段的最前面。
- 如果 DISTINCT 关键字后有多个字段，则会对多个字段进行组合去重，也就是说，只有多个字段组合起来完全是一样的情况下才会被去重。

举例：

对 student 表的 name 和 age 字段进行去重  
```sql
SELECT DISTINCT name,age FROM student;
```

## AS：设置别名

为了查询方便，MySQL 提供了 AS 关键字来为表和字段指定别名。

### 为表指定别名：

当表名很长或者执行一些特殊查询的时候，为了方便操作，可以为表指定一个别名，用这个别名代替表原来的名称。

格式：

```sql
<表名> [AS] <别名>  
```

含义：

- <表名>：数据库中存储的数据表的名称。
- <别名>：查询时指定的表的新名称。
- AS关键字可以省略，省略后需要将表名和别名用空格隔开。

注意：

- 表的别名不能与该数据库的其它表同名。
- 表别名只在执行查询时使用，并不在返回结果中显示。


举例：  

为 tb_students_info 表指定别名 stu
```sql
SELECT stu.name,stu.height FROM tb_students_info AS stu;
```



### 为字段指定别名：

在使用 SELECT 语句查询数据时，MySQL 会显示每个 SELECT 后面指定输出的字段。有时为了显示结果更加直观，我们可以为字段指定一个别名。  

格式：
```sql
<字段名> [AS] <别名>
```
含义：
- <字段名>：为数据表中字段定义的名称。
- <字段别名>：字段新的名称。
- AS关键字可以省略，省略后需要将字段名和别名用空格隔开。

注意：

- 字段的别名不能与该表的其它字段同名。
- 字段定义别名之后，会返回给客户端显示，显示的字段为字段的别名。

举例：  

查询 tb_students_info 表，为 name 指定别名 student_name，为 age 指定别名 student_age  
```sql
SELECT name AS student_name, age AS student_age FROM tb_students_info;
```

## LIMIT：限制查询结果的条数
当数据表中有上万条数据时，一次性查询出表中的全部数据会降低数据返回的速度，同时给数据库服务器造成很大的压力。这时就可以用 LIMIT 关键字来限制查询结果返回的条数。


### 指定初始位置：  
LIMIT 关键字可以指定查询结果从哪条记录开始显示，显示多少条记录。  

格式：
```sql
LIMIT 初始位置，记录数
```
含义：
- “初始位置”表示从哪条记录开始显示；
- “记录数”表示显示记录的条数。第一条记录的位置是 0，第二条记录的位置是 1。后面的记录依次类推。
- 上述两个参数必须是正整数

举例：  

在 tb_students_info 表中，使用 LIMIT 子句返回从第 4 条记录开始的行数为 5 的记录

```sql
SELECT * FROM tb_students_info LIMIT 3,5;
```

### 不指定初始位置：  
LIMIT 关键字不指定初始位置时，记录从第一条记录开始显示。显示记录的条数由 LIMIT 关键字指定。

格式：
```sql
LIMIT 记录数
```

含义：

- “记录数”表示显示记录的条数。如果“记录数”的值小于查询结果的总数，则会从第一条记录开始，显示指定条数的记录。如果“记录数”的值大于查询结果的总数，则会直接显示查询出来的所有记录。

注意：

- 带一个参数的 LIMIT 指定从查询结果的首行开始，唯一的参数表示返回的行数，即“LIMIT n”与“LIMIT 0，n”返回结果相同。带两个参数的 LIMIT 可返回从任何位置开始指定行数的数据。

举例：

显示 tb_students_info 表查询结果的前 4 行

```sql
SELECT * FROM tb_students_info LIMIT 4;
```

### LIMIT和OFFSET组合使用
格式：
```sql
LIMIT 记录数 OFFSET 初始位置
```

含义：
- “初始位置”指定从哪条记录开始显示；
- “记录数”表示显示记录的条数。

举例：

在 tb_students_info 表中，使用 LIMIT OFFSET 返回从第 4 条记录开始的行数为 5 的记录

```sql
SELECT * FROM tb_students_info LIMIT 5 OFFSET 3;
```

## ORDER BY：对查询结果进行排序
通过条件查询语句可以查询到符合用户需求的数据，但是查询到的数据一般都是按照数据最初被添加到表中的顺序来显示。为了使查询结果的顺序满足用户的要求，MySQL 提供了 ORDER BY 关键字来对查询结果进行排序。  

格式：  

```sql
ORDER BY <字段名> [ASC|DESC]
```

含义：

- 字段名：表示需要排序的字段名称，多个字段时用逗号隔开。
- ASC|DESC：ASC表示字段按升序排序；DESC表示字段按降序排序。其中ASC为默认值。

注意：

- ORDER BY 关键字后可以跟子查询。
- 当排序的字段中存在空值时，ORDER BY 会将该空值作为最小值来对待。
- ORDER BY 指定多个字段进行排序时，MySQL 会按照字段的顺序从左到右依次进行排序。
- 在对多个字段进行排序时，排序的第一个字段必须有相同的值，才会对第二个字段进行排序。如果第一个字段数据中所有的值都是唯一的，MySQL 将不再对第二个字段进行排序。

### 单字段排序

举例：

查询 tb_students_info 表的所有记录，并对 height 字段进行排序

```sql
SELECT * FROM tb_students_info ORDER BY height;
```

### 多字段排序

举例：

查询 tb_students_info 表中的 name 和 height 字段，先按 height 排序，再按 name 排序

```sql
SELECT name,height FROM tb_students_info ORDER BY height,name;
```

举例：

查询 tb_students_info 表，先按 height 降序排序，再按 name 升序排序

```sql
SELECT name,height FROM tb_student_info ORDER BY height DESC,name ASC;
```

## WHERE：条件查询  

格式：

```sql
WHERE 查询条件
```

含义：

查询条件可以是：
- 带比较运算符和逻辑运算符的查询条件
- 带 BETWEEN AND 关键字的查询条件
- 带 IS NULL 关键字的查询条件
- 带 IN 关键字的查询条件
- 带 LIKE 关键字的查询条件

### 单一条件查询语句

单一条件指的是在 WHERE 关键字后只有一个查询条件。

举例：

在 tb_students_info 数据表中查询身高为 170cm 的学生姓名

```sql
SELECT name,height FROM tb_students_info
WHERE height=170;
```

在 tb_students_info 数据表中查询年龄小于 22 的学生姓名

```sql
SELECT name,age FROM tb_students_info
WHERE age<22;
```

### 多条件查询语句

多个查询条件时用逻辑运算符 AND（&&）、OR（||）或 XOR 隔开。

- AND：记录满足所有查询条件时，才会被查询出来。
- OR：记录满足任意一个查询条件时，才会被查询出来。
- XOR：记录满足其中一个条件，并且不满足另一个条件时，才会被查询出来。


举例：

在 tb_students_info 表中查询 age 大于 21，并且 height 大于等于 175 的学生信息

```sql
SELECT name,age,height FROM tb_students_info 
WHERE age>21 AND height>=175;
```

在 tb_students_info 表中查询 age 大于 21，或者 height 大于等于 175 的学生信息

```sql
SELECT name,age,height FROM tb_students_info 
WHERE age>21 OR height>=175;
```

## LIKE：模糊查询

格式：

```sql
[NOT] LIKE  '字符串'
```

含义：

- NOT ：可选参数，字段中的内容与指定的字符串不匹配时满足条件。
- 字符串：指定用来匹配的字符串。“字符串”可以是一个很完整的字符串，也可以包含通配符。

注意：

- 匹配的字符串必须加单引号或双引号。
- LIKE 关键字支持百分号“%”和下划线“_”通配符。
- “%”是 MySQL 中最常用的通配符，它能代表任何长度的字符串，字符串的长度可以为 0。
- “_”只能代表单个字符，字符的长度不能为 0。
- 通配符是一种特殊语句，主要用来模糊查询。当不知道真正字符或者懒得输入完整名称时，可以使用通配符来代替一个或多个真正的字符。 

举例：

在 tb_students_info 表中，查找所有以字母“T”开头的学生姓名

```sql
SELECT name FROM tb_students_info
WHERE name LIKE 'T%';
```

在 tb_students_info 表中，查找所有以字母“y”结尾，且“y”前面只有 4 个字母的学生姓名

```sql
mysql> SELECT name FROM tb_students_info
WHERE name LIKE '____y';
```

## BETWEEN AND：范围查询

MySQL 提供了 BETWEEN AND 关键字，用来判断字段的数值是否在指定范围内。

格式：

```sql
[NOT] BETWEEN 取值1 AND 取值2
```

含义：

- NOT：可选参数，表示指定范围之外的值。如果字段值不满足指定范围内的值，则这些记录被返回。
- 取值1：表示范围的起始值。
- 取值2：表示范围的终止值。

注意：

- BETWEEN AND 能匹配指定范围内的所有值，包括起始值和终止值。

举例：

在表 tb_students_info 中查询年龄在 20 到 23 之间的学生姓名和年龄

```sql
SELECT name,age FROM tb_students_info 
WHERE age BETWEEN 20 AND 23;
```

## NULL：空值查询

MySQL 提供了 IS NULL 关键字，用来判断字段的值是否为空值（NULL）。空值不同于 0，也不同于空字符串。如果字段的值是空值，则满足查询条件，该记录将被查询出来。如果字段的值不是空值，则不满足查询条件。

格式：

```sql
IS [NOT] NULL
```

含义：

- NOT”是可选参数，表示字段值不是空值时满足条件。

注意：

- IS NULL 是一个整体，不能将 IS 换成“=”

举例：

查询 tb_students_info 表中 login_date 字段是 NULL 的记录

```sql
SELECT name,login_date FROM tb_students_info 
WHERE login_date IS NULL;
```

查询 tb_students_info 表中 login_date 字段不为空的记录

```sql
SELECT name,login_date FROM tb_students_info 
WHERE login_date IS NOT NULL;
```

## GROUP BY：分组查询

GROUP BY 关键字可以根据一个或多个字段对查询结果进行分组。

格式：

```sql
GROUP BY  <字段名>
```

含义：

- “字段名”表示需要分组的字段名称，多个字段时用逗号隔开。

举例：

根据 tb_students_info 表中的 sex 字段进行分组查询

```sql
SELECT name,sex FROM tb_students_info 
GROUP BY sex;
```

## HAVING：过滤分组

可以使用 HAVING 关键字对分组后的数据进行过滤。

格式：

```sql
HAVING <查询条件>
```

含义：

- HAVING 关键字和 WHERE 关键字都可以用来过滤数据，且 HAVING 支持 WHERE 关键字中所有的操作符和语法。


注意：

WHERE 和 HAVING 关键字也存在以下几点差异：

- 一般情况下，WHERE 用于过滤数据行，而 HAVING 用于过滤分组。
- WHERE 查询条件中不可以使用聚合函数，而 HAVING 查询条件中可以使用聚合函数。
- WHERE 在数据分组前进行过滤，而 HAVING 在数据分组后进行过滤 。
- WHERE 针对数据库文件进行过滤，而 HAVING 针对查询结果进行过滤。也就是说，WHERE 根据数据表中的字段直接进行过滤，而 HAVING 是根据前面已经查询出的字段进行过滤。
- WHERE 查询条件中不可以使用字段别名，而 HAVING 查询条件中可以使用字段别名。


举例：

根据 height 字段对 tb_students_info 表中的数据进行分组，并使用 HAVING 关键字分别查询出分组后平均身高大于 170 的学生姓名、性别和身高

```sql
SELECT GROUP_CONCAT(name),sex,height FROM tb_students_info 
GROUP BY height 
HAVING AVG(height)>170;
```

## CROSS JOIN：交叉连接
前面所讲的查询语句都是针对一个表的，但是在关系型数据库中，表与表之间是有联系的，所以在实际应用中，经常使用多表查询。多表查询就是同时查询两个或两个以上的表。多表查询主要有交叉连接、内连接和外连接。

交叉连接（CROSS JOIN）一般用来返回连接表的笛卡尔积。

格式：

```sql
SELECT <字段名> FROM <表1> CROSS JOIN <表2> [WHERE子句]

或

SELECT <字段名> FROM <表1>, <表2> [WHERE子句] 
```

含义：

- 字段名：需要查询的字段名称。
- <表1><表2>：需要交叉连接的表名。
- WHERE 子句：用来设置交叉连接的查询条件。

注意：

- 多个表交叉连接时，在 FROM 后连续使用 CROSS JOIN 或`,`即可。以上两种语法的返回结果是相同的，但是第一种语法才是官方建议的标准写法。
- 当连接的表之间没有关系时，我们会省略掉 WHERE 子句，这时返回结果就是两个表的笛卡尔积，返回结果数量就是两个表的数据行相乘。
- 交叉连接可以查询两个或两个以上的表.

举例：

查询 tb_course 表中的 id 字段和 tb_students_info 表中的 course_id 字段相等的内容

```sql
SELECT * FROM tb_course CROSS JOIN tb_students_info 
WHERE tb_students_info.course_id = tb_course.id;
```

## INNER JOIN：内连接

内连接（INNER JOIN）主要通过设置连接条件的方式，来移除查询结果中某些数据行的交叉连接。简单来说，就是利用条件表达式来消除交叉连接的某些数据行。

内连接使用 INNER JOIN 关键字连接两张表，并使用 ON 子句来设置连接条件。如果没有连接条件，INNER JOIN 和 CROSS JOIN 在语法上是等同的，两者可以互换。

格式：

```sql
SELECT <字段名> FROM <表1> INNER JOIN <表2> [ON子句]
```

含义：

- 字段名：需要查询的字段名称。
- <表1><表2>：需要内连接的表名。
- INNER JOIN ：内连接中可以省略 INNER 关键字，只用关键字 JOIN。
- ON 子句：用来设置内连接的连接条件。

注意：

- 多个表内连接时，在 FROM 后连续使用 INNER JOIN 或 JOIN 即可。
- INNER JOIN 也可以使用 WHERE 子句指定连接条件，但是 INNER JOIN ... ON 语法是官方的标准写法，而且 WHERE 子句在某些时候会影响查询的性能。
- 内连接可以查询两个或两个以上的表。
- 当对多个表进行查询时，要在 SELECT 语句后面指定字段是来源于哪一张表。因此，在多表查询时，SELECT 语句后面的写法是`表名.列名`。另外，如果表名非常长的话，也可以给表设置别名，这样就可以直接在 SELECT 语句后面写上`表的别名.列名`。

举例：

在 tb_students_info 表和 tb_course 表之间，使用内连接查询学生姓名和相对应的课程名称

```sql
SELECT s.name,c.course_name FROM tb_students_info s INNER JOIN tb_course c 
ON s.course_id = c.id;
```
## LEFT/RIGHT JOIN：外连接

外连接会先将连接的表分为基表和参考表，再以基表为依据返回满足和不满足条件的记录。外连接可以分为左外连接和右外连接

### LEFT JOIN：左连接

左外连接又称为左连接，使用 LEFT OUTER JOIN 关键字连接两个表，并使用 ON 子句来设置连接条件。

格式：

```sql
SELECT <字段名> FROM <表1> LEFT OUTER JOIN <表2> <ON子句>
```

含义：

- 字段名：需要查询的字段名称。
- <表1><表2>：需要左连接的表名。
- LEFT OUTER JOIN：左连接中可以省略 OUTER 关键字，只使用关键字 LEFT JOIN。
- ON 子句：用来设置左连接的连接条件，不能省略。

注意：

- 上述语法中，“表1”为基表，“表2”为参考表。左连接查询时，可以查询出“表1”中的所有记录和“表2”中匹配连接条件的记录。如果“表1”的某行在“表2”中没有匹配行，那么在返回结果中，“表2”的字段值均为空值（NULL）。
- 多个表左/右连接时，在 ON 子句后连续使用 LEFT/RIGHT OUTER JOIN 或 LEFT/RIGHT JOIN 即可。

举例：

在 tb_students_info 表和 tb_course 表中查询所有学生姓名和相对应的课程名称，包括没有课程的学生

```sql
SELECT s.name,c.course_name FROM tb_students_info s LEFT OUTER JOIN tb_course c 
ON s.course_id=c.id;
```



### RIGHT JOIN：右连接

右外连接又称为右连接，右连接是左连接的反向连接。使用 RIGHT OUTER JOIN 关键字连接两个表，并使用 ON 子句来设置连接条件。

格式：

```sql
SELECT <字段名> FROM <表1> RIGHT OUTER JOIN <表2> <ON子句>
```

含义：

- 字段名：需要查询的字段名称。
- <表1><表2>：需要右连接的表名。
- RIGHT OUTER JOIN：右连接中可以省略 OUTER 关键字，只使用关键字 RIGHT JOIN。
- ON 子句：用来设置右连接的连接条件，不能省略。

注意：

- 右连接以“表2”为基表，“表1”为参考表。右连接查询时，可以查询出“表2”中的所有记录和“表1”中匹配连接条件的记录。如果“表2”的某行在“表1”中没有匹配行，那么在返回结果中，“表1”的字段值均为空值（NULL）。
- 多个表左/右连接时，在 ON 子句后连续使用 LEFT/RIGHT OUTER JOIN 或 LEFT/RIGHT JOIN 即可。

举例：

在 tb_students_info 表和 tb_course 表中查询所有课程，包括没有学生的课程

```sql
SELECT s.name,c.course_name FROM tb_students_info s RIGHT OUTER JOIN tb_course c 
ON s.course_id=c.id;
```

## FULL JOIN：全连接

只要其中某个表存在匹配，FULL JOIN 关键字就会返回行。(返回JOIN 两端表的所有数据，无论其与另一张表有没有匹配。显示左连接、右连接和内连接的并集)

格式：

```sql
SELECT <字段名> FROM <表1> FULL OUTER JOIN <表2> <ON子句>
```

含义：

- 字段名：需要查询的字段名称。
- <表1><表2>：需要右连接的表名。
- FULL OUTER JOIN：全连接中可以省略 OUTER 关键字，只使用关键字 FULL JOIN。
- ON 子句：用来设置全连接的连接条件，不能省略。

举例：

在 tb_students_info 表和 tb_course 表中查询所有课程和所有学生，包括没有学生的课程以及没有课程的学生

```sql
SELECT s.name,c.course_name FROM tb_students_info s FULL OUTER JOIN tb_course c 
ON s.course_id=c.id;
```

## MySQL各种连接总结

![在这里插入图片描述](https://img-blog.csdnimg.cn/4f3f037175d443a1ba09f67b98cae9a4.png)

## 子查询

通过子查询可以实现多表查询。子查询指将一个查询语句嵌套在另一个查询语句中。子查询可以在 SELECT、UPDATE 和 DELETE 语句中使用，而且可以进行多层嵌套。在实际开发时，子查询经常出现在 WHERE 子句中。

格式：

```sql
WHERE <表达式> <操作符> (子查询)
```

含义：

操作符可以是比较运算符和 IN、NOT IN、EXISTS、NOT EXISTS 等关键字。

- IN | NOT IN：当表达式与子查询返回的结果集中的某个值相等时，返回 TRUE，否则返回 FALSE；若使用关键字 NOT，则返回值正好相反。
- EXISTS | NOT EXISTS：用于判断子查询的结果集是否为空，若子查询的结果集不为空，返回 TRUE，否则返回 FALSE；若使用关键字 NOT，则返回的值正好相反。

注意：

- 习惯上，外层的 SELECT 查询称为父查询，圆括号中嵌入的查询称为子查询（子查询必须放在圆括号内）。MySQL 在处理上例的 SELECT 语句时，执行流程为：先执行子查询，再执行父查询。

举例：

使用子查询在 tb_students_info 表和 tb_course 表中查询学习 Java 课程的学生姓名

```sql
SELECT name FROM tb_students_info 
WHERE course_id IN (SELECT id FROM tb_course WHERE course_name = 'Java');
```

在 tb_course 表和 tb_students_info 表中查询出所有学习 Python 课程的学生姓名

```sql
SELECT name FROM tb_students_info
WHERE course_id = (SELECT id FROM tb_course WHERE course_name = 'Python');
```

## INSERT：向表中插入数据

使用 INSERT 语句可以向数据库已有的表中插入一行或者多行元组数据。

格式1：

```sql
INSERT INTO <表名> [ <列名1> [ , … <列名n>] ]
VALUES (值1) [… , (值n) ];
```

含义1：

- <表名>：指定被操作的表名。
- <列名>：指定需要插入数据的列名。若向表中的所有列插入数据，则全部的列名均可以省略，直接采用 INSERT<表名>VALUES(…) 即可。
- VALUES 或 VALUE 子句：该子句包含要插入的数据清单。数据清单中数据的顺序要和列的顺序相对应。

格式2：

```sql
INSERT INTO <表名>
SET <列名1> = <值1>,
        <列名2> = <值2>,
        …
```

含义2：

- 用于直接给表中的某些列指定对应的列值，即要插入的数据的列名在 SET 子句中指定，col_name 为指定的列名，等号后面为指定的数据，而对于未指定的列，列值会指定为该列的默认值。

注意：
- 使用 INSERT…VALUES 语句可以向表中插入一行数据，也可以插入多行数据；
- 使用 INSERT…SET 语句可以指定插入行中每列的值，也可以指定部分列的值；
- INSERT…SELECT 语句向表中插入其他表的数据。
- 采用 INSERT…SET 语句可以向表中插入部分列的值，这种方式更为灵活；
- INSERT…VALUES 语句可以一次插入多条数据。
- 当使用单条 INSERT 语句插入多行数据的时候，只需要将每行数据用圆括号括起来即可。
- INSERT 语句后面的列名称顺序可以不是 tb_courses 表定义时的顺序，即插入数据时，不需要按照表定义的顺序插入，只要保证值的顺序与列字段的顺序相同就可以。


举例：

在 tb_courses 表中插入一条新记录，course_id 值为 2，course_name 值为“Database”，course_grade 值为 3，info值为“MySQL”。

```sql
INSERT INTO tb_courses
(course_name,course_info,course_id,course_grade)
VALUES('Database','MySQL',2,3);
```

从 tb_courses 表中查询所有的记录，并将其插入 tb_courses_new 表中。

举例：

```sql
INSERT INTO tb_courses_new
(course_id,course_name,course_grade,course_info)
SELECT course_id,course_name,course_grade,course_info
FROM tb_courses;
```

## UPDATE：修改表中数据

使用 UPDATE 语句可以修改、更新一个或多个表的数据。

格式：

```sql
UPDATE <表名> SET 字段 1=值 1 [,字段 2=值 2… ] [WHERE 子句 ]
[ORDER BY 子句] [LIMIT 子句]
```

含义：

- <表名>：用于指定要更新的表名称。
- SET 子句：用于指定表中要修改的列名及其列值。其中，每个指定的列值可以是表达式，也可以是该列对应的默认值。如果指定的是默认值，可用关键字 DEFAULT 表示列值。
- WHERE 子句：可选项。用于限定表中要修改的行。若不指定，则修改表中所有的行。
- ORDER BY 子句：可选项。用于限定表中的行被修改的次序。
- LIMIT 子句：可选项。用于限定被修改的行数。

注意：

- 修改一行数据的多个列值时，SET 子句的每个值用逗号分开即可。
- 若只是更新部分行的数据，保证 UPDATE 以 WHERE 子句结束，通过 WHERE 子句指定被更新的记录所需要满足的条件，如果忽略 WHERE 子句，MySQL 将更新表中所有的行。

举例：

在 tb_courses_new 表中，更新所有行的 course_grade 字段值为 4

```sql
UPDATE tb_courses_new
SET course_grade=4;
```

在 tb_courses 表中，更新 course_id 值为 2 的记录，将 course_grade 字段值改为 3.5，将 course_name 字段值改为“DB”

```sql
UPDATE tb_courses_new
SET course_name='DB',course_grade=3.5
WHERE course_id=2;
```

## DELETE：删除表中数据

使用 DELETE 语句可以删除表的一行或者多行数据。

格式：

```sql
DELETE FROM <表名> [WHERE 子句] [ORDER BY 子句] [LIMIT 子句]
```

含义：

- <表名>：指定要删除数据的表名。
- ORDER BY 子句：可选项。表示删除时，表中各行将按照子句中指定的顺序进行删除。
- WHERE 子句：可选项。表示为删除操作限定删除条件，若省略该子句，则代表删除该表中的所有行。
- LIMIT 子句：可选项。用于告知服务器在控制命令被返回到客户端前被删除行的最大值。

注意：

- 在不使用 WHERE 条件的时候，将删除所有数据。

举例：

删除 tb_courses_new 表中的全部数据

```sql
DELETE FROM tb_courses_new;
```

在 tb_courses_new 表中，删除 course_id 为 4 的记录

```sql
DELETE FROM tb_courses
WHERE course_id=4;
```

# MySQL常见面试题

## 查找入职员工时间排名倒数第三的员工所有信息

有一个员工employees表简况如下:
```sql

drop table if exists  `employees` ; 
CREATE TABLE `employees` (
`emp_no` int(11) NOT NULL,
`birth_date` date NOT NULL,
`first_name` varchar(14) NOT NULL,
`last_name` varchar(16) NOT NULL,
`gender` char(1) NOT NULL,
`hire_date` date NOT NULL,
PRIMARY KEY (`emp_no`));
INSERT INTO employees VALUES(10001,'1953-09-02','Georgi','Facello','M','1986-06-26');
INSERT INTO employees VALUES(10002,'1964-06-02','Bezalel','Simmel','F','1985-11-21');
INSERT INTO employees VALUES(10003,'1959-12-03','Parto','Bamford','M','1986-08-28');
INSERT INTO employees VALUES(10004,'1954-05-01','Chirstian','Koblick','M','1986-12-01');
INSERT INTO employees VALUES(10005,'1955-01-21','Kyoichi','Maliniak','M','1989-09-12');
INSERT INTO employees VALUES(10006,'1953-04-20','Anneke','Preusig','F','1989-06-02');
INSERT INTO employees VALUES(10007,'1957-05-23','Tzvetan','Zielinski','F','1989-02-10');
INSERT INTO employees VALUES(10008,'1958-02-19','Saniya','Kalloufi','M','1994-09-15');
INSERT INTO employees VALUES(10009,'1952-04-19','Sumant','Peac','F','1985-02-18');
INSERT INTO employees VALUES(10010,'1963-06-01','Duangkaew','Piveteau','F','1989-08-24');
INSERT INTO employees VALUES(10011,'1953-11-07','Mary','Sluis','F','1990-01-22');
```



请你查找employees里入职员工时间排名倒数第三的员工所有信息

(注意：可能会存在同一个日期入职的员工，所以入职员工时间排名倒数第三的员工可能不止一个。)

解答：

```sql
SELECT * FROM employees
WHERE hire_date = (
    SELECT DISTINCT hire_date FROM employees
    ORDER BY hire_date DESC
    LIMIT 1 OFFSET 2
)
```

## 查找当前薪水详情以及部门编号dept_no

有一个全部员工的薪水表salaries和一个各个部门的领导表dept_manager简况如下:

```sql

drop table if exists  `salaries` ; 
drop table if exists  `dept_manager` ; 
CREATE TABLE `salaries` (
`emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`from_date`));
CREATE TABLE `dept_manager` (
`dept_no` char(4) NOT NULL,
`emp_no` int(11) NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`dept_no`));
INSERT INTO dept_manager VALUES('d001',10002,'9999-01-01');
INSERT INTO dept_manager VALUES('d002',10006,'9999-01-01');
INSERT INTO dept_manager VALUES('d003',10005,'9999-01-01');
INSERT INTO dept_manager VALUES('d004',10004,'9999-01-01');
INSERT INTO salaries VALUES(10001,88958,'2002-06-22','9999-01-01');
INSERT INTO salaries VALUES(10002,72527,'2001-08-02','9999-01-01');
INSERT INTO salaries VALUES(10003,43311,'2001-12-01','9999-01-01');
INSERT INTO salaries VALUES(10004,74057,'2001-11-27','9999-01-01');
INSERT INTO salaries VALUES(10005,94692,'2001-09-09','9999-01-01');
INSERT INTO salaries VALUES(10006,43311,'2001-08-02','9999-01-01');
INSERT INTO salaries VALUES(10007,88070,'2002-02-07','9999-01-01');
```

请你查找各个部门当前领导的薪水详情以及其对应部门编号dept_no，输出结果以salaries.emp_no升序排序，并且请注意输出结果里面dept_no列是最后一列

解答：

```sql
SELECT s.emp_no, s.salary, s.from_date, s.to_date, d.dept_no 
FROM salaries AS s RIGHT JOIN dept_manager AS d 
ON s.emp_no=d.emp_no  
ORDER BY s.emp_no
```

## 获取每个部门中当前员工薪水最高的相关信息

有一个员工表dept_emp,有一个薪水表salaries简况如下:

```sql
drop table if exists  `dept_emp` ; 
drop table if exists  `salaries` ; 
CREATE TABLE `dept_emp` (
`emp_no` int(11) NOT NULL,
`dept_no` char(4) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`dept_no`));
CREATE TABLE `salaries` (
`emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`from_date`));
INSERT INTO dept_emp VALUES(10001,'d001','1986-06-26','9999-01-01');
INSERT INTO dept_emp VALUES(10002,'d001','1996-08-03','9999-01-01');
INSERT INTO dept_emp VALUES(10003,'d002','1996-08-03','9999-01-01');

INSERT INTO salaries VALUES(10001,88958,'2002-06-22','9999-01-01');
INSERT INTO salaries VALUES(10002,72527,'2001-08-02','9999-01-01');
INSERT INTO salaries VALUES(10003,92527,'2001-08-02','9999-01-01');
```

获取每个部门中当前员工薪水最高的相关信息，给出dept_no, emp_no以及其对应的salary，按照部门编号dept_no升序排列

解答：

```sql
# 先找出各个部门最高的薪资，再找到各个员工的部门、薪资，联结查询后的两个表，这里筛选时需要两个条件，一个是部门，一个是最高薪资

SELECT a.dept_no,b.emp_no,a.salary
FROM
    (SELECT dept_no,MAX(salary) AS salary
    FROM dept_emp
    INNER JOIN salaries
    ON dept_emp.emp_no=salaries.emp_no
    GROUP BY dept_no) AS a
INNER JOIN
    (SELECT dept_no,dept_emp.emp_no,salary
    FROM dept_emp
    INNER JOIN salaries
    ON dept_emp.emp_no=salaries.emp_no)AS b
ON a.salary=b.salary
AND a.dept_no=b.dept_no
ORDER BY dept_no
```