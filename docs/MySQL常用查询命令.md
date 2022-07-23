## 查询数据表
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

## 去重
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

## 设置别名
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

## 限制查询结果的条数
当数据表中有上万条数据时，一次性查询出表中的全部数据会降低数据返回的速度，同时给数据库服务器造成很大的压力。这时就可以用 LIMIT 关键字来限制查询结果返回的条数。


### 指定初始位置：  
LIMIT 关键字可以指定查询结果从哪条记录开始显示，显示多少条记录。  

格式：
```
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
```
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
```
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

## 对查询结果进行排序
通过条件查询语句可以查询到符合用户需求的数据，但是查询到的数据一般都是按照数据最初被添加到表中的顺序来显示。为了使查询结果的顺序满足用户的要求，MySQL 提供了 ORDER BY 关键字来对查询结果进行排序。  

