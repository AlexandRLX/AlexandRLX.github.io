---
title: Mac上用iTerm使用rz
author: c cm
layout: post
permalink: /mac_iterm_rz/
categories:
tags:
description:
---
1. 安装lrzsz

    `brew install lrzsz`

2. 下载iterm2-zmodem
    `git clone https://github.com/mmastrac/iterm2-zmodem.git`
    
3. iTerm里面设置Trigger，路径：Preferences-Profiles-Advanced-Trigger Edit

```
 Regular expression: rz waiting to receive.\*\*B0100
    Action: Run Silent Coprocess
    Parameters: /usr/local/bin/iterm2-send-zmodem.sh

    Regular expression: \*\*B00000000000000
    Action: Run Silent Coprocess
    Parameters: /usr/local/bin/iterm2-recv-zmodem.sh
```

登上远程服务器，`rz`就会弹出交互窗口啦~
