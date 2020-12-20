SST
树莓派耳机没声音

sudo raspi-config

https://blog.csdn.net/qq_39306369/article/details/86000542





# Tacotronv2 Wavernn Chinese

## 树莓派虚拟环境安装（可选）

```bash
sudo pip3 install virtualenv	# 安装虚拟环境
sudo pip3 install virtualenvwrapper # 安装虚拟环境扩展包
```

编辑`home`目录下的`.bashrc`文件，添加下面两行。

```bash
source.bashrc	# 使其生效
```

> 创建虚拟环境命令：`mkvirtualenv -p python3 +虚拟环境名`
>
> 退出虚拟环境：`deactivate`
>
> 查看机器上的所有虚拟环境：`workon空格+两个tab键`

##  安装

### 抽取GitHub项目

```bash
git clone https://github.com/lturing/tacotronv2_wavernn_chinese.git
```

### 安装依赖

首先安装`llvmlite`：

```bash
sudo apt install llvm-9  #树莓派需要版本对应namba==0.48.0  llvm-8
LLVM_CONFIG=llvm-config-9 pip3 install llvmlite
```

打开项目目录，修改`requirements.txt`如下：

```
requests==2.22.0
Flask==1.1.1
numpy==1.18.1
grpcio==1.27.2
matplotlib==3.1.2
inflect==4.1.0
tensorflow_serving_api==1.14.0
sounddevice==0.3.15
librosa==0.7.2
scipy==1.3.2
tqdm==4.36.1
Unidecode==1.1.1
hparams==0.3.0
lws==1.2.6
scikit_learn==0.23.1
numba==0.48
```

使用`pip3 install -r requirements.txt`命令安装以上依赖。

下载1.15版本的Tensorflow的whl文件后，转到下载目录后使用`pip3 install 文件名`安装。

## 文件目录

- demo：TTS后的demo wav音频文件。
- logs-Tacotron-2：Tacotron预训练模型
- logs_wavernn：WaveRNN预训练模型
- tacotron：tacotron的实现代码/拼音文件
- wavernn：WaveRNN的实现代码
- tacotron_inference_output：tacotron模型的输出结果
- wavernn_inference_output：WaveRNN模型的输出结果
- website：可视化网页部署模块

## 文件

- tacotron_preprocess.py：预处理训练数据集
- tacotron_train.py：训练TacotronV2模型
- tacotron_synthesize.py：合成语音
- wavernn_preprocess.py：利用训练好的TacotronV2生成Wavernn的训练数据
- wavernn_train.py：训练WaveRNN模型
- wavernn_gen.py：WaveRNN模型输出

## 语音合成

```bash
cd tacotronv2_wavernn_chinese
python tacotron_synthesize.py --text '现在是凌晨零点二十七分，帮您订好上午八点的闹钟。'
# 其中，参数--text 指定需要TTS的文本
```

合成的wav、attention align等文件存放于`./tacotron_inference_output`下。

```bash
python wavernn_gen.py --file ''
# 其中，参数--file 指定经tacotron合成后的.npy文件
```

经WaveRNN处理后的结果存放于`./wavernn_inference_output`下。

## 总结

TacotronV2 + WaveRNN实现的中文语音合成的结果具有高质量和高自然度的特点，同时克服了TacotronV2对长句子建模能力不足的缺陷，提高模型对长句子的语音合成效果，以及对语速的控制。

但由于树莓派的机能限制，在使用了经开源中文语音数据集标贝(女声)训练后的TacotronV2模型，输出音频所需的时间仍然较长，特别是WaveRNN的二次处理的过程耗时过长，该问题仍待解决。