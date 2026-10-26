# 零、Markdown的基本使用方法
## 1.标题
# 一级标题（通常用作文章大标题）
## 二级标题（最常用，用作段落小标题）
### 三级标题

## 2.文字强调
**加粗文字** （两边各两个星号）
*斜体文字* （两边各一个星号）
***加粗且斜体*** （三个星号）
~~删除线~~ （两边各两个波浪号）

## 3.列表
### 无序列表
- 第一项
- 第二项
  - 缩进就是子项（前面空两格）
  
### 有序列表
1. 第一步
2. 第二步

## 4.代码
### 行内代码
在命令行输入 `python main.py` 即可运行。

### 代码块（用三个反引号包围，并写上语言名称，可以高亮）
```python
def hello():
    print("Hello World")
```

## 5.链接与图片
[点击这里去百度](https://www.baidu.com)
![瑞士贤]("D:\AAA大汇总\本天才的专属文件夹\瑞士贤.jpg")
注意：链接是中括号 [] 包文字，小括号 () 包网址；图片前面多一个感叹号 !

## 6.引用（常用来引用别人的话或标注注意事项。）
> 这是一段引用文字。
> 可以换行继续写。

## 7.表格  用 | 分隔列，用 - 分隔表头。（不需要对齐，只要符号对了，渲染出来就好看）
| 姓名 | 年龄 | 职业 |
| --- | --- | --- |
| 张三 | 25 | 程序员 |
| 李四 | 30 | 产品经理 |

## 8.分割线（用三个或以上的 - 或 *。）
---
***


# 一、git的安装和下载
## 1.登录git官网
[git官网](https://git-scm.com/)
安装git，**不能放在中文目录下面**
桌面右键，选择open git bash，打开命令行
输入`git config --global user.name "用户名"`
`git config --global user.email "邮箱"`

## 2.创建自己的本地代码仓库
创建一个文件，然后右键，选择open git bash
然后初始化`git init`。会出现.git文件，不要动里面的内容

## 3.上传本地的项目
先`git add 文件名`，上传到了暂存区，有点像寄快递，先把东西放到快递盒里面
`git add .`就是把所有的代码上传上去

然后`git commit -m "新增了啥子有个备注信息"`，这个就可以添加到仓库了，还可以写备注，后面的 -m 是可选

## 4.查看日志
`git log`，可以查看仓库添加东西的信息
`git log --stat`，可以查看每次修改了什么文件

还有log里面有一个重要参数，是**commit id**
`git diff commit的id` 可以看到那次修改了什么东西，使用一个git的可视化插件就可以看到明显的对比

输入`git reset --hard[commit id]`或者`git checkout [commit id]` 就可以把内容回溯到那个节点

## 5.分支
就是一个项目可以有几个分支，他们版本不同，但是最后又可以合并
`git branch` 可以看到分支有哪些

一般git会自己创建一个**master**，一般用来保存经过测试的稳定代码，发布就用这个，一般不改
可以自己创建一个**develop**分支，一般用来保存开发过程中的代码 
用`git checkout -b develop` 就可以完成创建，在这个上面进行新的开发和测试

当完成了新功能的测试之后，需要合并
先输入提交的2条命令
然后输入`git checkout master` 进入分支
输入`git merge develop` 完成合并


---
# 二、创建并连接远程仓库
## 1.远程代码创建仓库
打开github
点击最上面的加号，点击new repository
然后填写名字和介绍，选择要不要公开
接下来是
- README.md 这个会直接显示在下面，作为介绍
- .gitignore 表示上传的时候忽略文件夹里面的哪个文件，直接把要忽略的文件名字写到这个文件里面就可以
在code的https里面找到链接

## 2.把远程仓库和本地代码库进行绑定
`git clone 远程仓库地址` 就可以绑定仓库了

`git remote add origin 仓库地址` origin可以是远程仓库的别名，随便取，这个要先有自己的本地文件

## 3.推送到远程
`git push origin master` github默认有一个mian分支，把master换成main
`git push origin main`

`git push <远程仓库名> <本地分支名>:<远程分支名>`
`git pull <远程仓库名> <本地分支名>` 

## 4.申请token
**settings-->Developer settings-->Personal access tokens-->Fine-grainde tokens** 然后新建就可以了
这样就可以连上了

或者用SSE也行，上面用的是HTTPS
` ssh-keygen -t rsa -C 邮箱`
找到  Your public key has been saved in 后面的这个文件里面找到他，复制里面的内容
然后再github上面，**settings-->SSH and GPG keys-->SSH Keys-->new ssh key**

## 总结
创建仓库
-->绑定仓库
-->切换到develop分支`git checkout -b develop`-b的话可以新建
（现在更推荐`git switch 分支名`/`git switch -c 新分支名`）
-->编写代码
-->`git add *`  暂存
-->`git commit -m ""` 提交
-->`git checkout master`切换回master
-->`git merge develop`执行这个合并修改好的代码
-->`git push origin master`推送到远程的仓库

---

# 三、UV实战教程

## 亮点
UV使用Rust写的
**Rust** 是一门现代的系统级编程语言。简单来说，它既有 C/C++ 那样“贴近底层、运行极快”的性能，又通过极其严格的规则，从根本上杜绝了内存安全漏洞。

[UV官网](https://docs.astral.sh/uv/)

## uv 的逻辑是：项目即环境。

**不用提前建环境：** 你只需要在项目文件夹里输入 uv init。它会自动生成一个 pyproject.toml（这个文件就是你的“点菜清单”）。

**自动管理解释器：** 你以前要自己下载安装 Python（没python用不了pip），现在你在项目里说一句“我要用 Python 3.12”，uv 发现你没装的话，它会静默帮你下载好。你不需要去官网找安装包。

**PyCharm 对接更简单：** 在 PyCharm 里，你直接选“uv”，它会自动扫描项目里的那个清单（pyproject.toml），然后自动把该装的包都装在项目目录下的 .venv 文件夹里。

## 基本语法
|命令|用途|对应传统命令|
|:-:|:-:|:-:|
|uv venv|在当前目录创建虚拟环境 (.venv)|python -m venv .venv|
|uv pip install <pkg>|安装指定的 Python 包|pip install <pkg>|
|uv pip freeze|列出已安装的包及其版本|pip freeze|
|uv pip compile|将 pyproject.toml 转为 requirements.txt|pip-compile|
|uv pip sync|根据 lock 文件同步环境（删除多余包）|pip-sync|

## UV项目管理（新一代工作流）
如果你在开发一个完整的项目，这个是 uv 的项目模式，它会自动处理虚拟环境。

|命令|用途|
|:-:|:-:|
|uv init|在当前文件夹初始化一个新的 Python 项目（生成 pyproject.toml）。**文件路径不能有中文**
|uv python find|查看当前项目正在使用的是哪个路径下的 Python。
|uv add <pkg>|添加依赖并自动更新 pyproject.toml 和锁文件。
|uv remove <pkg>|移除依赖。
|uv sync|确保项目环境与锁文件完全一致。
|uv run <script.py>|最强命令之一。它会自动在虚拟环境中运行脚本，如果环境不存在，它会帮你建好。

## Python 版本管理
再也不需要 pyenv 或手动下载 Python 了。

|命令|用途|
|:-:|:-:|
|uv python install 3.12|下载并安装指定版本的 Python。
|uv python list|查看系统中已安装的和可供下载的 Python 版本。
|uv python pin 3.11|固定当前项目使用的 Python 版本。

## 工具运行 (uvx)
如果你只想临时运行一个工具（比如 ruff 或 black），而不想把它安装到全局：

uvx <tool>：下载、缓存并运行一个 Python 工具。
比如：uvx ruff check .


## 使用init之后会有这些文件
1. **pyproject.toml**  —— 项目的“大脑”
这是最重要的一个文件。在现代 Python 开发中，它取代了以前乱七八糟的 setup.py、requirements.txt 和各种工具的配置文件。
- 干嘛用的：它记录了项目的元数据（名字、版本、作者）以及项目依赖。
- 怎么用：当你运行 ``uv add pillow``  时，uv 会自动把 pillow 写进这个文件里。以后你把项目发给别人，别人只需要运行 ``uv sync`` ，uv 就会根据这个文件里的清单，把所有的包原封不动地装好。

2. readme.md —— 项目的“脸面”
这是一个标准的 Markdown 文档。
- 干嘛用的：用来写项目的自我介绍。

3. .gitignore —— 项目的“过滤器”
- 干嘛用的：用 Git 来管理代码，这个文件会告诉 Git：“哪些东西不要上传”。
- 为什么重要：uv 自动帮你写好了规则。它会忽略 .venv（虚拟环境文件夹）。因为虚拟环境很大且因人而异，我们通常只分享代码和配置文件（如 pyproject.toml），让别人在自己电脑上重新生成环境。

4. .python-version —— 版本的“锚点”
这是 uv 非常贴心的一个设计。
- 干嘛用的：它里面只写了一个版本号（比如 3.12）。
- UV最大优势：当你在这个文件夹下运行 uv run 时，uv 会先看一眼这个文件。如果它发现你系统里没装 3.12，它会自动帮你下载一个纯净的 3.12 放在缓存里，确保你的项目永远运行在正确的 Python 版本上。

#### *而且这个和anaconda不冲突

---

# 四、Ruff
## 一个极其快速的 Python 助页和代码格式化器，用 Rust 编写。

[Ruff官网](https://docs.astral.sh/ruff/)

- 可以作为项目依赖安装
`uv add --dev ruff`
- 可以作为全局环境安装
`uv tool install ruff`

## 核心命令：检查代码问题 (ruff check)
这是 Ruff 作为 Linter 最常用的命令，用来找出代码里的错误和不良写法。

- 基本检查：扫描当前目录下的所有 Python 文件。

``` bash
ruff check .
```

- 自动修复：加上 --fix，Ruff 会尝试自动修掉能修的问题（比如删除没用的导入、调整格式）。

```bash
ruff check --fix .
```

- 只检查特定规则：如果你只想检查某类问题（比如行太长），可以用 --select。例如，只看 E501（行长度超限）：

```bash
ruff check --select E501 .
```

- 查看规则说明：想知道某个错误代码具体是什么意思，可以用 ruff rule 查询。

```bash
ruff rule E501
```

## 核心命令：统一代码格式 (ruff format)
这是 Ruff 作为 Formatter 的功能，用来把代码排版得整整齐齐（风格类似 Black）。

- 格式化代码：直接修改文件，让代码符合统一风格。

```bash
ruff format .
```

- 只检查不修改：如果你只想看代码格式对不对，不想改文件（比如在 CI 里用），加上 --check。

```bash
ruff format --check .
```

- 预览会改什么：加上 --diff，它会显示格式化前后的差异，但不会真的动你的文件。

```bash
ruff format --diff .
```

## 推荐组合用法
在提交代码前，一个很顺手的流程是先让 Ruff 检查并自动修复问题，然后再统一格式化。因为 --fix 可能会调整代码结构（比如重排导入），格式化能随后把排版收拾干净。

```bash
# 先自动修复能修的问题，再格式化
uv run ruff check --fix . && uv run ruff format .
```

---

# 五、