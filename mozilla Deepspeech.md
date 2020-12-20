## Deepspeech install on Raspberry pi3

 ### 一、 环境需求

- Raspberry pi3：https://www.jianshu.com/p/cf35fb2afabc
- Raspbian Lite buster系统 [系统安装](https://www.jianshu.com/p/cf35fb2afabc)
- USB麦克风

### 二、参考手册

model：https://github.com/mozilla/DeepSpeech/releases

doc： https://deepspeech.readthedocs.io/en/latest/index.html

github： https://github.com/mozilla/DeepSpeech/tree/mandarin-all-2048

论坛：https://discourse.mozilla.org/c/mozilla-voice-stt/247

###  三、实践

3.1 安装DeepSpeech 0.9.1

```
sudo apt install git python3-pip python3-scipy python3-numpy python3-pyaudio libatlas3-base

pip3 install deepspeech --upgrade

下载：中文model
madir ～/deepspeech
curl -LO https://github.com/mozilla/DeepSpeech/releases/download/v0.9.1/deepspeech-0.9.1-models-zh-CN.tflite
curl -LO https://github.com/mozilla/DeepSpeech/releases/download/v0.9.1/deepspeech-0.9.1-models-zh-CN.scorer
```

3.2 准备语音文件

```
//自行下载测试的wav语音文件，并放置于deepspeech的audio中（修改代码）  建议小一点的
source ~/.profile

//抄录测试文件（根据具体情况）
deepspeech --model deepspeech-0.9.1-models-zh-CN.tflite --scorer deepspeech-0.9.1-models-zh-CN.scorer --audio audio/1.wav
deepspeech --model deepspeech-0.9.1-models-zh-CN.tflite --scorer deepspeech-0.9.1-models-zh-CN.scorer --audio audio/2.wav
deepspeech --model deepspeech-0.9.1-models-zh-CN.tflite --scorer deepspeech-0.9.1-models-zh-CN.scorer --audio audio/3.wav
```

3.3 实时录音

```
git clone -b mandarin-all-2048 https://github.com/mozilla/DeepSpeech.git


pip install halo webrtcvad --upgrade
python3 DeepSpeech-examples/mic_vad_streaming/mic_vad_streaming.py --device 1 -m eepspeech-0.9.1-models-zh-CN.tflite -s deepspeech-0.9.1-models-zh-CN.scorer
```

> //tensorflow：执行：
>
> ```
> git submodule sync tensorflow/
> git submodule update --init tensorflow/
> ```
>
> Bazel 3.1.0：https://docs.bazel.build/versions/3.1.0/install-ubuntu.html
>
> ```
> cd tensorflow
> ./configure
> 参考：
> https://deepspeech.readthedocs.io/en/v0.9.1/BUILDING.html#dependencies
> ```





https://lturing.github.io/tacotronv2_wavernn_chinese/



标贝数据：https://www.data-baker.com/open_source.html

https://test.data-baker.com/#/specs/distinguish/word