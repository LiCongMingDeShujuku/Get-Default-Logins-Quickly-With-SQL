![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 快速获取默认登录信息SQL
#### Get Default Logins Quickly With SQL
**发布-日期: 2018年03月20日 (评论)**

![#](images/get-default-logins-quiickly-with-sql-a.png?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
这里有一些可以获取在安装时自动创建的默认登录，以及安装完成后创建的默认登录的快速SQL逻辑。它旨在提取在安全设置的第一分钟内创建的所有登录。请注意，默认帐户的创建时间均为11:41（或者更早，如默认的“sa”帐户所示）

请记住，这仅显示在执行传统SQL Server安装时创建的登录，而不使用Reporting Services，Analysis Services等相关服务。



## English
Here’s some quick SQL logic which gets you the default logins automatically created at the point of installation, and also those created after the installation was already carried out. It’s designed to pull all logins that were created during the first minute of the security setup. Notice the time of creation of the default accounts are all at 11:41 (or earlier as in the default ‘sa’ account shows)
Keep in mind this only shows logins created whenever you perform a traditional SQL Server Installation without associated services such as Reporting Services, Analysis Services etc.


---
## Logic
```SQL

use master;
set nocount on
 
-- get date when sql server was installed
-- 获取安装sql server的日期
declare @install_date       datetime = (select [createdate] from syslogins where [sid] = 0x010100000000000512000000)
declare @default_accounts   datetime = (select dateadd(minute, 1, @install_date))
 
-- get all logins not associated with the installed accounts
-- 获取与已安装帐户无关的所有登录
select [createdate], [name] from syslogins where [createdate] > @default_accounts
 
-- get all default logins created during installation.
-- 获取安装期间创建的所有默认登录。
select [createdate], [name] from syslogins where [createdate] < @default_accounts

```

[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

