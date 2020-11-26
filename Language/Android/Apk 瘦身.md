## Apk 瘦身方案

- CPU架构过滤

  - 使用 `abiFilters`

    ```groovy
    ndk {
        abiFilters "armeabi", "armeabi-v7a", "arm64-v8a", "x86", "x86_64"
    }
    ```

  - 分架构打包

    - 在 flutter 中使用 `flutter build apk --flavor dev --split-per-abi` 打多个包

- 压缩图片

  - 使用 `TinyPng` 压缩图片

- 移除未使用的资源

- 代码混淆

