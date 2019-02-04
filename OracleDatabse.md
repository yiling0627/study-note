<b>因为SQL的执行顺序为：
先where 再group 再having 再select 后order.
	
sql语句解析的顺序的问题。先where条件过滤出需要的纪录，再对筛选出来的记录分组group加having。接下来就是选取字段的过滤select最后order排序。所以别名只有在select和order by内才可以只用。</b>



###Substitution Variable
1. variable is not case-sensitive	
2. using the Double-Ampersand substitution variable	
the && define the variable and assign the value in the same time
3. use verify command to toggle the display of the substitution   variable both before and after SQL Developer replaces substitution variables with values(script output会详细写出变化前后的SQL语句)

		SET VERIFY ON
		SELECT employee_id, last_name, salary
		FROM employees
		WHERE EMPLOYEE_ID = &E_NUM;

4. if we need to use &t instead of variable t

		SET DEFINE OFF;
		SELCET * FROM DEPARTMENTS
		WHERE DEPARTEMENT_NAME LIKE '%&t%';
		
###Single-Row function
1. upper, lower, initcap
2. concat, substr(first_name,n,m), length
3. instr(first_name,x,n,m) 在first_name里面从n开始search 第m个x 的位置
4. Lpad: Lpad(salary,10,'#') 24000 -> #####24000
   Rpad, 
   replace(first_name,'a','#'), 
   trim
   
		   SELECT TRIM(' ' FROM '  khaled khudari  ') V From DUAL
		   SELECT TRIM(LEADING ' ' FROM '  khaled khudari  ') V From DUAL
		   SELECT TRIM(TRAILING ' ' FROM '  khaled khudari  ') V From DUAL
		   SELECT TRIM(BOTH ' ' FROM '  khaled khudari  ') V From DUAL
		   SELECT TRIM('k' FROM 'khaled khudari') V From DUAL
		   ->haled khudari
		   SELECT TRIM(LEADING 'k' FROM 'khaled khudari') V From DUAL
		   ->haled khudari
		   SELECT TRIM(TRAILING 'k' FROM 'khaled khudari') V From DUAL
		   ->khaled khudari
		  SELECT TRIM(' khaled khudari ') V From DUAL
		  ->default
	
5. Number Function: ROUND(10.55,1) -> 10.6
						ROUND(10.5) -> 11
						ROUND(101.5, -1) -> 100
						TRUNC(998.6565,-2) ->900
						MOD(15,2) -> 1
6. Data Function: DD-MM-RR RR->(50-99是19XX年，0-49是20XX年)
	MONTHs_BETWEEN(), add_months(hire_date,-2),   
	NEXT_DAY(sysdate,1) 1->sunday
	lastdate of the month LAST_DATE(sysdate)
	
	ROUND(),TRUNC()

###Conversion Function and Conditional Expression
implicit datatype conversion	
Varchar2 or Char <--> Number, Date	
explicit datatype conversion	
to_number,to_char <font color="blue">number</font> - <font color="red">character</font> - <font color="blue">date</font> to_date,to_char

<pre>TO_CHAR(date[,'format_model'])</pre>

fmDD MoNTH YYYY fm to remove space  MoNTH is case sensitive different from MONTH

fmDDspth -> seventh 7号

<pre>TO_CHAR(number[,'format_model'])</pre>



###
group by 不能用alias order by可以用
group function can be only nested two


###
is null, is not null. 写成 = null 不会return any data
所以 
in 意味 =any
in(100,101,null)不会返回 含有null的row
not in 意味 <>all
not in(100,101,null)什么都不返回

###DML,DDL,DCL,Transaction Control
DML:Data Manipulation Language - Select, Insert, Update, Delete, Merge	
DDL: Data Definition Language - Create, Alter, Drop, Rename, Truncate, Comment	
DCL: Data Control Language - Grant, Revoke	
Transaction Control: Commit, Rollback, SavePoint

######difference between Delete and truncate
1. DML statement - DDL statement
2. rollback - can't rollback
3. fire the trigger - not fire the trigger
4. could have where clause - no where clause
5. delete does not recover space - recover space

##transaction 需要学了PL之后回去看一下




