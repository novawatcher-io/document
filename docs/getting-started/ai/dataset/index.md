# 模型知识库

> 点击

RAG对话系统支持上传知识库文件，这些文件可以包含相关领域（如医疗、法律或金融等）的专业知识和术语。
通过扩展知识范围，知识库使模型能够生成更专业和准确的回答。本文为您介绍如何在RAG对话系统的WebUI页面中上传和管理知识库文件。

## 基于RAGFLOW开发


星观网络基于 [ragflow](https://ragflow.io/)  开源项目开发了大模型知识库

## 添加知识库

当不同部门或个人使用各自独立的知识库时，可以通过以下方法建立多个知识库实现数据的有效隔离

![create_dataset](/doc/assets/img/ai/dataset/create_dataset.png)

填写数据表单，添加知识库

![create_dataset_form](/doc/assets/img/ai/dataset/create_dataset_form.png)

删除知识库

![delete_dataset](/doc/assets/img/ai/dataset/delete_dataset.png)


## 上传和管理知识库文件

以告警知识库为例：

### 上传文件

在知识库页签的文件管理页面，单击新增文件，。拖拽本地文件或单击右上角的image，上传知识库文件。

![upload_file](/doc/assets/img/ai/dataset/upload_file.png)

### 解析文档

点击解析按钮，解析文档，把文档通过OCR识别，写入大模型知识库

![start_parse](/doc/assets/img/ai/dataset/start_parse.png)

### 查看文件解析和切片结果

在告警知识库页面，单击文档名称，然后进入文档条目，解析后的内容存放在如下记录中:

![select_document](/doc/assets/img/ai/dataset/select_document.png)

进入页面查看文档切片

![document](/doc/assets/img/ai/dataset/document.png)


