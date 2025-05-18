# fusionFM Docker 使用说明

## 1. 克隆 Space 仓库到本地

```bash
git lfs install          # 安装 Git LFS，支持大文件上传/下载
git clone https://huggingface.co/spaces/Cocofeat/fusionFM
cd fusionFM
````

---

## 2. 准备预训练权重

* 从 Hugging Face Hub 克隆预训练权重仓库：

```bash
git lfs install         # 确保 Git LFS 已启用
git clone https://huggingface.co/Cocofeat/fusionFM-weights
mv fusionFM-weights pretrain_weights
```

* 确保权重文件都在 `pretrain_weights` 文件夹内，路径示例如：

```
./pretrain_weights/model1.pth
./pretrain_weights/model2.pth
```

---

## 3. 构建 Docker 镜像

```bash
docker build -t fusionfm .
```

---

## 4. 运行 Docker 容器并挂载权重和数据

```bash
docker run -it -p 7860:7860 \
  -v $(pwd)/pretrain_weights:/app/pretrain_weights \
  -v /path/to/local/data:/app/data \
  fusionfm
```

* 说明：

  * `pretrain_weights` 挂载到容器内 `/app/pretrain_weights`
  * 本地数据目录挂载到容器内 `/app/data`
  * 如果程序有 Web 界面，打开浏览器访问 `http://localhost:7860`

---

## 5. 运行推理脚本

```bash
bash scripts/run_all_models.sh <DATA_PATH> <TASK_TYPE> <DATA_CLASS>
```

* 参数说明：

  * `DATA_PATH`：数据所在目录路径，例如 `/data1/zouke/projects_data/PAPILA/`
  * `TASK_TYPE`：任务类型，例如 `PAPILA`
  * `DATA_CLASS`：细分类别，例如 `3`

* 示例：

```bash
bash scripts/run_all_models.sh /data1/zouke/projects_data/PAPILA/ PAPILA 3
```

---

如果有任何问题，欢迎随时联系！

```

---

需要我帮你写一个更简洁的邮件正文模板，把这个 README 附上也可以。
```
