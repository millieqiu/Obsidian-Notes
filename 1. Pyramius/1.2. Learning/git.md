# 基本操作

## 查看 git 倉庫
查看目前的專案綁定了哪些 git 倉庫：
```
git remote -v
```
發現只有沛米的 Azure，因此新增一行指令添加 github 倉庫：
```
git remote add github (url)
```
再次查看可以發現現在綁定了兩個倉庫。

```
git pull github main
```
這邊有兩個參數：`github` 遠端倉庫的名稱，`main` 分支的名稱。

```
git push origin main
```

