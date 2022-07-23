## MySqL查询语句书写顺序

```sql
STEP0: select 选择某些列进行数据展示 [distinct] 需要对结果做独一无二的限定
STEP1: from 考虑选择某数据表 [as] 取别名
STEP2: where 在选中的数据表后进行一定条件的筛选
STEP3：group by 筛选完后的数据可能需要进行分组
STEP4：having 分完组后的数据可能需要进行组内筛选
STEP5：order by 组也分完了，数据也根据分组筛选完毕，可能需要进行排序准备待展示了
STEP6：limit 排序过后，就是展示出来了，但是如果一个数据表几万条记录需要展示，难道全部显示吗，此时就需要限制展示条数了

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