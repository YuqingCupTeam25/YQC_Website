## Debug_Record 1

<h6>git version: 2.46.0.windows.1</h6>

这段说明是关于解决在使用 Git 克隆大型代码库时遇到的特定问题：

#### 1.关闭压缩

```bash
git config --global core.compression 0
```

- **作用**：关闭 Git 的数据压缩功能。
- **原因**：在某些情况下，压缩可能导致性能问题，尤其是在网络连接不稳定时。关闭压缩可以减少网络数据处理中的复杂性，从而可能避免与 SSL 连接相关的错误。

#### 2. 进行部分克隆

```bash
git clone --depth 1 <repo_URI>
```

- **作用**：执行部分克隆，限制克隆的提交深度为 1。
- **解释**：`--depth 1` 表示只克隆最新的提交，而不是整个历史记录。这可以显著减少需要下载的数据量，适合网络不稳定或带宽有限的情况。

#### 3. 获取完整的克隆

进入新克隆的目录后，你可以运行：

```bash
git fetch --unshallow
```

或使用以下命令：

```bash
git fetch --depth=A_LARGE_NUMBER
```

- **作用**：这两个命令的目的是将之前部分克隆的内容扩展为完整克隆。
- **解释**：
  - `git fetch --unshallow`：将浅克隆转换为完整克隆，下载所有缺失的提交。
  - `git fetch --depth=A_LARGE_NUMBER`：将深度设置为一个非常大的值，实际上是想要获取所有的提交。

#### 4. （option）常规拉取

```bash
git pull --all
```

- **作用**：执行常规的拉取操作，更新本地仓库与远程仓库的状态。
- **解释**：这一步是为了确保本地仓库与远程仓库完全同步，包括所有分支的更新。