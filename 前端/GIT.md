## git使用

### 1、参考文章

* 廖雪峰git教程 https://www.liaoxuefeng.com/wiki/896043488029600



### 2、思考🤔及注意点

* git 分布式版本管理，可以在本地使用。多人开发时需要一个中央服务存储来同步管理代码；可以采用github或者gitlab；
* `git log --pretty=oneline` 查看commit日志。HEAD代表当前版本；Origin代表远程分支;
* stage(index) 相当于购物车，commit 相当于结账；每个东西相当于一个文件，东西可以添加和去掉只在购物车有影响；一旦结账就会有历史记录；相当于存档；就可以通过`git reset --hard`追溯回来；
* PR (github中) 是指对于非项目组的人员，对项目中的bug进行修复，fork ——> commit ——>PR 合并到另外一个仓库中去；
* commit 从时间的维度上记录每一次的更新变化，像管道一节一节，随着提交的推移，不断增加；而分支则是从横向的角度；相当于又开辟了一个管线；
* `git diff`比较；`git diff` 比较工作区和暂存区；`git diff HEAD`比较暂存区和当前分支；`git diff commitId commitId` 比较提交的区别；
* `git reset` 重置；默认不会改变工作区，会把stage暂存区的文件回退到工作区，`git reset --hard commitid`会把当前提交记录重置为 commitid