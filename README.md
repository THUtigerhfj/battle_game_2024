# Project 2: Battle Game

## 前言

本课程的 Project 2 的设计主题是团队和创造。希望大家能够通过这个 Project 初步体会到利用 Git 仓库进行团队合作的感觉以及自由发挥创造力感受编程的快乐。
2022 年我们设计了这个坦克小游戏作为实验性的项目框架发布，那年我们体会到了同学们回馈的热情和创造力。
因此我们一直希望能够沿着这个思路为同学们提供更好的学习以及娱乐体验，一直在尝试构建一个更加完善的项目框架可以真正地把大家的创意融合成一个完整的作品。
然而事与愿违，由于 TA 的时间和能力有限，我们的项目框架一直没有得到很好的完善。去年的新项目框架没有能够在团队协作上发挥出更好的效果。
今年在连续几周的持续工作下，我们很遗憾地发现新的工程进度离理想的项目框架还有很大的差距，在 DDL 面前不得不妥协，复用了 2022 年的初版框架。
我们深感抱歉，也希望大家能够理解我们的困难，我们会继续努力，争取在未来的课程中完成我们的蓝图。

Project 2 的难度并不高，希望大家能在期末结束之后以一个放松地心态完成这个项目。

经过一个学期的学习，我们已经一起学习了许多编程知识，大家的编程技能想必也有了显著的提高。
与历次作业和第一次大作业单打独斗的体验不同，这个项目将由参与课程的所有同学共同完成，
你需要为这个代码仓库提交你的贡献，体验共同开发的乐趣。

这个项目的目标是制作一款内容丰富的对战小游戏。
同学们可以自由地发挥自己的创造力，设计各种奇妙有趣的游戏内容，添加绚丽的视觉效果。

## 构建

在拉取项目仓库时，你需要使用 `--recursive` 参数以拉取项目的子模块。

由于项目依赖 vcpkg，你还需要在某个你选定的非本仓库目录下的位置拉取 vcpkg 仓库。

```bash
git clone https://github.com/microsoft/vcpkg.git
```

在进行 CMake 配置阶段，你需要使用`-DCMAKE_TOOLCHAIN_FILE={vcpkg path}/scripts/buildsystems/vcpkg.cmake`参数指定 vcpkg 的 CMake 配置文件。

即 `cmake -S {repo path} -B {build path} -DCMAKE_TOOLCHAIN_FILE={vcpkg path}/scripts/buildsystems/vcpkg.cmake`

`cmake -S ~/Yao_Class/Introduction_to_Programming/battle_game_2024 -B ~/Yao_Class/Introduction_to_Programming/battle_game_2024/build -DCMAKE_TOOLCHAIN_FILE=~/Yao_Class/Introduction_to_Programming/vcpkg/scripts/buildsystems/vcpkg.cmake` 

项目的其他依赖还包括：

