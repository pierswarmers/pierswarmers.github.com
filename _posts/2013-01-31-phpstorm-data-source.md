---
layout: post
title: PHPStorm Data Sources and JDBC
author: Piers Warmers
---

Setting up [PHPStorms](http://www.jetbrains.com/phpstorm/) database integration for [MySQL](#mysql-on-localhost) and [Microsoft SQL Server](#microsoft-sql-server-on-remote-server), I ran into a couple of small gotcha's which might be worth noting for anyone else struggling through some of the vague error messages.

To keep things brief I'll note the the server locations and JDBC libraries I used.

## MySQL On Localhost

I run a local MySQL server on my OS X machine (mysql-5.5.25a-osx10.6-x86_64). The JDBC driver I used was downloaded from [the source](http://dev.mysql.com/downloads/connector/j/) and unpacked into a safe location.

I used the package:

`mysql-connector-java-5.1.22-bin.jar`

…and the class:

`com.mysql.jdbc.Driver`

My server location looked something like:

`jdbc:mysql://localhost:3306/myDataBaseName`

Done and done!

## Microsoft SQL Server on Remote Server

It's pretty rare I get to play with SQL Server, but at least a couple of my ongoing projects use remote SQL Server access. This example is from a Microsoft SQL Server 2008R2 connection. The drivers can be [downloaded from Microsoft](http://msdn.microsoft.com/en-us/sqlserver/aa937724.aspx). Like above, I unpack them into a shared location and…

I used the package:

`jdbcsql.jar`

…and the class:

`com.microsoft.sqlserver.jdbc.SQLServerDriver`

My server location looked something like:

`jdbc:sqlserver://example.com:1433;databaseName=myDataBaseName`

Hope it helps!