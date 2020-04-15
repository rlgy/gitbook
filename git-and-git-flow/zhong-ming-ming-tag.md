---
description: Git 重命名tag 并同步到远程仓库
---

# 重命名Tag

假设需要将本地的tag 1.1.0 重命名为 v1.1.0 , 并且同步到远程仓库

第一步: 新建Tag

```text
git tag v1.1.0 1.1.0 // 使用的命令 git tag newTag oldTag
```

第二步: 删除旧Tag

```text
git tag -d 1.1.0    // git tag -d 删除一个本地tag
```

第三步: 删除远程仓库的Tag

```text
git push origin :refs/tags/1.1.0
```

第四步: 将新Tag推送到远程仓库

```text
git push --tags
```

