# ubuntu常用配置

## Caps Lock 和 Esc互换
新建~/.Xmodmap
``` json
remove Lock = Caps_Lock
add Lock = Escape
keysym Caps_Lock = Escape
keysym Escape = Caps_Lock
```
