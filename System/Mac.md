### Mac 系统问题

- App 在 `macOS Catalina` 下提示已损坏无法打开

  在终端输入以下命令

```shell
sudo xattr -d com.apple.quarantine /Applications/xxxx.app
```

- 英语系统环境下，Office显示中文界面

```bash
defaults write com.microsoft.Excel AppleLanguages '("zh-cn")'
defaults write com.microsoft.Powerpoint AppleLanguages '("zh-cn")'
defaults write com.microsoft.Word AppleLanguages '("zh-cn")'
```

