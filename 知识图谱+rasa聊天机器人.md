pycharm conda python3.8.5 rasa==2.0.2

https://github.com/pengyou200902/Doctor-Friende

## 1. 安装neo4j：

https://neo4j.com/docs/operations-manual/current/installation/linux/debian/#debian-install

**https://blog.csdn.net/weixin_42185136/article/details/102918663**

https://blog.csdn.net/weixin_42185136/article/details/102918663

账号：neo4j

密码：123456

```
启动：sudo service neo4j start   http://127.0.0.1:7474/browser/
查看状态： sudo service neo4j status
停止服务: sudo service neo4j stop
```



## 2.安装MITIE

git clone https://github.com/mit-nlp/MITIE.git

python setup.py build

python setup.py install



## 3. 导入知识图谱

pip install py2neo==2020.0.0

create_graph.py



## 4. 安装rasa

```
pip --default-timeout=1000 install -U rasa==2.0.1
```



## 5.安装mysql

```
sudo apt install mysql-client-core-8.0
sudo apt install mysql-server
添加密码：https://blog.csdn.net/fiq_527/article/details/109013597
```

## 6. 训练模型

```
rasa train -c config/config_pretrained_embeddings_mitie_zh.yml --data data/medical/M3-training_dataset_1564317234.json data/medical/stories.md --out models/medicalRasa2 --domain config/domains.yml --num-threads 5 --augmentation 100 -vv


```

## 

## 7.运行

```
命令行直接运行：
rasa run actions --actions MyActions.actions

rasa shell -m models/medicalRasa2/20201108-200002.tar.gz --endpoints config/endpoints.yml 


botfront运行:
rasa run actions --actions MyActions.actions

rasa run --enable-api -m models/medicalRasa2/20201108-200002.tar.gz --port 5005 --endpoints config/endpoints.yml --credentials config/credentials.yml 

运行chat-html中的网页


inferface:
参考：https://cloud.tencent.com/developer/news/46295
rasa run actions --actions MyActions.actions

rasa run --enable-api -m models/medicalRasa2/20201108-200002.tar.gz --port 5005 --endpoints config/endpoints.yml --credentials config/credentials.yml 

docker run -p 8000:8000 rasa/duckling

python3 -m http.server 8888
```

