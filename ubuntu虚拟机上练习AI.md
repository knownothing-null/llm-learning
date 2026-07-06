# 安装
```bash
sudo apt update
sudo apt install build-essential
sudo apt install python3 #python3.8说找不到，然后安装了说是最新的3.14
```

### 安装Miniconda
官网指导链接：https://www.anaconda.com/docs/getting-started/miniconda/install/linux-install#curl
```bash
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

bash ./Miniconda3-latest-Linux-x86_64.sh
```
直接运行bash就进入conda的环境了

```
bash
```

### 安装torch
```
# 指定国内镜像，否则会很慢
pip install jupyter d2l torch torchvision -i  https://pypi.tuna.tsinghua.edu.cn/simple
```

### d2l下载

```
wget https://zh-v2.d2l.ai/d2l-zh.zip
```

### 安装压缩工具

```
sudo apt install zip
```
### 解压d2l-zh.zip
```
unzip d2l-zh.zip
```
### 其他
```
sudo apt install git
git clone https://github.com/d2l-ai/d2l-pytorch-slides.git
```


