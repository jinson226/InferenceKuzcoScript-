# 能绕过限制多开，但需要一些技巧，请耐心看完。
# Inference（原 Kuzco）Epoch 2 最新一键自动重启 + 多开脚本（仅支持显卡用户）

**作者：J1N，KuzCommunityCN Founder**  
**推特：[ @J1N226 ](https://twitter.com/J1N226)**（关注推特私信拉交流群）

---

## 📌 项目简介

该脚本为 Inference Epoch 2 提供了 **一键部署、自动重启和多开** 的完整解决方案。  
基于 [Singosol 原项目](https://github.com/singosol/kuzco-docker) 进行 Fork，并根据官方 Epoch 2 的更新进行了适配与优化。

主要优化内容包括：
- 自动重启
- 支持单卡多开、多卡多开
- 脚本内含详细注释，方便根据不同设备灵活调整参数

---

## ✅ 环境要求

- **操作系统**：Linux  
- **显卡驱动**：NVIDIA 550  
- **显存要求**：显存大于 6GB（详见[官方文档](https://docs.inference.supply/hardware)）  
- **Python**：3.8 及以上版本
- **Docker**：最新版

---

## 🚀 脚本功能

- 🔁 **自动重启**：无需人工干预，持续稳定运行  
- 🧩 **多开支持**：单卡多开、多卡多开 
  - 例如：6GB 显存 = 单开，12GB 显存 = 双开，以此类推

---

## 🛠️ 使用方法

在终端输入以下指令运行脚本： 
- 单开
```bash
python3 kzco.py -c "--worker XXX --code XXX"
```
- 多开
```bash
python3 kzco.py -c "--worker1 XXX --code XXX"
python3 kzco.py -c "--worker2 XXX --code XXX"
python3 kzco.py -c "--worker3 XXX --code XXX"
python3 kzco.py -c "--worker4 XXX --code XXX"
```

> 参数 `"--worker XXX --code XXX"` 来自官方 Inference 平台创建 Worker 时选择 Docker 方式所自动生成的命令，多开需要生成多个worker。

---

## 📖 注意事项

- ✅ **支持单卡多开和多卡多开**
- 当你**创建一个 Worker 并运行一次脚本时**，你机器上的**每张显卡将会单开**
- 如果你**再创建一个新的 Worker 并再次运行脚本**，每张显卡将会**双开**
- 通过重复创建 Worker 和运行脚本，可以逐步实现每张卡的多开

### 📊 举例说明：

| 显卡显存 | 每张卡最大进程数 | 所需 Worker 数 |
|----------|------------------|----------------|
| 12GB     | 2                | 2              |
| 18GB     | 3                | 3              |
| 24GB     | 4                | 4              |

> 💡 每创建一个新的 Worker 并再次运行脚本，系统就会为每张显卡会多开一个进程

