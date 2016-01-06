#ubuntu12.04 config

##1 安装与卸载软件

###1.1 变更源：
```
sudo cp sources.list /etc/apt/sources.list
```

###1.2 执行更新：
```
sudo apt-get update
```

###1.3 卸载软件：
```
sudo apt-get purge deja-dup* aisleriot* brasero* gwibber* empathy* landscape-client-ui-install* mahjong* gnomine* totem* onboard* gnome-orca* usb-creator* gnome-sudoku* ubuntuone* software-center* memtest86+* gnome-bluetooth* shotwell* simple-scan* yelp* indicator-messages* update-manager* update-notifier*

sudo apt-get autoremove
```

###1.4 修复依赖：
```
sudo apt-get install -f
```

###1.5 更新软件：
```
sudo apt-get upgrade
```

##2 优化

###2.1 禁用guest：
```
sudo gedit /etc/lightdm/lightdm.conf
```
在末尾添加：
```
allow-guest=false
```

###2.2 删除gedit的备份文件：
```
sudo find / -name "*~" -print -exec rm -f {} \;
```