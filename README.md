# 🩹 使用 patch 应用补丁（简易版）

## 📍 步骤

1. 进入 Python 库目录（示例路径）：
   ```bash
   cd /xx/miniconda/envs/xx/lib/python3.x/site-packages/
````

2. 应用补丁：

   ```bash
   patch -p1 < fix_xxx.patch
   ```

---

## 💡 说明

* `patch`：用来修改源码文件。
* `-p1`：忽略补丁路径的第一级目录（一般保持这个即可）。
* `< fix_xxx.patch`：指定补丁文件。

---

## 🧰 如果未安装 patch

在 Debian / Ubuntu 系统中安装：

```bash
sudo apt install patch -y
```

# 🩹 将 Windows 生成的 patch 文件转为 Linux 可用格式

Windows 下生成的 `.patch` 文件通常使用 **CRLF（回车+换行）** 换行符，  
在 Linux 中应用时可能会报错，如：
```

patch unexpectedly ends in middle of line

```
或
```

patch: **** malformed patch at line xx

````

---

## ✅ 解决方法

1. 安装转换工具：
   ```bash
   sudo apt install dos2unix -y
````

2. 将补丁文件从 Windows 格式转换为 Linux 格式：

   ```bash
   dos2unix fix.patch
   ```

3. 然后正常应用补丁：

   ```bash
   patch -p1 < fix.patch
   ```

---

## 📘 示例

```bash
cd /xx/miniconda/envs/xx/lib/python3.x/site-packages/
sudo apt install dos2unix patch -y
dos2unix fix.patch
patch -p1 < fix.patch
```

---

## 💡 说明

* `dos2unix`：将 Windows 格式（CRLF）转换为 Unix 格式（LF）。
* `patch -p1`：应用补丁。
* `< fix.patch`：指定补丁文件输入。

执行成功后将输出：

```
patching file vllm/entrypoints/openai/api_server.py
```

表示补丁应用完成。
