<h1>
通过Git得到项目代码量信息
</h1>

<code>
git log  --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }'
</code>

<h1>
  安装WSL
</h1>

  <p>
    使用 WSL 在 Windows 上安装 Linux
2022/08/17


本指南将介绍如何使用适用于 Linux 的 Windows 子系统安装 Linux 发行版（例如 Ubuntu、OpenSUSE、Kali、Debian、Arch Linux 等）。 通过 WSL，你可使用与 Windows 工具（如 PowerShell 或 Visual Studio Code）完全集成的 Linux 工具（如 Bash 或 Grep），而无需双启动。

先决条件
必须运行 Windows 10 版本 2004 及更高版本（内部版本 19041 及更高版本）或 Windows 11。

 备注

若要检查 Windows 版本及内部版本号，选择 Windows 徽标键 + R，然后键入“winver”，选择“确定” 。 可通过选择“开始”>“设置”>“Windows 更新”>“检查更新”来更新到最新的 Windows 版本。

如果你运行的是旧版，或只是不想使用 install 命令并希望获得分步指引，请参阅旧版 WSL 手动安装步骤。

安装 WSL 命令
现在，可以在管理员 PowerShell 或 Windows 命令提示符中输入此命令，然后重启计算机来安装运行适用于 Linux 的 Windows 子系统 (WSL) 所需的全部内容。

PowerShell

复制
wsl --install
此命令将启用运行 WSL 并安装 Linux 的 Ubuntu 发行版所需的功能。 （可以更改此默认发行版）。

首次启动新安装的 Linux 发行版时，将打开一个控制台窗口，要求你等待将文件解压缩并存储到计算机上。 未来的所有启动时间应不到一秒。

 备注

上述命令仅在完全未安装 WSL 时才有效，如果运行 wsl --install 并查看 WSL 帮助文本，请尝试运行 wsl --list --online 以查看可用发行版列表并运行 wsl --install -d <DistroName> 以安装发行版。 若要卸载 WSL，请参阅卸载旧版 WSL 或注销或卸载 Linux 发行版。

更改默认安装的 Linux 发行版
默认情况下，安装的 Linux 分发版为 Ubuntu。 可以使用 -d 标志进行更改。

若要更改安装的发行版，请输入：wsl --install -d <Distribution Name>。 将 <Distribution Name> 替换为要安装的发行版的名称。
若要查看可通过在线商店下载的可用 Linux 发行版列表，请输入：wsl --list --online 或 wsl -l -o。
若要在初始安装后安装其他 Linux 发行版，还可使用命令：wsl --install -d <Distribution Name>。
 提示

如果要通过 Linux/Bash 命令行（而不是通过 PowerShell 或命令提示符）安装其他发行版，必须在命令中使用 .exe：wsl.exe --install -d <Distribution Name> 或若要列出可用发行版，则使用：wsl.exe -l -o。

如果在安装过程中遇到问题，请查看疑难解答指南的安装部分。

要安装未列为可用版本的 Linux 发行版，可使用 TAR 文件导入任何 Linux 发行版。 在某些情况下，与 Arch Linux 一样，也可使用 .appx 文件进行安装。 还可以通过 WSL 创建自己的自定义 Linux 发行版，以供使用。

设置 Linux 用户信息
安装 WSL 后，需要为新安装的 Linux 发行版创建用户帐户和密码。 请参阅设置 WSL 开发环境的最佳做法指南来了解详细信息。

设置和最佳做法
建议遵循设置 WSL 开发环境的最佳做法这一指南，逐步了解以下操作：为已安装的 Linux 发行版设置用户名和密码、使用基本的 WSL 命令、安装和自定义 Windows 终端、针对 Git 版本控制进行设置、使用 VS Code 远程服务器进行代码编辑和调试、文件存储的最佳做法、设置数据库、装载外部驱动器、设置 GPU 加速等。

检查正在运行的 WSL 版本
可列出已安装的 Linux 发行版，并通过在 PowerShell 或 Windows 命令提示符中输入以下命令来检查每个发行版的 WSL 版本：wsl -l -v。

