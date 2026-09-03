# Magpie 用户手册

适用版本：1.0 · iPhone、iPad 与 Mac · iOS / iPadOS 26.0 及以上

[English](manual.md)

Magpie 是运行于 iPhone、iPad 和 Mac 的分子可视化与几何处理程序，可读取分子坐标和计算输出，编辑结构、进行本地力场优化，并生成量子化学程序包输入文件及坐标文件。通过 SSH 连接，可以访问远程计算目录并调用 Multiwfn 分析波函数。

## 目录

1. [基本使用与入门](#1-基本使用与入门)
2. [文件与文件夹](#2-文件与文件夹)
3. [连接服务器](#3-连接服务器)
4. [查看与测量结构](#4-查看与测量结构)
5. [搭建与编辑分子](#5-搭建与编辑分子)
6. [力场优化](#6-力场优化)
7. [生成输入文件与坐标文件](#7-生成输入文件与坐标文件)
8. [查看计算结果](#8-查看计算结果)
9. [播放轨迹](#9-播放轨迹)
10. [CUBE 表面可视化](#10-cube-表面可视化)
11. [分子轨道与快速 ESP](#11-分子轨道与快速-esp)
12. [终端与交互式 Multiwfn](#12-终端与交互式-multiwfn)
13. [设置](#13-设置)
14. [常见问题](#14-常见问题)

## 1. 基本使用与入门

### 1.1. 工作环境

Local 是 Magpie 的设备本地文件区。结构查看、编辑、力场优化、输入生成、CUBE 渲染和计算结果分析均在本地完成。连接 SSH 主机后可使用远程文件浏览器和 Terminal；Molecular Orbitals、Quick ESP 及交互式 Multiwfn 调用服务器上的 Multiwfn。

工作区由文件浏览器、文档区域和 Results 抽屉组成，分子轨道列表和终端面板在文档旁展开。本手册中的控件名称与 App 界面一致。

Magpie 显示的原子编号从 1 开始；几何控件中的距离使用 Å，角度使用度。Generate 按所选程序的输入语法转换编号和单位。

### 1.2. 打开一个结构

1. 在服务器选择页进入 **Local**。
2. 点击文件浏览器中的导入按钮，从“文件”App 选择 XYZ、MOL2、CIF 或 PDB 文件。
3. 点击导入的文件，打开分子结构。
4. 单指拖动旋转视角，双指捏合缩放，双指拖动平移视图。
5. 点击尺子按钮测量距离和角度，点击铅笔按钮编辑结构。

### 1.3. 新建一个分子

1. 进入 Local，选择 **New 3D Model**。
2. 使用 **Add atom** 或 **Add group** 放置原子和片段。
3. 连接原子，调整结构。
4. 点击编辑工具栏中的播放按钮，进行力场优化。
5. 打开 **Generate**，选择 **XYZ** 或 **MOL2**，填写文件名并点击 **Save**。

只需要坐标时选择 XYZ；需要保留化学键信息时选择 MOL2。

### 1.4. 查看一次计算

导入并打开支持的计算输出文件。在 **Results** 中切换结构轨迹、计算详情、收敛图、振动和分析面板。对于 ORCA 的 IRC 和扫描计算，将配套坐标及轨迹文件与主输出放在同一目录。

### 1.5. 示例：创建第一个坐标文件

选择 New Text File，输入以下 XYZ 记录：

```text
3
Water
O   0.000000   0.000000   0.000000
H   0.758602   0.000000   0.504284
H  -0.758602   0.000000   0.504284
```

另存为 `water.xyz`，从文件列表打开。第一行为原子数，第二行为注释，后续各行分别给出元素及以 Å 为单位的笛卡尔坐标。用这个文件即可熟悉测量、编辑和 Generate，无需连接服务器。

## 2. 文件与文件夹

### 2.1. 文件格式

| 类型 | 格式 | 用途 |
| --- | --- | --- |
| 分子坐标 | `.xyz`、`.mol2`、`.cif`、`.pdb` | 查看、测量、编辑结构并生成新文件 |
| 计算输入 | 支持的量子化学程序包输入文件格式，包括 `.inp`、`.gjf`、`.com` | 打开几何结构；使用 Open as Text 编辑输入文本 |
| 计算输出 | 支持的量子化学程序包文本输出，常见扩展名为 `.out`、`.log` | 查看结构、能量、优化、振动、IRC、扫描及电子激发结果 |
| 体积数据 | `.cub`、`.cube` | 分子轨道、WFN Analysis、Interaction 和 ESP 表面 |
| 轨迹 | 多帧 `.xyz`；配合参考 XYZ 使用的 `.dcd` | 播放连续结构 |
| 远程波函数 | `.molden`、`.mwfn`、`.gms`、`.wfn`、`.wfx`、`.fchk`、`.fch`、`.chk`、`.gbw` | 通过服务器上的 Multiwfn 打开 |
| 文本 | `.txt`、`.text`、`.md`、`.csv`、`.tsv` | 阅读与编辑文本 |
| 图片 | PNG、JPEG、HEIC / HEIF、GIF、BMP、TIFF | 预览、缩放和平移 |

### 2.2. 浏览与整理

点击文件夹进入，点击列表顶部的 **../** 返回上级目录。路径栏用于跳转目录，筛选栏用于缩小当前文件列表。远程计算生成新文件后，点击 **Refresh** 刷新。

长按文件，或使用鼠标右键，打开文件菜单：

- **Open as Text**：按原始文本打开输入、输出或其他文本文件。
- **Copy**：在当前目录创建副本。
- **Rename**：重命名。
- **Delete**：确认后删除所选项目。
- **Export File**：通过系统文件界面导出副本。
- **Download to Local**：将远程文件复制到 Magpie 的本地工作区。

使用 **New Folder** 新建文件夹。将文件拖到文件夹上即可移入，拖到 **../** 上即可移到上级目录。在 **Settings → File Browser → Show Hidden Files** 中开启隐藏文件显示，可查看名称以点开头的文件和文件夹。

### 2.3. 从“文件”或其他 App 导入

导入按钮将文件复制到 Magpie 当前打开的目录。在 Local 中，文件保存在设备上；在 Remote 中，文件上传到当前服务器目录。遇到同名文件时保留原文件，并为导入副本使用新的名称。

也可以在其他 App 中分享兼容文件，选择 Magpie 打开。系统分享的文件进入 Local：如果原先连接着 SSH，Magpie 会断开连接，导入到 Local 根目录；如果已经处于 Local，则导入当前文件夹。DCD 文件导入后，再从参考 XYZ 附加。波函数文件使用 Magpie 内的导入按钮导入。

### 2.4. 编辑文本

选择 **New Text File** 新建文本，或对已有文件使用 **Open as Text**。编辑后点击文档顶部的勾选 **Save** 按钮保存；**Save As** 在当前目录另存一份。保存的文本使用 Unix 换行符，适合计算输入文件和 shell 脚本。

## 3. 连接服务器

### 3.1. 添加 SSH 主机

1. 返回服务器选择页，添加主机。
2. 填写 **Name**、**Host**、**Port** 和 **Username**。SSH 默认端口为 22。
3. 选择认证方式，填写凭据或导入密钥。
4. 点击 **Save**，然后选择主机卡片连接。
5. 按提示确认主机密钥并完成认证。连接后进入账户的主目录。

| 认证方式 | 填写内容 |
| --- | --- |
| Password | 账户密码 |
| Password + Passcode | 密码，可选填当前验证码；其余认证提示会在连接时出现 |
| Private Key | 导入 OpenSSH 私钥文件 |

编辑已有主机时，密码留空会保留已保存的密码；未导入新私钥时沿用原私钥。长按主机卡片可编辑设置。

如果服务器要求先确认手机推送、再按 Enter，请先在手机上确认，然后将响应输入框留空，点击 **Continue**。

文件浏览器中的返回服务器列表按钮会断开当前连接。本地文件可继续从 Local 卡片进入。

### 3.2. 准备 Multiwfn

在服务器上安装 Multiwfn，并将它加入对应 shell 的运行环境。两种二进制波函数格式需要在 Multiwfn 设置中声明相关转换程序路径：

| 波函数文件 | 需声明路径的转换程序 |
| --- | --- |
| `.chk` | `formchk` |
| ORCA `.gbw` | `orca_2mkl` |

其余已列出的波函数格式直接交给 Multiwfn 读取。源文件应放在可写的计算目录中，Magpie 会在该目录下创建临时分析文件。

### 3.3. Multiwfn 预热命令

打开主机编辑页，展开 **Advanced**，在 **Multiwfn Prewarm Command** 中填写运行 Multiwfn 前所需的环境设置或前台资源申请命令。

使用单行 shell 命令加载环境，或进入计算资源分配后的 shell。队列和资源参数按所在集群填写。命令应自行完成设置，不再等待额外输入，并保持在前台会话中运行。

交互式 Multiwfn、Molecular Orbitals 和 Quick ESP 共用这套环境，普通 Terminal 使用独立会话。结束一次 Multiwfn 分析后，环境会保留供下次使用；断开服务器连接时结束。如果集群资源分配已到期，重新连接以准备新的环境。

例如，Multiwfn 可执行文件位于 `/opt/Multiwfn` 时，可使用以下预热命令将该目录加入分析环境：

```sh
export PATH=/opt/Multiwfn:$PATH
```

目录替换为服务器上的安装路径。需要在分配的计算节点运行 Multiwfn 时，在同一字段填写集群资源申请命令，队列、时限和资源参数沿用集群配置。

## 4. 查看与测量结构

### 4.1. 视图操作

| 操作 | 手势或按钮 |
| --- | --- |
| 旋转视角 | 单指拖动 |
| 缩放 | 双指捏合 |
| 平移视图 | 双指拖动；鼠标或触控板滚动也可平移 |
| 设置旋转中心 | 在非编辑、非测量模式下轻点原子 |
| 重新适配结构 | **Reset view**，圆形箭头按钮 |
| 连续旋转 | 自动旋转按钮 |
| 测量 | 尺子按钮 |
| 编辑结构 | 铅笔按钮 |
| 红蓝立体显示 | 眼镜按钮 |

在非编辑、非测量模式下，轻点一个原子，后续视角旋转便以该原子为中心，该原子会高亮显示。轻点其他原子可切换旋转中心；点击 **Reset view** 恢复以整体结构中心旋转，并重置视图。

眼镜按钮开启红蓝立体显示，配合红蓝 3D 眼镜使用。通过红、蓝强度滑块调整两幅图像的亮度。

文档顶部的侧栏和 Results 按钮可收起对应面板，为结构腾出空间。iPad 可拖动面板分隔条调整大小；iPhone 的分子工作区使用横屏，Terminal 和 Multiwfn 使用竖屏。

### 4.2. 测量

开启尺子工具后，按顺序点击原子：

- 两个原子：距离，单位 Å。
- 三个原子 A–B–C：以 B 为顶点的键角。
- 四个原子 A–B–C–D：绕 B–C 的二面角。

再次点击已选原子可将其移出测量选择；双击空白处清空选择。测量不会改变原子坐标。

### 4.3. 化学键显示

MOL2 文件保留原有的显式键信息。对于只有坐标的结构，Magpie 根据几何与局部化学环境识别连接和键级。芳香键、酰胺键与共振键采用相同的部分双键外观，但各自的化学含义会保留。

## 5. 搭建与编辑分子

点击铅笔进入 **Geometry Editor**，或从 **New 3D Model** 开始。编辑以当前显示的帧为起点，因此可以从轨迹中选取一帧，作为新计算的初始结构。

### 5.1. 选择与移动

选择 **Select atoms**。逐个点击原子形成有序选择，拖出矩形进行框选，双击可全选原子。

- **R**：旋转所选原子。
- **T**：平移所选原子。
- 选择 R 或 T 后，在画布中拖动进行变换。
- 再次点击当前变换按钮，或按 Esc，退出该变换模式。

这些操作会改变所选原子的坐标；普通视角旋转只改变观察方向。再次点击当前编辑工具可回到查看模式。

### 5.2. 添加或替换原子

1. 选择 **Add atom**。
2. 点击元素符号打开周期表，选择元素。
3. 在 **Bond Order** 中选择 Single、Double、Triple 或 Partial Double。
4. 点击空白处添加独立原子；从已有原子向外拖动，添加与其相连的新原子。

Add atom 模式下，点击已有原子会替换其元素。从一个已有原子拖到另一个已有原子可以建键；如果两者已有键，重复拖动会按 Single → Double → Triple → Single 循环切换，Partial Double 则变为 Double。

### 5.3. 添加官能团与环

选择 **Add group**，在 **Group / Structure** 中选择片段。点击空白处独立放置，或从已有原子拖出并连接片段。点击末端原子可用所选片段替换它，例如用官能团取代一个氢原子。

以搭建苯酚为例：在新画布上放置 **Benzene**，将片段选项切换为 **Hydroxyl**，再点击苯环上的一个末端氢原子。羟基会替换该氢并与苯环连接。随后优化结构，通过 Generate 保存。

### 5.4. 修改或删除化学键

在 Select atoms 模式下选择两个原子，长按选择区域，使用菜单中的 **Add Bond**、**Delete Bond** 或键型选项。**Delete Atoms** 删除所选原子，也可用于较大的原子选择。

### 5.5. 调整键长、键角和二面角

逐个点击原子，保留选择顺序，不使用框选。对应的几何编辑按钮会出现在工具栏中。

| 选择顺序 | 控件 | 移动方式 |
| --- | --- | --- |
| A、B | Bond Length | A 一侧移动，B 保持固定 |
| A、B、C | Angle | A 绕 B 移动 |
| A、B、C、D | Dihedral | A 一侧绕 B–C 旋转 |

选择控件后拖动滑块。键长单位为 Å，角度单位为度。结构扩展到视野外时，点击 **Reset view** 重新适配。

### 5.6. 键盘快捷键

| 按键 | 操作 |
| --- | --- |
| R | 旋转所选原子 |
| T | 平移所选原子 |
| Esc | 退出当前变换 |
| Delete | 删除所选原子 |
| Command–Z | 撤销 |
| Shift–Command–Z | 重做 |

### 5.7. 保存编辑后的结构

在 Geometry Editor 中打开 **Generate**，将结构保存为输入文件或坐标文件。离开编辑器前先保存：**Stop editing** 返回原文档，不会将编辑坐标直接写回源文件。

## 6. 力场优化

### 6.1. 优化整个结构

1. 打开 **Settings → Geometry Editor → Force Field**，选择 **UFF** 或 **MMFF94s**，默认为 UFF。
2. 返回 Geometry Editor，准备好原子和化学键。
3. 点击编辑工具栏中的播放按钮 **Optimize geometry**。
4. 观察结构变化。优化过程中仍可旋转、平移和缩放视角。
5. 等待收敛，或点击暂停接受当前显示的结构。
6. 使用 **Generate** 保存。

一次优化对应一条撤销记录。需要修改原子或键时，先暂停优化。优化仍在运行时退出编辑器，会取消本轮优化。

两套力场均使用当前结构和键级。同一画布中未相连的多个分子会作为整体优化，并计入分子间相互作用。含过渡金属配位键的结构选择 UFF。

### 6.2. 固定部分原子

开启 **Settings → Geometry Editor → Freeze Selected Atoms**。选中需要保持不动的原子，再开始优化。每次点击播放时确定本轮固定原子，其余原子自由移动。关闭该设置后恢复全结构优化。

### 6.3. 默认形式电荷

Magpie 根据当前显示的元素、化学键、显式氢以及识别到的芳香或共振基团，为力场原子类型分配形式电荷。未与其他原子成键的孤立原子采用以下默认离子电荷：

| 孤立原子 | 默认形式电荷 |
| --- | --- |
| 碱金属，如 Li、Na、K | +1 |
| 碱土金属，如 Be、Mg、Ca | +2 |
| 氧族元素，如 O、S、Se | −2 |
| 卤素，如 F、Cl、Br、I | −1 |

例如，未成键的 Na 按 Na⁺ 处理，未成键的 Cl 按 Cl⁻ 处理。这些元素族默认值用于孤立原子；已成键的主族原子则根据局部成键环境判断。例如，形成四条单键的氮取 +1，只有一条单键的氧取 −1。氢原子在结构中显式存在时，才计入这里的价态判断。

过渡金属中心采用预设氧化态进行力场原子类型匹配，配位结构中的金属也使用这些默认值。前三个 d 区系列的默认值如下：

| 元素 | 默认氧化态 |
| --- | --- |
| Cu、Ag | +1 |
| Mn、Fe、Ni、Zn、Ru、Pd、Cd、Pt、Hg | +2 |
| Sc、Y、Cr、Co、Rh、Ir、Au | +3 |
| Ti、Zr、Hf | +4 |
| V、Nb、Ta、Tc | +5 |
| Mo、W、Os | +6 |
| Re | +7 |

这些形式电荷用于传给力场的分子拓扑。Generate 中的 **Charge** 和 **Mult** 设置量子化学输入的总电荷与多重度，不改变上述力场电荷分配。每轮优化都使用当前结构；补充氢原子或修改键级后，下一轮会按更新后的结构重新分配电荷。

## 7. 生成输入文件与坐标文件

**Generate** 使用编辑器当前的几何结构生成文件。打开时默认选择 ORCA，可在 **Format** 中选择支持的量子化学程序包输入文件格式，或 XYZ、MOL2、CIF、PDB 坐标文件。

### 7.1. 支持的量子化学程序包输入文件格式

1. 选择程序包和 **Job**。
2. 设置 **Functional** 与 **Basis**。方法菜单也包含非 DFT 方法，相关控件随方法变化。
3. 填写 **Charge**、**Mult**、**Mem GB** 和 **Cores**。
4. 设置任务专属参数、色散和溶剂模型。
5. 查看生成文本，填写文件名并点击 **Save**。

Mem GB 表示总内存。生成 ORCA 输入时，Magpie 按核心数换算为 `%maxcore`。**Additional keywords** 用于补充关键词，ORCA 对适用方法提供辅助基组选项。

| Job | 用途 |
| --- | --- |
| SPE | 单点能计算 |
| OPT | 几何优化 |
| FREQ | 频率计算 |
| OPT+FREQ | 几何优化后计算频率 |
| TS | 过渡态优化 |
| IRC | 内禀反应坐标 |
| Scan | 一维或二维柔性扫描 |
| TDDFT | 电子激发态 |
| AIMD | ORCA 分子动力学 |

IRC 可选择 Both、Forward 或 Backward，并设置路径参数。TDDFT 中通过 **Excited states** 设置请求的激发态数目。

在 Local 中保存到当前本地文件夹；连接 SSH 时保存到当前远程目录。Generate 负责准备文件，实际计算使用 Terminal 中的程序命令或集群作业提交命令运行。

### 7.2. 柔性扫描

以下以 ORCA 为例。

1. 选择 **Job → Scan**，在 **Dimensions** 中选择 **1D** 或 **2D**。
2. 选择坐标类型 Bond、Angle 或 Dihedral。
3. 按顺序填写原子编号。Magpie 的原子编号从 1 开始。
4. 设置起点、终点和点数。
5. 二维扫描还需独立设置 Coordinate 2。

编辑器中按顺序选取的 2–4 个原子可预填一维扫描的 Coordinate 1；任务仍需手动选择 Scan。键长扫描使用 Å，键角与二面角使用度。

例如，在 ORCA 中扫描 1、2 号原子间的距离，从 0.9 Å 到 1.3 Å，可填写：

| 字段 | 数值 |
| --- | --- |
| Dimensions | 1D |
| Coordinate type | Bond |
| 原子编号 | 1、2 |
| Start | 0.9 |
| End | 1.3 |
| Points | 9 |

该设置包含两个端点，共九个位置，间隔 0.05 Å。生成的输入块使用 ORCA 从零开始的编号：

```text
%geom
  Scan
    B 0 1 = 0.9, 1.3, 9
  end
end
```

二维扫描由两组坐标组成网格，例如第一维 9 个点、第二维 7 个点，对应 63 组坐标组合。

### 7.3. 手动修改生成文本

控件下方的文本可直接编辑。手动修改后，文本会保留，不再随后续参数变化自动重生成。点击 **Reset** 可按当前控件重新生成；切换 Format 会开始新的模板。

### 7.4. 导出坐标

- **XYZ**：保存元素符号与笛卡尔坐标。
- **MOL2**：保存原子与化学键信息，包括芳香键和酰胺键。
- **CIF**、**PDB**：生成相应格式的坐标文件。

这里导出的是当前结构，而非完整轨迹或计算输出。要保留原有多帧文件，使用文件浏览器中的 **Export File**。

ORCA 输入文件及各输入块的语法参见 [ORCA 6 输入参考](https://www.faccts.de/docs/orca/6.0/manual/contents/structure.html)。

### 7.5. ORCA 分子动力学

在 Generate 中选择 **ORCA → Job → AIMD**，设置电子结构方法和动力学参数。

| 控件 | 含义 | 默认值 |
| --- | --- | --- |
| Time step (fs) | 积分时间步长 | 1 fs |
| Steps | MD 总步数 | 1000 |
| Initial temp. (K) | 初始化速度所用的温度 | 298.15 K |
| Thermostat | CSVR、NHC、Berendsen 或 None | CSVR |
| Bath temp. (K) | 热浴目标温度 | 298.15 K |
| Time constant (fs) | 温控耦合时间 | 100 fs |
| Trajectory Format | XYZ 或 DCD | XYZ |
| Stride | 每隔多少步输出一帧 | 1 |

**Keep center of mass** 控制模拟运行期间的质心固定。

#### 7.5.1. 约束壁

在 **Cell wall** 中选择 None、Cube、Rectangular、Sphere 或 Ellipsoid。长度单位为 Å，壁弹簧常数单位为 kJ/mol/Å²。这些选项是非周期谐振约束壁。

选择约束壁后，**Center geometry at origin** 将结构的算术几何中心移到生成输入的原点，编辑器中的坐标保持不变。这是生成输入时的处理，与运行期间的 Keep center of mass 分开设置。

#### 7.5.2. 输出文件

以 `sample.inp` 为例：

- XYZ 模式输出 `sample_traj.xyz`。
- DCD 模式输出 `sample_traj.dcd`，并生成参考结构 `sample.xyz`。

计算结束后刷新远程目录。XYZ 轨迹可直接打开；DCD 则先打开 `sample.xyz`，再附加 `sample_traj.dcd`。

#### 7.5.3. 示例：输出 DCD 轨迹

在 Geometry Editor 中打开结构，选择 ORCA 和 AIMD，填写以下参数：

| 控件 | 数值 |
| --- | --- |
| File name | `sample.inp` |
| Time step (fs) | 0.5 |
| Steps | 2000 |
| Initial temp. (K) | 298.15 |
| Thermostat | CSVR |
| Bath temp. (K) | 298.15 |
| Time constant (fs) | 100 |
| Trajectory Format | DCD |
| Stride | 10 |
| Cell wall | None |
| Keep center of mass | 关闭 |

模拟时长为 1 ps，坐标输出间隔为 5 fs。Generate 在所选电子结构设置和坐标之外写入以下 MD 块：

```text
%md
  Timestep 0.5_fs
  Initvel 298.15_K
  Thermostat CSVR 298.15_K Timecon 100_fs
  Dump Position Format XYZ Stride 0 Filename "sample.xyz"
  Dump Position Format DCD Stride 10 Filename "sample_traj.dcd"
  Run 2000
end
```

计算结束后打开 `sample.xyz`，从 Results 加载 `sample_traj.dcd`。MD 命令的详细定义参见 [ORCA 6 分子动力学参考](https://www.faccts.de/docs/orca/6.0/manual/contents/detailed/moldyn.html)。

## 8. 查看计算结果

打开支持的计算输出文件，显示 **Results**。面板菜单按文件中记录的计算内容提供对应项目。

### 8.1. 详情与几何优化

**Details** 包含 **Info**、**Thermo** 和 **Convergence** 表格，可查看程序和任务信息、电荷与多重度、能量、热化学量以及收敛指标。

几何优化可通过轨迹控件逐步查看。收敛图显示各项指标随优化步数的变化，并标记当前步骤。

### 8.2. 振动

选择 **Vibrations**，从频率菜单选择模式，点击 **Play Vibration** 播放。左右箭头切换相邻模式，**Displacement Amplitude** 调整显示的振幅。频率单位为 cm⁻¹，输出中的虚频以负值显示。

### 8.3. IRC 与一维扫描

在 Results 中选择 **IRC** 或 **Scan**，查看能量曲线和关联轨迹。点击曲线上的点，画布切换到对应结构。相对能量单位为 kcal/mol。

ORCA 的配套文件应与主输出放在同一目录。Magpie 会读取可用的 IRC 路径、合并扫描坐标，以及编号 XYZ 或轨迹 XYZ 来组合结果。

### 8.4. 二维扫描

点击 Results 顶部的 **2D Scan**，打开势能面。

- **Surface**：完整网格的可旋转三维能量曲面。
- **Contour**：两个扫描坐标及能量等高线。
- **Top view** 和 **Reset view**：调整三维曲面的观察方向。
- 在等高线视图中选择计算点，可关联到对应分子结构。

坐标轴使用扫描坐标，相对能量单位为 kcal/mol。不完整网格使用等高线视图，缺失计算点的位置保留空缺。

### 8.5. UV–Vis 与轨道跃迁

对于 TDDFT 或其他可识别的激发态输出，**UV-Vis Spectrum** 显示以波长为横轴的吸收光谱，波长单位为 nm。图中标出的 FWHM（半峰全宽）表示光谱展宽所用的峰宽。

**Orbital Transitions** 列出激发态、跃迁轨道对、自旋标记和贡献百分比。它用于阅读输出中的跃迁组成；从波函数生成空间轨道则使用 Molecular Orbitals 侧栏。

## 9. 播放轨迹

### 9.1. 多帧 XYZ

打开 XYZ 文件，选择 **Trajectory**。点击 Play 播放，拖动 Frame 滑块选择结构，通过 **Speed** 调整每秒播放帧数。开启 **Settings → Molecule Viewer → Loop Trajectory Playback** 可循环播放。

### 9.2. DCD 与参考 XYZ

1. 将 DCD 和参考 XYZ 放在同一个 Local 或 Remote 文件夹。
2. 打开单帧 XYZ。
3. 在 Results 中点击 Details 旁的 **Load trajectory (.dcd)**。
4. 选择配套 DCD。
5. 使用 Trajectory 控件播放或逐帧查看。

XYZ 提供元素和原子顺序，DCD 提供各帧坐标。使用生成轨迹时配套写出的 XYZ，使两者的原子数和顺序一致。Magpie 读取标准 ORCA 风格的 DCD 坐标轨迹；固定原子压缩和四维变体需先转换。

需要复用某一帧时，暂停到该帧，进入 Geometry Editor，再使用 Generate。

## 10. CUBE 表面可视化

打开 `.cub` 或 `.cube` 文件，在 **CUBE Visualization** 中选择模式。

| 模式 | 第一份 CUBE | 第二份 CUBE | 显示内容 |
| --- | --- | --- | --- |
| Molecular Orbital | 轨道数值 | — | 正负轨道等值面 |
| WFN Analysis | 福井函数、自旋密度等带正负值的标量场 | — | 正值绿色、负值蓝色表面 |
| Interaction | 用于定义等值面的场 | 用于着色的场 | 蓝—绿—红着色表面 |
| ESP | 电子密度 | 静电势 | 将静电势映射到电子密度表面 |

### 10.1. 单场表面

打开 CUBE，选择 Molecular Orbital 或 WFN Analysis，再在 Results 中调整 Surface 控件。WFN Analysis 显示 CUBE 已包含的数据，所需物理量先由分析程序生成。

### 10.2. 着色表面

1. 打开用于定义表面形状的 CUBE。
2. 选择 Interaction 或 ESP。
3. Magpie 提示选择 coloring CUBE 时，在文件列表中点击第二份文件。
4. 配对完成后调整等值面和外观。

ESP 先选电子密度 CUBE，再选静电势 CUBE。Interaction 使用同一次分析生成的表面场和着色场。两份数据应处于同一分子坐标系。

### 10.3. 表面控件

- **Iso Value**：选择绘制等值面的数值。
- **Render Quality**：调整表面采样质量。
- **Surface Opacity**：调整表面透明度。
- **Settings → Molecule Viewer → Surface Material**：选择 Constant 或 Lambert 材质。

调整大型表面时可先降低 Render Quality，确定视角和等值面后再提高质量。

### 10.4. ESP 色标

色标从最小值的蓝色，经中点的白色，过渡到最大值的红色，单位为原子单位。点击端点数值修改范围：iPad 在原位置输入，iPhone 使用独立输入框。

**Auto** 根据当前电子密度等值面上实际采样的静电势调整范围。修改 Iso Value 后，再次点击 Auto 可适配新表面。比较多个结构时，为它们填写相同的最小值和最大值。白色对应所选范围的中点；只有对称范围的中点才是零。

例如，最小值 −0.030、最大值 +0.030 a.u. 时，白色对应零；最小值 −0.020、最大值 +0.040 a.u. 时，白色对应 +0.010 a.u.。超出上下限的数值使用相应端点颜色。

### 10.5. 保存 CUBE 到 Local

远程单文件表面使用 **Save**，配对表面使用 **Save Both**。选择已有 Local 文件夹，或新建文件夹保存。重新打开 Interaction 或 ESP 配对表面需要两份 CUBE。

## 11. 分子轨道与快速 ESP

这两项功能从远程波函数文件出发，调用服务器已准备好的 Multiwfn 环境。

### 11.1. 分子轨道

1. 连接服务器，打开波函数文件。
2. 点击工作区顶部的 **Molecular Orbitals** 按钮。
3. 在列表中查看轨道能量、占据数和 HOMO / LUMO 标记。非限制性波函数分为 α、β 两列。
4. 点击轨道，生成并显示其等值面。
5. 在 Results 中调整 Iso Value、Render Quality 和 Surface Opacity。

前线轨道附近的数据会预先准备。双击较远的轨道，还可补齐它与附近已缓存区域之间同一自旋的未缓存轨道。在 **Settings → Analysis → Orbital Energy Unit** 中可切换 a.u. 和 eV。

### 11.2. 快速 ESP

1. 打开远程波函数文件。
2. 点击 Molecular Orbitals 旁的 **Quick ESP** 按钮。
3. Multiwfn 生成电子密度和静电势，Magpie 显示着色表面，并自动适配初始色标。
4. 调整等值面，或填写用于多结构比较的统一色标范围。
5. 选择 **Save Both** 将两份 CUBE 保存到 Local；选择 **Skip** 则继续查看而不保存。

分子轨道和快速 ESP 使用临时分析文件。将 CUBE 结果保存到 Local 后，可在没有服务器连接时重新查看这些表面。

## 12. 终端与交互式 Multiwfn

### 12.1. Terminal

连接 SSH 后，从工作区顶部打开 **Terminal**。终端从当前远程目录启动，可运行命令、提交计算和查看服务器输出。使用完毕点击面板的 × 关闭，再刷新文件列表查看新文件。

### 12.2. 交互式 Multiwfn

选择远程分析文件，从顶部打开 **Multiwfn**。面板显示程序的终端输出，并为识别到的菜单选项提供快捷按钮。

点击编号选项，或直接在终端输入响应，按 Multiwfn 菜单继续操作。重启按钮针对所选文件重新启动分析。使用程序的退出命令或关闭面板结束本次分析，已准备的环境保留到服务器断开。

Molecular Orbitals、Quick ESP 和交互式 Multiwfn 共用运行环境，结束或关闭当前分析后再启动另一项。普通 Terminal 使用独立会话。

## 13. 设置

| 分区 | 设置 | 用途 |
| --- | --- | --- |
| Molecule Viewer | Viewer Background | 画布背景颜色 |
| Molecule Viewer | Lighting Intensity | 主光强度 |
| Molecule Viewer | Fill Light | 阴影区域的补光 |
| Molecule Viewer | Surface Material | Constant (Default) 为平坦着色，Lambert 为漫反射光照 |
| Molecule Viewer | Loop Trajectory Playback | 轨迹循环播放 |
| Geometry Editor | Force Field | 选择 UFF 或 MMFF94s |
| Geometry Editor | Freeze Selected Atoms | 在下一轮优化中固定所选原子 |
| File Browser | Show Hidden Files | 显示名称以点开头的文件和文件夹 |
| Analysis | Orbital Energy Unit | 选择 a.u. 或 eV |

About 显示 App 版本；Credits 和 Open Source Software 列出使用的科学软件、库及其许可信息。

## 14. 常见问题

### 14.1. 生成的文件保存在哪里？

Generate 保存到文件浏览器当前目录。本地操作到 Local 中查找，远程操作刷新服务器目录。CUBE 的 Save / Save Both 使用保存时选定的 Local 文件夹。

### 14.2. 怎样保留编辑后的结构？

停止编辑前使用 Generate。保留键级选择 MOL2，只保存坐标选择 XYZ。如果需要修改原始输入文本，而非生成新的几何文件，使用 Open as Text。

### 14.3. 为什么没有 DCD 按钮？

先打开单帧参考 XYZ，再显示 Results，DCD 附加按钮会出现在该结构的底栏。将 DCD 放在同一目录。

### 14.4. 为什么没有振动、光谱或完整扫描点？

打开包含这些结果的主计算输出。坐标文件只提供结构，不包含频率或激发态数据。ORCA IRC 和扫描还应将配套文件放在同一目录，刷新后重新打开输出。

### 14.5. 波函数为什么打不开？

从 Remote 打开，并确认预热环境中能够运行 Multiwfn。在 Multiwfn 设置中检查转换程序路径：`.chk` 对应 `formchk`，`.gbw` 对应 `orca_2mkl`。同时确认源文件所在目录可写。集群分配到期后，重新连接以准备新的环境。

### 14.6. 力场优化报错后应调整什么？

查看画布上的元素、键和氢原子，修正错误连接或键级后重试。过渡金属配位结构使用 UFF。MMFF94s 可处理已识别的芳香和共振结构；孤立的通用 Partial Double 键应先明确其化学键型。

### 14.7. 表面为空，或颜色不合预期？

表面为空时降低 Iso Value。配对表面检查两份 CUBE 的选择顺序。ESP 可点击 Auto 适配当前表面，或恢复比较时使用的统一数值范围。

### 14.8. 文件太大，无法导入？

单文件导入上限为 512 MiB。CUBE 每个文件支持一个标量数据集，最多 2000 万个网格点。可重新生成较粗网格的 CUBE，或导出较短轨迹供设备查看。

### 14.9. 反馈问题

通过仓库的 [Issues 页面](https://github.com/RowenaZireael/Magpie-privacy/issues) 反馈，附上 Magpie 版本、设备与系统版本、文件类型、复现步骤和错误信息。提供小型示例文件或截图有助于复现。
