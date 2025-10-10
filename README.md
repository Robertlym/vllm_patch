# 🧩 使用 `patch` 应用补丁说明

本文档介绍如何在 **Linux** 和 **Windows（WSL 或 Git Bash）** 环境中使用 `patch` 命令应用补丁文件 `fix.patch`。

---

## 📦 一、安装必要工具

### 🐧 Linux / Ubuntu 系统

在终端执行以下命令：

```bash
sudo apt update
sudo apt install dos2unix patch -y
````

**说明：**

* `dos2unix`：用于将 Windows 格式的文本文件（CRLF）转换为 Unix 格式（LF），防止补丁文件格式不兼容。
* `patch`：用于应用 `.patch` 或 `.diff` 文件中的修改。

---

### 🪟 Windows（通过 WSL 或 Git Bash）

#### 1️⃣ 如果使用 WSL（Ubuntu 环境）：

直接在 WSL 终端中执行与上面相同的命令：

```bash
sudo apt install patch -y
```

#### 2️⃣ 如果使用 Git Bash：

Git Bash 自带 `patch` 工具，无需额外安装。

---

## 🔧 二、应用补丁文件

假设当前目录下有补丁文件 `fix.patch`，要将其应用到项目中。

### 步骤 1：确保补丁文件是 Unix 格式

如果补丁来自 Windows 环境，请先转换格式：

```bash
dos2unix fix.patch
```

### 步骤 2：应用补丁

进入项目的根目录后执行：

```bash
patch -p1 < fix.patch
```

**参数说明：**

| 参数            | 含义                                                  |
| ------------- | --------------------------------------------------- |
| `-p1`         | 忽略补丁文件路径中的第一级目录结构。根据补丁生成时的路径结构可能需调整为 `-p0`、`-p2` 等。 |
| `< fix.patch` | 指定输入的补丁文件。                                          |

---

## 🧠 三、常见问题与解决方法

| 问题                                                 | 原因               | 解决方法                                                      |
| -------------------------------------------------- | ---------------- | --------------------------------------------------------- |
| `patch: command not found`                         | 未安装 patch 工具     | 安装：`sudo apt install patch`                               |
| `Reversed (or previously applied) patch detected!` | 补丁已应用或方向错误       | 检查是否重复打补丁，或使用 `--reverse` 选项撤销：`patch -R -p1 < fix.patch` |
| `dos2unix: command not found`                      | 未安装 dos2unix 工具  | 安装：`sudo apt install dos2unix`                            |
| 文件编码问题                                             | 补丁文件为 Windows 格式 | 使用 `dos2unix fix.patch` 转换格式                              |

---

## 🧾 四、撤销补丁

若想撤销已应用的补丁，可以运行：

```bash
patch -R -p1 < fix.patch
```

---

## ✅ 示例

假设项目目录结构如下：

```
myproject/
├── src/
│   └── main.py
└── fix.patch
```

执行：

```bash
cd myproject
dos2unix fix.patch
patch -p1 < fix.patch
```

输出类似：

```
patching file src/main.py
```

即表示补丁应用成功。

---

## 📚 附录：生成补丁文件

如需自己创建补丁，可使用以下命令：

```bash
diff -ruN old_dir/ new_dir/ > fix.patch
```

**参数说明：**

* `-r`：递归比较目录。
* `-u`：以统一格式输出。
* `-N`：将缺失文件视为空文件。

---

**作者：** 技术维护团队
**文件名：** `patch_usage.md`
**更新时间：** 2025-10-10

```