要在安装新的 Linux 发行版时将默认版本设置为 WSL 1 或 WSL 2，请使用命令 wsl --set-default-version <Version#>，将 <Version#> 替换为 1 或 2。

要设置与 wsl 命令一起使用的默认 Linux 发行版，请输入 wsl -s <DistributionName> 或 wsl --setdefault <DistributionName>，将 <DistributionName> 替换为要使用的 Linux 发行版的名称。 例如，从 PowerShell/CMD 输入 wsl -s Debian，将默认发行版设置为 Debian。 现在从 Powershell 运行 wsl npm init 将在 Debian 中运行 npm init 命令。

要在 PowerShell 或 Windows 命令提示符下运行特定的 WSL 发行版而不更改默认发行版，请使用命令 wsl -d <DistributionName>，将 <DistributionName> 替换为要使用的发行版的名称。

有关详细信息，请参阅 WSL 的基本命令指南。

将版本从 WSL 1 升级到 WSL 2
使用 wsl --install 命令安装的新 Linux 安装将默认设置为 WSL 2。

wsl --set-version 命令可用于从 WSL 2 降级到 WSL 1，或将以前安装的 Linux 发行版从 WSL 1 更新到 WSL 2。

要查看 Linux 发行版是设置为 WSL 1 还是 WSL 2，请使用命令 wsl -l -v。

要更改版本，请使用 wsl --set-version <distro name> 2 命令将 <distro name> 替换为要更新的 Linux 发行版的名称。 例如，wsl --set-version Ubuntu-20.04 2 会将 Ubuntu 20.04 发行版设置为使用 WSL 2。

如果在 wsl --install 命令可用之前手动安装了 WSL，则可能还需要启用 WSL 2 所使用的虚拟机可选组件并安装内核包（如果尚未这样做）。

如需了解更多信息，请参阅 WSL 命令参考以获取 WSL 命令列表，并参阅比较 WSL 1 和 WSL 2，获取有关用于你的工作场景的指南，或参阅设置 WSL 开发环境的最佳做法，了解有关使用 WSL 设置良好开发工作流的一般指南。

使用 WSL 运行多个 Linux 发行版的方法
WSL 支持运行想要安装的任意数量的不同 Linux 发行版。 这可能包括从 Microsoft Store 选择发行版、导入自定义发行版或生成自己的自定义发行版。

安装后，有几种方法可以运行 Linux 发行版：

安装 Windows 终端（推荐）：使用 Windows 终端支持你想要安装的任意数量的命令行，并允许你在多个标签或窗口窗格中打开它们并在多个 Linux 发行版或其他命令行（PowerShell、命令提示符、PowerShell、Azure CLI 等）之间快速切换。 可使用独特的配色方案、字体样式、大小、背景图像和自定义键盘快捷键来完全自定义终端。 了解详细信息。
通过访问 Windows“开始”菜单并键入已安装的发行版的名称，可以直接打开 Linux 发行版。 例如：“Ubuntu”。 这会在其自己的控制台窗口中打开 Ubuntu。
在 Windows 命令提示符或 PowerShell 中，可以输入已安装的发行版的名称。 例如：ubuntu
在 Windows 命令提示符或 PowerShell 中，可以在当前命令行中打开默认的 Linux 发行版，方法是输入：wsl.exe。
在 Windows 命令提示符或 PowerShell 中，可以在当前命令行中使用默认的 Linux 发行版，而无需输入新的发行版名称，方法是输入：wsl [command]。 将 [command] 替换为 WSL 命令，例如，替换为 wsl -l -v 以列出已安装的发行版，或 wsl pwd 以查看当前目录路径在 WSL 中的装载位置。 在 PowerShell 中，命令 get-date 将提供 Windows 文件系统中的日期，而 wsl date 将提供 Linux 文件系统中的日期。
选择的方法应取决于所执行的操作。 如果已在 Windows 提示符或 PowerShell 窗口中打开 WSL 命令行并想退出，请输入命令：exit。
    </p>
