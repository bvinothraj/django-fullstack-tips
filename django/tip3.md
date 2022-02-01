---
layout: default
title: Django Backend Tips
description: A knowledge-sharing platform
---
# How to find the query associated with a queryset?

_Pardeep_ <br />
_Jan 31, 2022_ <br />

Sometime we want to know how a Django ORM ( Object Relation Mapper) makes our queries execute or what is the corresponding SQL of the code we are writing. This is very strightforward. You can get `str` of any `queryset.query` to get the sql.

You have a model called `Employee`. For getting all records, you will write something like `Employee.objects.all()`, then do `str(queryset.query)` <br />

### Example 1

```
>>> queryset = Employee.objects.all()
>>> str(queryset.query)
SELECT "employee"."id", "employee"."first_name", "employee"."last_name", 
"employee"."salary" FROM "employee"

```

### Example 2

```
>>> queryset = Employee.objects.filter(salary__gt=40000)
>>> str(queryset.query)
SELECT "employee"."id", "employee"."first_name", "employee"."last_name", 
"employee"."salary" FROM "employee" WHERE "employee"."salary" > 40000
```

[back](../)
