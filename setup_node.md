自从出过 IO.js 这个幺蛾子之后，Node.js 的版本迭代速度异常快。我的机子上至少会有三个版本的 Node.js，一个是 LTS 的稳定版本，用来主力开发。另外一个就是最新版本，用来把玩一下新的特性。

有了 nvm(Node Version Manager) 这个工具之后，你就可以轻松应对 Node.js 版本很多，时常需要切换版本的问题。

完整的安装指引可以直接访问 nvm 的[项目主页](https://github.com/creationix/nvm#install-script)：

下面我会在 Mac 系统上演示一次：

```bash
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.0/install.sh | bash
```

这个操作会把 nvm 安装在 `~/.nvm` 的这个目录，大部分情况下安装脚本会自动在把`~/.bash_profile`, `~/.zshrc`，`~/.profile` 或者 `~/.bashrc` 添加启动脚本，这样你就能在命令行里使用 `nvm` 命令。

如果脚本运行完之后，系统显示无法找到 `nvm` 命令。那么你需要手动地把以下代码添加到命令行的配置文件，也就是上面四个文件的其中一个（根据你所使用的命令行环境）。添加完后记得 `source` 一下或者重启命令行：

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm
```

可以来验证一下 `nvm` 已经成功安装了：
```bash
$ nvm --version
0.32.0
```

因为众所周知的原因，无论是安装 Node.js 还是使用 npm 安装 Node.js 的各种第三方包，速度都会非常地恶心...所以几乎所有的大型软件仓库，都会在国内有各种镜像:) 所以我一般都会做以下设置。

在命令行设置文件(我的是 `.zshrc`)里添加以下环境变量：

```bash
 export NVM_NODEJS_ORG_MIRROR="https://npm.taobao.org/dist" # Node.js 的镜像
 export ELECTRON_MIRROR="http://npm.taobao.org/mirrors/electron/" # Electron 的镜像
```

然后在 `~/` 下面创建 `.npmrc` 文件，内容是：

```bash
 registry=https://registry.npm.taobao.org/  # npm 的镜像
 ```

现在我们可以来安装 Node.js 啦：

```bash
$ nvm install 6 #先来一个最新的 LTS 版本
$ nvm alias default 6 #这会把上面安装的版本设置为 nvm 使用的默认版本，每次打开命令行就可以直接用
$ node --version
v6.6.0
```

然后可以再安装个 Node.js 4.4（原来的项目一直在用 4.4 T_T）：
```bash
$ nvm install 4.4
$ nvm use 4.4
$ node --version
v4.4.7
```

可以看一下你安装了那些版本，当前用的是哪一个：
```bash
$ nvm ls
     v6.6.0
->   v4.4.7
default -> 6 (-> v6.6.0)
node -> stable (-> v6.6.0) (default)
stable -> 6.6 (-> v6.6.0) (default)
iojs -> N/A (default)
```