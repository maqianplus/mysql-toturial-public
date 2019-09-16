# MySQL LIKE

**Summary**: in this tutorial, you will learn how to use the MySQL `LIKE` operator to query data based on a specified pattern.

## Introduction to MySQL `LIKE` operator

The `LIKE` operator is a logical operator that tests whether a string contains a specified pattern or not. Here is the syntax of the `LIKE` operator:

```mysql
expression LIKE pattern ESCAPE escape_character
```

The `LIKE` operator is used in the `WHERE` clause of the `SELECT` , `DELETE`, and `UPDATE` statements to filter data based on patterns.

MySQL provides two wildcard characters for constructing patterns: percentage `%` and underscore `_` .

- The percentage ( `%` ) wildcard matches any string of zero or more characters.
- The underscore ( `_` ) wildcard matches any single character.

For example, `s%` matches any string starts with the character `s` such as `sun` and `six`. The `se_` matches any string starts with  `se` and is followed by any character such as `see` and `sea`.

## MySQL `LIKE` operator examples

Let’s practice with some examples of using the `LIKE` operator. We will use the following `employees` table from the [sample database](http://www.mysqltutorial.org/mysql-sample-database.aspx) for the demonstration:

![Employees Table](http://www.mysqltutorial.org/wp-content/uploads/2013/02/employees_table.png)

### A) Using MySQL `LIKE` with the percentage (%) wildcard examples

This example uses the `LIKE `operator to find employees whose first names start with `a`:

```mysql
SELECT 
    employeeNumber, 
    lastName, 
    firstName
FROM
    employees
WHERE
    firstName LIKE 'a%';
```

[Try It Out](http://www.mysqltutorial.org/tryit/query/mysql-like/#1)

![MySQL LIKE Operator Example](http://www.mysqltutorial.org/wp-content/uploads/2009/12/MySQL-LIKE-Operator-Example.png)
In this example, MySQL scans the whole `employees` table to find employees whose first names start with the character `a` and are followed by any number of characters.

This example uses the `LIKE` operator to find employees whose last names end with `on` e.g., `Patterson`, `Thompson`:

```mysql
SELECT 
    employeeNumber, 
    lastName, 
    firstName
FROM
    employees
WHERE
    lastName LIKE '%on';
```

[Try It Out](http://www.mysqltutorial.org/tryit/query/mysql-like/#2)

![MySQL LIKE operator lastname pattern example](http://www.mysqltutorial.org/wp-content/uploads/2009/12/MySQL-LIKE-operator-lastname-pattern-example.png)

If you know the searched string is embedded inside in the middle of a string, you can use the percentage ( `%` ) wildcard at the beginning and the end of the pattern.

For example, to find all employees whose last names contain `on` , you use the following query with the pattern `%on%`

```mysql
SELECT 
    employeeNumber, 
    lastName, 
    firstName
FROM
    employees
WHERE
    lastname LIKE '%on%';
```

[Try It Out](http://www.mysqltutorial.org/tryit/query/mysql-like/#3)

![MySQL LIKE operator with prefix and suffix patterns](http://www.mysqltutorial.org/wp-content/uploads/2009/12/MySQL-LIKE-operator-with-prefix-and-suffix-patterns.png)

### B) Using MySQL `LIKE` with underscore( `_` ) wildcard examples

To find employees whose first names start with  `T` , end with `m`, and contain any single character between e.g., `Tom` , `Tim`, you use the underscore (_) wildcard to construct the pattern as follows:

```mysql
SELECT 
    employeeNumber, 
    lastName, 
    firstName
FROM
    employees
WHERE
    firstname LIKE 'T_m';
```

[Try It Out](http://www.mysqltutorial.org/tryit/query/mysql-like/#4)

![mysql-like-with-_-pattern](http://www.mysqltutorial.org/wp-content/uploads/2009/12/mysql-like-with-_-pattern.png)

### C) Using MySQL `LIKE` operator with the `NOT` operator example

The MySQL allows you to combine the `NOT` operator with the `LIKE` operator to find a string that does not match a specific pattern.

Suppose you want to search for employees whose last names don’t start with the character `B`, you can use the `NOT LIKE` with a pattern as shown in the following query:

```mysql
SELECT 
    employeeNumber, 
    lastName, 
    firstName
FROM
    employees
WHERE
    lastName NOT LIKE 'B%';
```

[Try It Out](http://www.mysqltutorial.org/tryit/query/mysql-like/#5)

![MySQL NOT LIKE example](http://www.mysqltutorial.org/wp-content/uploads/2009/12/MySQL-NOT-LIKE-example-1.png)

Note that the pattern is not case sensitive, therefore, the `b%` or `B%` pattern returns the same result.

## MySQL `LIKE` operator with `ESCAPE` clause

Sometimes the pattern, which you want to match, contains wildcard character e.g., 10%, _20, etc. In this case, you can use the `ESCAPE` clause to specify the escape character so that MySQL will interpret the wildcard character as a literal character. If you don’t specify the escape character explicitly, the backslash character `\` is the default escape character.

For example, if you want to find products whose product codes contain the string `_20` , you can use the pattern `%\_20%` as shown in the following query:

```mysql
SELECT 
    productCode, 
    productName
FROM
    products
WHERE
    productCode LIKE '%\_20%';
```

[Try It Out](http://www.mysqltutorial.org/tryit/query/mysql-like/#6)

Or you can specify a different escape character e.g., `$` by using the `ESCAPE` clause:

```mysql
SELECT 
    productCode, 
    productName
FROM
    products
WHERE
    productCode LIKE '%$_20%' ESCAPE '$';
```

[Try It Out](http://www.mysqltutorial.org/tryit/query/mysql-like/#7)

![MySQL LIKE ESCAPE example](http://www.mysqltutorial.org/wp-content/uploads/2009/12/MySQL-LIKE-ESCAPE-example.png)

The pattern `%$_20%` matches any string that contains the `_20` string.

In this tutorial, you have learned how to use the MySQL `LIKE` operator to query data based on patterns, which is more flexible than using comparison operators.

## Related Tutorials

- [MySQL SELECT](http://www.mysqltutorial.org/mysql-select-statement-query-data.aspx)
- [MySQL REGEXP: Search Based On Regular Expressions](http://www.mysqltutorial.org/mysql-regular-expression-regexp.aspx)
- [MySQL Boolean Full-Text Searches](http://www.mysqltutorial.org/mysql-boolean-text-searches.aspx)