# 基本操作

## 查看 git 倉庫
查看目前的專案綁定了哪些 git 倉庫：
```shell
git remote -v
```
發現只有沛米的 Azure，因此新增一行指令添加 github 倉庫：
```shell
git remote add github (url)
```
再次查看可以發現現在綁定了兩個倉庫。

```shell
git pull github main
```
這邊有兩個參數：`github` 遠端倉庫的名稱，`main` 分支的名稱。

```shell
git push origin main
```

# 學習筆記 - 為你自己學 git

> Reference
> [為你自己學 Git](https://www.kobo.com/tw/zh/ebook/git-6)
> [Git & GitHub 教學手冊](https://w3c.hexschool.com/git/cfdbd310)
> [【Git】從零開始學習 Git - 30 天的學習筆記 - 鐵人賽系列文](https://ithelp.ithome.com.tw/users/20141010/ironman/4499)

### 什麼是 Git？
Git 是一種分散式的版本控制系統。