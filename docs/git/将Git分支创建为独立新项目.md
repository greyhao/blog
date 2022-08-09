# 将 Git 分支创建为独立新项目

tag: git 使用记录

起因：需要将正在开发的一个项目，在其 dev 分支的基础上创建一个新的独立项目。

首先想到直接创建新分支进行开发，后期只要分支不合并也没有什么问题。

但是考虑到后面项目可以出去维护，所以还是独立为项目比较好，所以有了本篇记录。

1. 切到 dev 分支

   `# git checkout dev`

2. 复制项目为新项目

   `# cd ../ // 到工程所在目录`

   `# cp -r prj/ newprj/`

3. 切到新项目目录

   `# cd newprj`

4. 删除本地的分支

   `# git branch -D master // 其他无用分支也删除`

5. 将当前分支命名为 master 分支

   `# git branch -m master`

6. 修改仓库地址

   `# git remote set-url origin url // url 为新项目实际地址`

7. 修改对应远程分支

   ```
   # vim .git/config

   // 原内容
   [branch "master"]
      remote = origin
      merge = refs/heads/dev

    // 修改之后
    [branch "master"]
        remote = origin
        merge = refs/heads/master
   ```

8. 提交修改

   `git push origin master:master`
