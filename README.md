#ubuntu12.04 config

##1 安装与卸载软件

###1.1 变更源：
```
sudo cp ubuntu-config/files/sources.list /etc/apt/sources.list
```

###1.2 执行更新：
```
sudo apt-get update
```

###1.3 卸载软件：
```
sudo apt-get purge deja-dup* aisleriot* brasero* gwibber* empathy* landscape-client-ui-install* mahjong* gnomine* totem* onboard* gnome-orca* usb-creator* gnome-sudoku* ubuntuone* software-center* memtest86+* gnome-bluetooth* shotwell* simple-scan* yelp* indicator-messages* ibus

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

###1.6 安装软件：
```
sudo apt-get install build-essential audacious p7zip-full p7zip-rar openjdk-7-jdk vlc git-core git-cola xpad chromium-browser gdebi network-manager-gnome conky
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

###2.3 给chromium/firefox安装flash插件：
```
sudo cp ubuntu-config/flash_player/libflashplayer.so /usr/lib/chromium-browser/plugins/
sudo cp ubuntu-config/flash_player/libflashplayer.so /usr/lib/firefox/browser/plugins/
sudo cp -r ubuntu-config/flash_player/usr/* /usr
```

###2.4 用goagent翻墙：
```
sudo chmod 777 /home/sun/.goagent/local/proxy.py
sudo chmod 777 /home/sun/.goagent/goagent.run
sudo ln -s /home/sun/.goagent/goagent.run /usr/bin/goagent
```

###2.5 添加开机自启：
```
/home/sun/.conky/startconky
xpad -N
```

## 3.ppa软件

###3.1 安装搜狗拼音：
```
sudo add-apt-repository ppa:fcitx-team/nightly
sudo apt-get update
sudo apt-get install fcitx-sogoupinyin fcitx-config-gtk
```

###3.2 安装sublime:
```
sudo add-apt-repository ppa:webupd8team/sublime-text-2
sudo apt-get update
sudo apt-get install sublime-text
```

####3.2.1 序列号(2221)：
```
—– BEGIN LICENSE —–
Andrew Weber
Single User License
EA7E-855605
813A03DD 5E4AD9E6 6C0EEB94 BC99798F
942194A6 02396E98 E62C9979 4BB979FE
91424C9D A45400BF F6747D88 2FB88078
90F5CC94 1CDC92DC 8457107A F151657B
1D22E383 A997F016 42397640 33F41CFC
E1D0AE85 A0BBD039 0E9C8D55 E1B89D5D
5CDB7036 E56DE1C0 EFCC0840 650CD3A6
B98FC99C 8FAC73EE D2B95564 DF450523
—— END LICENSE ——
```

####3.2.2 添加到user-key-setting:
```
{ "keys": ["ctrl+alt+f"], "command": "reindent" }
```

####3.2.3 设置是否记录上次打开
在Preferences->Settings Default
```
"hot_exit": false,
"remember_open_files": false,
```

####3.2.4 解决sublime无法输入中文的问题：

#####3.2.4.1 安装gtk环境：
```
sudo apt-get install libgtk2.0-dev
```

#####3.2.4.2 编译共享类库：
```
gcc -shared -o libsublime-imfix.so sublime_imfix.c  `pkg-config --libs --cflags gtk+-2.0` -fPIC
```

#####3.2.4.3 将libsublime-imfix.so复制到sublime目录下：
```
sudo cp libsublime-imfix.so /opt/sublime_text_2/
```

#####3.2.4.4 修改subl命令：
```
sudo cp /usr/bin/subl /usr/bin/subl.bak
sudo gedit /usr/bin/subl
```
将原有命令改为：
```
LD_PRELOAD=/opt/sublime_text_2/libsublime-imfix.so /opt/sublime_text_2/sublime_text --class=sublime-text-2 "$@"
```

#####3.2.4.5 卸载libgtk：
```
sudo apt-get purge libgtk2.0-dev
sudo apt-get autoremove
```

####3.2.5 安装插件：
```
import urllib2,os,hashlib; h = '7183a2d3e96f11eeadd761d777e62404' + 'e330c659d4bb41d3bdf022e94cab3cd0'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')
```
然后安装：
```
ConventToUtf8
markdown preview
```

##4 常见问题及解决
###4.1 chromium配置出错：
```
rm -rf .config/chromium/Default
```
