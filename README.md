![image](https://github.com/DreamMaoMao/mydot/assets/30348075/6aec7c13-bf7c-4332-bb46-88a40d508525)
![image](https://github.com/DreamMaoMao/mydot/assets/30348075/092b077e-aece-447c-b2c3-b52f30186237)
![image](https://github.com/DreamMaoMao/mydot/assets/30348075/300c2efb-49e6-467d-93ba-d7200cba1b78)
![image](https://github.com/DreamMaoMao/mydot/assets/30348075/9848fdea-9aca-4bfa-a910-76ca4a90d366)



https://github.com/DreamMaoMao/mydot/assets/30348075/daf2a4bb-1bb0-466e-aed8-9ffb7c9511f4



# dependency

```
paru -S hyprland-git waybar-hyprland-git  wofi xdg-desktop-portal-hyprland-git tty-clock-git swaylock grim slurp pokemon-colorscripts-git starship jq dunst wl-clipboard swaylock-effects-git swww-git
```

# other dependency:
```
nm-applet
blueman-manager
nautilus
rofi
gnome-terminal
gnome-system-monitor 
policykit-gnome
fcitx
xrdb
wlsunset 
wl-clip-xrdb 
clipman
swappy 
brightnessctl 
eww
bluetoothctl
bluetooth
```

# moving config files
```
git clone  https://github.com/DreamMaoMao/mydot.git
cd mydot
cp -r ./* ~/.config
```
# service
```
sudo systemctl enable bluetooth
```


# hyprland操作(配置-hypr/bindkey.conf)
想要更改快捷键绑定的应用的在这个文件改
## 工作区操作
|  选项   | 操作  |
|  ----  | ----  |
|切换到特定工作区| ctrl + 1-6(小键盘)
|移动工作区 |ctrl + 上下方向键

## 窗口操作
|  选项   | 操作  |
|  ----  | ----  |
|关闭窗口 |alt + q
|最大化窗口| alt + a
|窗口与主窗口(左边为主窗口)切换| alt + s
|移动窗口到特定工作区| alt + 1-6(小键盘)

## 系统操作
|  选项   | 操作  |
|  ----  | ----  |
|注销退出| super + m
|系统挂起| super + b

## 应用操作
|  选项   | 操作  |
|  ----  | ----  |
|打开wofi选择app|  alt + space
|剪贴板历史| super + v
|打开终端| alt + return
|打开文件浏览器| alt + e

## 鼠标操作
|  选项   | 操作  |
|  ----  | ----  |
|最大化一个窗口| 鼠标中键
|移动工作区| super + 鼠标滚轮
|拖动窗口| super + 按住鼠标右键移动
|调整窗口大小| super + 按住鼠标左键移动

# waybar操作(配置-hypr/component/waybar/config)
如果waybar有任何控件显示不正常 就要去这个配置下看看,修改成你自己的,一般以下
几个可能会需要修改一下
```
温度(hwmon-path选项):这个路径不大统一,找不到可以用这个路径/sys/class/thermal/thermal_zone*/temp 
背光(device选项):ls /sys/class/backlight/ 获得背光设备名
电池(bat选项):acpi -b 得到电池编号如果是0 那就是BAT0
```
```json
    "temperature": {
        "thermal-zone": 2,
        "hwmon-path": "/sys/class/thermal/thermal_zone*/temp",
        "critical-threshold": 10,
        "format-critical": "{temperatureC}°C",
        "format": ""
    },
    "backlight": {
        "interval":2,
        "device": "amdgpu_bl0",
        "format": "{percent}% {icon}",
        "format-icons": ["",""],
        "on-scroll-up":"~/.config/hypr/scripts/lightup",
        "on-scroll-down":"~/.config/hypr/scripts/lightdown",
        "smooth-scrolling-threshold":1
    },
    "battery": {
        "bat": "BAT0",
        "interval": 60,
        "states": {
            "warning": 30,      
            "critical": 60      
        },   
        "format": "{capacity}% {icon}",   
        "format-icons": ["", "", "", "", ""],
        "on-click-right":"~/.config/eww/System-Menu/launch",
        "on-click":"eww open-many --toggle background-closer powermenu"
    },
```
|  选项   | 操作  |
|  ----  | ----  |
|查看日期                |左键时间图标  
|打开系统监控            |左键cpu图标     
|打开蓝牙工具            |左键声音图标
|调整音量                |滑轮声音图标
|打开rofi选择app         |左键内存图标
|打开电源选项            |左键电池图标
|打开所以系统面板        | 右键电池图标
|打开网速监控           | 左键wifi图标
|打开文件浏览器          |   左键磁盘图标
|调整亮度               |   滑轮亮度图标
|关闭某个正在打开的窗口   |       右键窗口图标  
|切换到某个正在打开的窗口 |    左键窗口图标
|切换到某个工作区        |   左键工作区图标    


# 可能要修改的地方
## hypr/bingkey.conf
- terminal(这个改成你自己要的终端,我这里是gnome-terminal)
```conf
bind=ALT,RETURN,exec,gnome-terminal
```
- move workspace(code:83-87是右边小键盘,改成数字用的是正常的数字键盘)
```conf
bind=CTRL,code:87,workspace,1
bind=CTRL,code:88,workspace,2
bind=CTRL,code:89,workspace,3
bind=CTRL,code:83,workspace,4
bind=CTRL,code:84,workspace,5
bind=CTRL,code:85,workspace,6
```
- move window to worksapce(code:83-87是右边小键盘,改成数字用的是正常的数字键盘)
```conf
bind=ALT,code:87,movetoworkspace,1
bind=ALT,code:88,movetoworkspace,2
bind=ALT,code:89,movetoworkspace,3
bind=ALT,code:83,movetoworkspace,4
bind=ALT,code:84,movetoworkspace,5
bind=ALT,code:85,movetoworkspace,6
```

## hypr/exec.conf
- 权限认证工具的路径,policykit-gnome这个包安装好之后注意查看polkit-gnome-authentication-agent-1安装到那个路径下了
```conf
exec-once=/usr/local/libexec/polkit-gnome-authentication-agent-1 &
```


# Reference

- https://github.com/flick0/dotfiles/tree/dreamy

- https://github.com/Syndrizzle/hotfiles/tree/bspwm