- [Vulkan SDK](https://vulkan.lunarg.com/sdk/home)
- [Python3](https://www.python.org/)

请确保你的环境中已经安装了这些依赖项。

Run the executable file:

`tiger@tigerThinkPad:~/Yao_Class/Introduction_to_Programming/battle_game_2024/build/src/battle_game$ ./battle_game`

## 任务

### 1、创建分叉（Fork）并提交 PR （Pull Request）【10 pts】

在一个团队合作的项目中，每个人提交的每一行代码都可能引发无法预料的后果，你的每一行代码在进入主仓库之前都需要经过严格的审核。
你不拥有对主仓库的写权限，在编写你贡献的新代码之前，你需要先从主仓库创建一个属于你自己的分叉（Fork）。在 GitHub 中，
实现这个操作只需要点击仓库主页面右上角的 `Fork` 按钮，并根据跳转页面的提示创建你的分叉。

在你的分叉仓库里，你可以对其进行任意的改动，这些都不会影响到主仓库的内容。

在你写完并提交了新的代码后，你可以通过创建 PR （Pull Request）的方式申请将你分叉仓库中新的代码合并到主仓库。
你可以通过仓库页面导航栏的 `Pull requests` 按钮进入 PR 页面。
在 PR 页面内，你可以点击偏右上方绿色的 `New pull request` 按钮进入 Pull Request 创建页面。
接下来根据页面中的提示和选项，选择你的分叉仓库和你分叉仓库里更新代码的分支（branch）。
在选择完成后，点击 `Create pull request` 按钮提交你的 PR。

这一子任务不需要你提交有意义的代码，你只需要正确地创建分叉，随意提交一些改动，然后正确提交一个 PR 即可。

### 2、创建一个新的游戏单位类型 【10 pts】

本游戏的框架涉及 4 种类型的元素：单位（Units）、障碍物（Obstacles）、子弹（Bullets）和粒子（Particles）。
这些元素共同组成了游戏内容。每种类型的元素都有一个基类的定义，所有相应类型的设计实现都应通过继承对应类型元素的基类的方式实现。
不同类型的元素也有一些符合各自定位的虚函数声明，你在实现的过程中需要给出相应的定义。
更多框架相关信息的说明请前往 `src/battle_game/core/` 目录下的 [README.md](src/battle_game/core/README.md) 文件查阅。

在几种类型的元素中，单位是玩家主要操控的对象，即玩家在游戏内可以扮演的角色。
这个子任务要求你在项目中创建一个由你进行维护的游戏单位类型，你可以自由地设计你的游戏单位的功能和特性，但你至少需要完成最基础的功能。
在本次作业发布时，游戏框架已经给出了一个游戏单位的实现范例，即 `src/battle_game/core/units/` 目录下的 `tiny_tank.h,cpp`。
这个范例实现的是一个坦克单位，可以用键盘进行移动，用鼠标进行瞄准和射击。
作为最基础的要求，你需要仿制这个坦克单位，并复现其功能。
如果你希望实现一些别样的游戏单位，你可以自行创造，但你的单位至少需要包含：
正确的外观、合理的移动逻辑以及至少一种射击飞射物（Bullet）的功能。

这是你需要做的具体步骤：
1. 在 `src/battle_game/core/units/` 目录下仿照 `tiny_tank.h` 和 `tiny_tank.cpp` 的模式新建一对用于编写你的游戏单位的 `.h` 和 `.cpp` 文件。
你可以自行选取合适的名字。为了避免和他人的命名产生冲突，你可以在文件名中添加带有个人特征的标记，如：常用网名、学号等。
2. 重新进行 CMake 配置 (CMake Configuration，即常见情况下调用 `cmake ..` 生成 build 目录下项目结构的命令)，使用 IDE 的同学应该可以找到重新配置相关的按钮，CMake 会自动将你新建的文件引用到项目中。
3. 在你创建的代码文件里，你需要定义一个新的类型，使其继承自 `Unit` 类型。这个类型名可以任意选取。
同样的，你可以添加带有个人特征的标记以避免与其他同学冲突。
4. 实现功能：如果你希望快速获得这部分分数，你可以参考 `tiny_tank` 的实现完成一个你的坦克的功能。
如果你希望设计创造性的单位，你可以参考 `tiny_tank` 的逻辑设计，编写你自己的单位逻辑。
5. 在实现完成你的单位类型后，给你的作品签上自己的名字吧！你需要重载 `UnitName` 和 `Author` 两个函数，
前者是你创造的单位的名称，后者是作者的名称，也就是你的名字，你可以随意地用真实姓名或者昵称。
6. 最后你需要前往 `src/battle_game/core/selectable_units.cpp` 将你的单位添加到可选单位列表。


一切做完后，编译并运行程序，你会看到你的单位已经出现在左上角的可选单位列表中了。你可以从列表中选择你的单位，
用 `自毁` 按钮消灭当前默认创建的单位，等待 5 秒后重生出的新单位就是你的作品！

如果你的单位运行起来一切正常，你可以将你的代码推送到你的分叉仓库中，你之前创建的 PR 会自动同步你更新的内容。

7. 我们需要你将你的运行结果截图提交到 PR 的备注中，截图应当包含画面左上角你的单位的名称和你使用的作者名。我们需要在验收时看到你的截图。

### 3、提出一个新功能的想法到 Issues 列表 【5 pts】

有时你有一个很好的想法，但是没有办法立刻实现，
或者你发现项目中存在一个 Bug，希望以后去修复。
这时你可以利用 GitHub 的 Issues 功能先把问题记下来。

项目的构建需要大家发挥自己的想象力和创造力，
你既是乙方，也是甲方。
这个子任务要求你在 GitHub Issues 栏中提交一个有效的 Issue。
你需要在 Issue 中尽可能详细的说明问题的需求，最好同时给出一个可行的实现思路。
如果前面已经有同学提过类似或者相同的问题，那就不要再重复提交了。
我们不在意你提的问题是复杂还是简单，只要是一个有效的问题，你都可以直接拿到这个子任务的 5 分！

### 4、自由创造 【5 pts】

在同学们提出很多好的 idea 后，我们希望能够把他们一一变为现实。
你可以从 Issues 列表中选择一个你认为自己可以解决的部分，然后提交一个新的 PR 实现这个功能。
在实现完成后，你同样需要将你的运行结果截图提交到 PR 的备注中。同时，请在备注中加入 Close #IssueNumber 的方式关联你的 PR 和 Issue。
Good Luck and Have Fun！

## 验收

在 GitHub 上完成以上所有任务后，请在网络学堂提交一个文本文件，包含你提交的所有 PR 的链接以及你提交的 Issue 的链接。

PR 和 Issue 的范例参考：

[https://github.com/Yao-class-cpp-studio/battle_game_2024/pull/1](https://github.com/Yao-class-cpp-studio/battle_game_2024/pull/1)

[https://github.com/Yao-class-cpp-studio/battle_game_2024/issues/2](https://github.com/Yao-class-cpp-studio/battle_game_2024/issues/2)
