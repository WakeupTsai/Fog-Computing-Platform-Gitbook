# 帳號及權限設置

1. 加入使用者

```
sudo adduser <ACCOUNT> 
```

   2. 變更權限至可以使用sudo

```
sudo usermod -g sudo <ACCOUNT>
```

  也可以至/etc/sudoer 中加上 

```
 root    ALL=(ALL) ALL
 <ACCOUNT> ALL=(ALL) ALL  #加上這行
```



