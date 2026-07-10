## 新增 Markdown 后的操作流程

### 1 创建新文件
文件保存在docs/class.md

---

### 2 修改导航

在 `nav` 中加入新文件：

```yaml
nav:
  - 基础语法: index.md
  - 类与对象: class.md
```

---

### 3 本地预览

```bash
mkdocs serve
```

浏览器打开：

```text
http://127.0.0.1:8000/
```

---

### 4 检查构建

```bash
mkdocs build --strict
```

没有报错即可继续。

---

### 5 上传源码并更新网页

```bash
git add .
git commit -m "Add class notes"
git push

mkdocs gh-deploy --force
```

---

### 6 以后每次更新的固定流程

```bash
cd ~/cpp-notes
nano mkdocs.yaml  #在nav部分添加

mkdocs build --strict

git add .
git commit -m "Update C++ notes"
git push

mkdocs gh-deploy --force
```

新增文件时，记得同时修改 `mkdocs.yml` 中的 `nav`。