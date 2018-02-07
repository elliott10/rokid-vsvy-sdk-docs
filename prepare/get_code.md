### 获取源码
* 安装repo 工具

```
mkdir ~/bin
curl https://storage.googleapis.com/git-repo-downloads/repo  > ~/bin/repo
chmod a+x ~/bin/repo
```
* 下载源码

```
mkdir <vsys_src>
cd <vsys_src>
repo init -u ssh://<user>@s.rokid-inc.com:29418/open-platform/client/manifests/vsys --no-repo-verify
repo sync
```

> 现在还是公司内部仓库，未来将开源到github

