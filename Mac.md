- App 在 `macOS Catalina` 下提示已损坏无法打开

  在终端输入以下命令

```shell
sudo xattr -d com.apple.quarantine /Applications/xxxx.app
```

