# Power Shell 连接 SQL SERVER

## 1. 下载SqlServer模块

###  为当前用户而不是以管理员身份安装

如果不能以管理员身份运行 PowerShell 会话，则使用以下命令为当前用户安装：

PowerShell复制

```powershell
Install-Module -Name SqlServer -Scope CurrentUser
```

### 覆盖先前版本的 SqlServer 模块

还可以使用 `Install-Module` 命令覆盖以前的版本。

## 2.SSMS 打开 PowerShell

右键数据库选择 启动 powershell

![image-20220104180627218](C:\Users\rx793\AppData\Roaming\Typora\typora-user-images\image-20220104180627218.png)

出现了SQLSERVER:\SQL的上下文

![image-20220104181017482](C:\Users\rx793\AppData\Roaming\Typora\typora-user-images\image-20220104181017482.png)

## 3. 使用命令查询表数据

```powershell
Invoke-Sqlcmd -Query "SELECT TOP(1) * FROM LogTest"
```


## 4. 原生power shell 连接 SQLSERVER:\SQL的上下文

```powershall
&{[System.Console]::Title = 'SQL Server Powershell';Import-Module -Name 'SqlServer' ;Convert-UrnToPath 'Server[@Name=''M5-A220571'']/Database[@Name=''testdb'']'|cd}
```

