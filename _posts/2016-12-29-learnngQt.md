---
layout: post
title: 在QT中使用sqlite
subtitle: 
author: Thursday
date: 2016-12-29 11:07:27 +0800
categories: qt
tag: qt
---

#### 在苹果上使用Qt连接sqlite时,使用如下代码连接数据库时候总会报错“out of memory"错误

```C++
bool connect(const QString &dbName)
{
    QSqlDatabase db = QSqlDatabase::addDatabase("QSQLITE");
    db.setDatabaseName("mydatabase.db");
    if (!db.open()) {
        qDebug() << "Database Error!";
        return false;
    }
    return true;
}
```

百度后得知可能是写入文件的权限问题，遵循这个思路加上用户目录下的绝对路径之后发现错误消失。 然而绝对路径不可靠，所以最好是获取到app运行的目录，

在文档中查找之后果然发现有两个方法

```
 QCoreApplication::applicationDirPath()
 //On macOS and iOS this will point to the directory actually containing the executable, which may be inside an application bundle (if the application is bundled).
 QCoreApplication::applicationFilePath()
```

由此想到在iOS开发中的bundle概念。。。
