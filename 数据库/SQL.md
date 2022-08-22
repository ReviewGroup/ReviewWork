```sql
// 找字段重复出现的行
SELECT `item_id` FROM `item_competitor`GROUP BY `item_id`  HAVING COUNT( `item_id`)>1




```

####  

#### SQL JOIN

```sql
# SQL Join 思路：都是先做笛卡尔积，然后再筛选：筛选的执行顺序是 from, on...and... , where,group by,having,select,distinct,order by, limit 
#  left join 是左表全选  right join 是右表全选
join （inner join） 的简写，只返回两个表中连接字段相等的行，取的是交集
// left join后的 on and... 不能过滤左表，能过滤右表，可以where
// inner join 后的 on and可以过滤
https://zhuanlan.zhihu.com/p/29234064
```



#### SQL 条件判断
```sql
(case
    when condition1
    then value1
    when condition2
    then value2
    else value3 end)
if
    (condition1,value1,value2)
```

