---
title: fastapi
tags:
  - python
categories:
  - 教程
abbrlink: 7
date: 2026-05-28 0:05:00
swiper_index: 7
cover: https://img.187360.xyz/img/动漫女孩-围巾.png
---

## 一、介绍

FastAPI 是一个现代、高性能的 Python Web 框架，用于构建 API。它基于 **Starlette**（异步 Web 框架）和 **Pydantic**（数据验证库），结合了异步编程和类型提示，兼顾开发效率与运行性能。

**文档**： [https://fastapi.tiangolo.com](https://fastapi.tiangolo.com/)

**源码**： <https://github.com/tiangolo/fastapi>

### 1.核心定位

| 维度         | 核心描述                                                     |
| ------------ | ------------------------------------------------------------ |
| 设计目标     | 快速开发（代码简洁）、高性能（接近 Node.js/Go）、易维护（类型注解 + 自动文档） |
| 技术基础     | 基于 Python 3.6+ 的类型注解，整合了 Starlette（异步 Web 框架）和 Pydantic（数据校验库） |
| 核心场景     | 构建 RESTful API、前后端分离项目的后端、微服务接口、数据可视化接口、自动化测试接口 |
| 对比传统框架 | 比 Flask 更现代（原生支持异步、自动校验、自动文档），比 Django 更轻量（无内置 ORM / 模板，可灵活选择） |

简单说：FastAPI 是「为 API 而生的框架」—— 它把 Web 开发中 “重复、繁琐的工作”（如参数校验、接口文档、类型提示）自动化，让你聚焦业务逻辑，而非底层细节。

### 2.核心优势

这是 FastAPI 最核心的竞争力，也是它能快速流行的原因：

⭐️ **极致易用：新手能快速上手**

- 语法极简：核心路由语法和 Flask 几乎一致（`@app.get("/")`），你已掌握 Python 基础，10 分钟就能跑通第一个接口；
- 自动校验：基于 Pydantic 实现请求参数自动校验，不用手动写`if`判断（如 “密码长度≥6”“年龄是数字”）；
- 自动文档：写完接口自动生成交互式 API 文档（`/docs`），调试接口不用装 Postman，直接在浏览器测试。

⭐️ **高性能：接近 Go/Node.js 的速度**

- 基于 Starlette 实现异步 I/O，支持高并发场景（如秒杀、高频接口调用）；
- 在第三方基准测试中，FastAPI 的吞吐量远超 Flask，接近 Django REST Framework，是 Python Web 框架中性能第一梯队。
- 新手友好点：**入门阶段可以完全忽略 “异步”**，先写同步代码，性能完全满足学习 / 中小型项目需求。

⭐️ **类型友好：代码可读性 / 可维护性高**

- 基于 Python 类型注解（如`def get_user(id: int) -> dict`），编辑器（VS Code/PyCharm）能提供实时提示，减少语法错误；
- 类型注解既是 “代码说明” 也是 “校验规则”，一份代码实现 “文档 + 校验 + 提示” 三重作用，后期维护成本极低。

⭐️ **生态灵活：按需选择，不绑定**

- 无内置 ORM：可自由搭配 SQLAlchemy、Peewee、Tortoise-ORM（新手先学 SQLAlchemy）；
- 无内置模板：主打 API 开发，也可通过 Jinja2 扩展实现模板渲染（前后端一体场景）；
- 兼容主流工具：支持 JWT 认证、Redis 缓存、Docker 部署、云服务器上线，能对接实际开发的所有需求。

⭐️ **文档完善：中文 / 英文双版本**

- 官方文档（<https://fastapi.tiangolo.com/zh/）是> “教程 + 示例 + 最佳实践” 一体化，每个知识点都有 “最小可运行示例”；
- 文档覆盖从 “入门 Hello World” 到 “生产环境部署” 的全流程，新手能跟着一步步学，不用到处找资料。

### 3.核心特性

除了核心优势，FastAPI 还提供了 Web 开发所需的全功能支持，且都做到了 “简单、高效”：

| 核心特性        | 用途                                          | 新手优先级 |
| --------------- | --------------------------------------------- | ---------- |
| 路由系统        | 定义接口路径、请求方法（GET/POST/PUT/DELETE） | 必须掌握   |
| 参数处理        | 路径参数、查询参数、请求体、Cookie/Header     | 必须掌握   |
| 数据校验        | Pydantic 模型、字段约束、嵌套模型             | 必须掌握   |
| 响应定制        | 状态码、响应模型（过滤字段）、JSON/HTML 响应  | 必须掌握   |
| 依赖注入        | 提取公共逻辑（如登录校验、权限控制）          | 重点掌握   |
| 用户认证        | OAuth2/JWT、API Key、Cookie 认证              | 重点掌握   |
| 数据库操作      | 对接 SQLite/MySQL/PostgreSQL                  | 必须掌握   |
| 文件上传 / 下载 | 单文件 / 多文件上传、文件流下载               | 了解掌握   |
| 跨域处理        | 解决前端跨域请求问题（CORS）                  | 必须掌握   |
| 异步编程        | 异步函数、异步数据库、异步依赖                | 后期掌握   |
| 后台任务        | 接口返回后执行耗时操作（如发送邮件）          | 了解掌握   |
| 部署上线        | Gunicorn+Uvicorn、Docker、云服务器            | 后期掌握   |

### 4.适用场景

✅ **非常适合的场景**

1. 前后端分离项目的后端 API 开发（如 Vue/React 前端 + FastAPI 后端）；
2. 移动端 / 小程序的数据接口开发（APP / 小程序调用的接口）；
3. 微服务 / 分布式系统的接口开发（如订单服务、用户服务）；
4. 数据可视化 / 自动化工具的接口（如爬虫数据提供接口、数据分析接口）；
5. 新手学习 Web 开发（语法简单、反馈及时、实战价值高）。

❌ **不太适合的场景**

1. 纯静态网站（如个人博客）：用 FastAPI 大材小用，直接用静态站点生成工具（如 Hexo）更高效；
2. 重度依赖模板渲染的传统网站（如 CMS 系统）：Django 内置 Admin / 模板系统，比 FastAPI 更省心；
3. Python 2.x 项目：FastAPI 仅支持 Python 3.6+，不兼容 Python 2。

### 5.Python Web 框架对比

| 框架    | 定位          | 优势                               | 劣势                                 | 新手适配度                        |
| ------- | ------------- | ---------------------------------- | ------------------------------------ | --------------------------------- |
| FastAPI | 现代 API 框架 | 高性能、自动文档、自动校验、易上手 | 生态比 Flask/Django 小、无内置 Admin | ⭐️⭐️⭐️⭐️⭐️（推荐）                     |
| Flask   | 轻量通用框架  | 生态极丰富、极致灵活               | 需手动写校验 / 文档、性能一般        | ⭐️⭐️⭐️⭐️（经典，但不如 FastAPI 现代） |
| Django  | 全能全栈框架  | 内置 ORM/Admin/ 模板、生态完善     | 重、学习曲线陡、API 开发需额外扩展   | ⭐️⭐️⭐️（适合复杂全栈项目，入门稍难） |

### 6.相关英文单词

| 单词           | 音标               | 中文                                                        |
| -------------- | ------------------ | ----------------------------------------------------------- |
| FastAPI        | /fæst ˌeɪ piː ˈaɪ/ | 高性能 Python Web 框架（核心框架名）                        |
| uvicorn        | /ˈjuːvɪkɔːrn/      | 通俗读法：U‑vi‑corn 重音在最前面：**「优‑维‑康」**          |
| Route          | /ruːt/             | 路由（接口访问路径）                                        |
| Endpoint       | /ˈendpɔɪnt/        | 接口端点（具体 API 访问地址）                               |
| Parameter      | /pəˈræmɪtə®/       | 参数（接口入参 / 出参）                                     |
| Starlette      | /stɑːˈlet/         | FastAPI 底层 ASGI 框架                                      |
| Pydantic       | /paɪˈdæntɪk/       | FastAPI 依赖的数据校验库名                                  |
| Schema         | /ˈskiːmə/          | 数据模型 / 模式（接口数据结构定义）                         |
| Validation     | /ˌvælɪˈdeɪʃn/      | 校验（数据格式 / 规则验证）                                 |
| Async          | /ˈeɪsɪŋk/          | 异步（非阻塞的代码执行方式）                                |
| Sync           | /sɪŋk/             | 同步（阻塞式代码执行方式）                                  |
| Uvicorn        | /ˈjuːvɪkɔːn/       | 运行 FastAPI 的 ASGI 服务器                                 |
| ASGI           | /ˌeɪ es dʒiː ˈaɪ/  | 异步服务器网关接口（Asynchronous Server Gateway Interface） |
| Middleware     | /ˈmɪdlweə®/        | 中间件（接口请求 / 响应的拦截处理）                         |
| Dependency     | /dɪˈpendənsi/      | 依赖（接口共用的逻辑 / 资源）                               |
| Authentication | /ɔːˌθentɪˈkeɪʃn/   | 认证（接口访问权限验证）                                    |
| Authorization  | /ˌɔːθəraɪˈzeɪʃn/   | 授权（认证后的权限分配）                                    |
| Cors           | /kɔːz/             | 跨域资源共享（Cross-Origin Resource Sharing）               |
| Swagger        | /ˈswæɡə®/          | FastAPI 默认的接口文档 UI 框架                              |
| Declarative    | /dɪˈklærətɪv/      | 声明式的                                                    |
| Mapped         | /mæpt/             | 映射的                                                      |
| Column         | /ˈkɒləm/           | 列（数据库字段）                                            |
| nullable       | /ˈnæləbl/          | 可空的、允许为 null                                         |
| scalars        | /ˈskeɪləz/         | 标量类型                                                    |
| alias          | /ˈeɪliəs/          | 别名                                                        |
| await          | /əˈweɪt/           | 等待                                                        |
| Sequence       | /ˈsiːkwəns/        | 序列                                                        |
| model          | /ˈmɑːdl/           | 模型                                                        |
| validate       | /ˈvælɪdeɨt/        | 验证                                                        |
| Schema         | /ˈskiːmə/          | 模式                                                        |
| raise          | /reɪz/             | 抛出                                                        |
| Alchemy        | /ˈælkəmi/          | 炼金术                                                      |

## 二、环境与基础（搭建 + 第一个可运行程序）

这是 FastAPI 的入门第一步，核心是 “装对包、跑通第一个接口”，类比你学 Python 时 “安装第三方库 + 写第一个 print 程序”。

### 1.核心知识点拆解

| 知识点                  | 核心内容                                                     | 易忽略 / 易错点 ⚠️                                            |
| ----------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| FastAPI/uvicorn 安装    | 1. FastAPI：框架核心包，提供 Web 开发的所有核心功能（路由、参数处理等） 2. uvicorn：FastAPI 的运行服务器（类似 Python 解释器，专门用来跑 FastAPI 程序） | 1. 只装 FastAPI 忘装 uvicorn：运行时会直接报 “找不到服务器” 错误，这是新手最常犯的错； 2. Python 版本要求：必须≥3.6（FastAPI 不支持 Python2，装包前先执行`python --version`检查版本）； 3. 建议用虚拟环境：执行`python -m venv venv`创建独立环境（避免不同项目的包版本冲突） |
| 第一个 Hello World 程序 | 1. 导入 FastAPI 模块并创建应用实例 2. 用装饰器绑定 URL 路径和处理函数 3. 编写接口函数并返回响应 4. 用 uvicorn 启动服务 | 1. 启动命令格式易错：正确格式是`uvicorn 文件名:应用实例名 --reload`（比如文件是`main.py`、实例是`app`，需写`main:app`，而非`main.py:app`）； 2. `--reload`仅开发环境用：修改代码后自动重启服务，生产环境必须去掉（避免安全风险）； 3. 默认端口是 8000：启动后访问`http://127.0.0.1:8000`，不是 Python 常用的 8080/8888 |
| 启动参数                | 1. --reload：代码热更新 2. --port：指定运行端口（如 8080） 3. --host：允许外部访问（如 0.0.0.0） | 1. --host 0.0.0.0：默认仅本机可访问，加此参数后同一局域网的手机 / 电脑也能访问； 2. 端口被占用：报错 “Address already in use”，需换端口（如 8081） |

#### 2.1.安装依赖

在虚拟环境中安装 FastAPI

```bash
# 安装FastAPI和运行服务器uvicorn
pip install "fastapi[standard]" uvicorn

# 指定版本安装
pip install fastapi==0.135.1
pip install uvicorn==0.41.0

# 验证安装
pip show fastapi
pip show uvicorn
一键获取完整项目代码bash12345678910
```

#### 2.2.编写程序

新建文件`main01.py`，写入以下代码：

```python
# 1. 导入FastAPI模块
from fastapi import FastAPI
import uvicorn

# 2. 创建FastAPI应用实例（所有接口都挂在这个实例上）
app01 = FastAPI()

# 3. 用装饰器绑定URL路径和处理函数（@app.get("/") 表示响应GET请求，路径为/）
@app01.get("/")
def read_root():
    # 4. 返回响应（FastAPI自动把字典转换成JSON格式）
    return {"message": "Hello FastAPI!"}

if __name__ == '__main__':
    # 传入导入字符串（推荐，符合热重载要求）
    # 格式："文件名:应用实例名"，当前文件是main01.py，所以写"main01:app01"
    uvicorn.run("main01:app01", host='127.0.0.1', port=8000, reload=True)

    # 关闭热重载（仅临时测试用）
    # 移除reload参数，应用程序作为导入字符串传递，才能启用“reload”或“workers”
    # uvicorn.run(app01, host='127.0.0.1', port=8000)
一键获取完整项目代码python123456789101112131415161718192021
```

#### 2.3.启动服务

1. 运行python脚本（代码中要用服务器启动代码）

    ```python
    # 传入导入字符串（推荐，符合热重载要求）
    uvicorn.run("main01:app01", host='0.0.0.0', port=8000, reload=True)
    
    # 关闭热重载（仅临时测试用）
    uvicorn.run(app01, host='0.0.0.0', port=8000)
    一键获取完整项目代码python12345
    ```

    终端执行命令:

    ```cmd
    python main01.py
    一键获取完整项目代码cmd1
    ```

2. 服务器启动项目（终端执行启动命令）

    ```shell
    # 基础启动（默认端口8000，仅本机访问）
    uvicorn main:app --reload
    
    # 自定义启动（指定端口8080，允许局域网访问）
    # uvicorn main:app --reload --port 8080 --host 0.0.0.0
    一键获取完整项目代码shell12345
    ```

3. 调试命令

    ```shell
    fastapi dev main01.py
    一键获取完整项目代码shell1
    ```

#### 2.4.验证结果

✅ `http://127.0.0.1:8000`

- **作用**：这是你 FastAPI 应用的**根路径**
- 打开浏览器访问 `http://127.0.0.1:8000`，能看到 `{"message":"Hello FastAPI!"}` 即成功。

✅ `http://127.0.0.1:8000/docs`

- **作用**：FastAPI 自动生成的 **Swagger UI 交互式接口文档**（最常用）
- ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/132594ca5b844fee8a4c209b818cd660.png#pic_center)

✅ `http://127.0.0.1:8000/redoc`

- **作用**：FastAPI 自动生成的 **ReDoc 风格接口文档**（纯文档展示）
- ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/a904cc95a8c6416c9430f8ffbe18beab.png#pic_center)

### 3.PyCharm 搭建

#### 3.1.前置准备（确认 PyCharm 环境）

1. 确保 PyCharm 2024.3.6 已安装（社区版 / 专业版均可，新手用社区版足够）；
2. 确保 PyCharm 已配置好 Python 解释器（3.6 + 版本，FastAPI 要求）：
    - 打开 PyCharm → 右上角`File` → `Settings` → `Project: 你的项目名` → `Python Interpreter`；
    - 能看到 Python 版本（如 3.13）即配置成功，若未配置，点击`Add Interpreter`选择本地 Python 解释器。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/4bc5187b971045d49c98663b9ddc6633.jpeg#pic_center)

#### 3.2.创建 FastAPI 项目

- 打开 PyCharm，点击`New Project`；

- 配置项目信息（关键参数看截图注释）：

    | 配置项             | 操作说明                                               | 易错点 ⚠️                                                     |
    | ------------------ | ------------------------------------------------------ | ------------------------------------------------------------ |
    | Location           | 选择项目保存路径（如`D:\Workspaces\python\FastAPI01`） | 路径不要包含中文 / 空格，否则可能报错                        |
    | Python Interpreter | 选择已配置的 Python 解释器（3.6+）                     | 不要选 “Create a virtual environment”（新手先不用虚拟环境，避免额外配置） |

- 点击`Create`创建项目。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/0c333cdc0c5b4802817e74191b3b62ba.jpeg#pic_center)

| 勾选项                 | 作用说明                                                     | 适用场景 & 注意点 ⚠️                                          |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 从基础解释器继承软件包 | 勾选后，虚拟环境会自动复制 “基础 Python 解释器” 中已安装的包（比如你本地 Python 装过的`requests`/`numpy`等） | - 适合想快速复用已装包的场景； - 不勾选则虚拟环境是 “纯净的”，需重新安装依赖（FastAPI 推荐不勾选，避免包版本冲突） |
| 可用于所有项目         | 勾选后，当前创建的虚拟环境会被 PyCharm 标记为 “全局可用”，后续新建其他项目时也能选择这个虚拟环境 | - 适合需要多个项目共用同一套依赖的场景； - 不勾选则该虚拟环境仅当前项目可用（FastAPI 项目建议不勾选，保持项目环境独立） |

#### 3.3.运行 / 调试 FastAPI

##### 3.5.1.运行 FastAPI

- 点击 PyCharm 右上角的运行按钮（绿色三角，旁边是你命名的`FastAPI Demo`）；

- 等待运行成功，PyCharm 的 `Run` 窗口会显示以下信息（关键日志）：

    ```
    D:\Workspaces\python\fastapi01\.venv\Scripts\python.exe -m uvicorn main:app --reload 
    INFO:     Will watch for changes in these directories: ['D:\\Workspaces\\python\\FastAPI01']
    INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
    INFO:     Started reloader process [26216] using StatReload
    INFO:     Started server process [21972]
    INFO:     Waiting for application startup.
    INFO:     Application startup complete.
    一键获取完整项目代码1234567
    ```

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/afa207ed08a940ff887d4b7109eabc13.jpeg#pic_center)

##### 3.5.2.验证运行结果

- 打开浏览器，访问 `http://127.0.0.1:8000`，能看到以下 JSON 即成功：

    ```json
    {"message":"Hello World"}
    一键获取完整项目代码json1
    ```

- 访问测试路由 `http://127.0.0.1:8000/hello/fastapi`，返回：

    ```json
    {"message":"Hello fastapi"}
    一键获取完整项目代码json1
    ```

- 访问自动文档`http://127.0.0.1:8000/docs`，能看到交互式文档即完全成功。

#### 3.4.手动配置运行参数的情况

这是新手最容易卡壳的地方 ——PyCharm 默认无法直接运行 FastAPI，需要手动配置运行参数（替代终端的`uvicorn`命令）。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/7e5e4c62380f4a8b9ddd218154d1d1aa.jpeg#pic_center)

##### 3.4.1.步骤 1：安装 FastAPI 和 Uvicorn 依赖

PyCharm 安装依赖有 2 种方式，任选其一（推荐方式 1，更直观）：

###### 方式 1：PyCharm 内置终端安装（推荐）

- 打开 PyCharm 底部的`Terminal`（终端）；

- 输入以下命令安装依赖（和手动敲命令一致）：

    ```bash
    pip install fastapi uvicorn
    一键获取完整项目代码bash1
    ```

- 等待安装完成（终端显示`Successfully installed...`即成功）。

###### 方式 2：通过 PyCharm 的 Package Manager 安装

- 打开`File` → `Settings` → `Project: fastapi_demo` → `Python Interpreter`；
- 点击右侧`+`号，搜索`fastapi`，点击`Install Package`；
- 同理搜索`uvicorn`并安装；
- 安装完成后点击`OK`关闭设置。

✅ 验证安装：终端输入`pip show fastapi`，能看到版本信息即安装成功。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/7fc0a714455c4cdfb04921cb8f05df2c.jpeg#pic_center)

##### 3.4.2.步骤 2：编写 FastAPI 代码

1. 在项目根目录右键 → `New` → `Python File`，命名为`main.py`（名字任意，建议用 main）；

2. 写入基础 FastAPI 代码（复制即可）：

    ```python
    # 导入FastAPI模块
    from fastapi import FastAPI
    
    # 创建FastAPI应用实例
    app = FastAPI()
    
    # 定义路由：根路径GET请求
    @app.get("/")
    def read_root():
        return {"message": "Hello FastAPI! 从PyCharm启动成功"}
    
    # 新增测试路由：路径参数
    @app.get("/users/{user_id}")
    def get_user(user_id: int):
        return {"user_id": user_id, "msg": "查询用户成功"}
    一键获取完整项目代码python123456789101112131415
    ```

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/49a000018e204141a353ea880542bcc3.jpeg#pic_center)

##### 3.4.3.步骤 3：配置 PyCharm 运行 / 调试环境

###### 3.4.3.1.打开运行配置界面

- 点击 PyCharm 右上角的`Add Configuration...`（或点击当前无配置的下拉框→`Edit Configurations`）；

    ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/e477eb9d63384a758bcef2da9d5baac4.jpeg#pic_center)

- 在弹出的窗口中，点击左上角`+`号，选择`Python`（注意：不是`FastAPI`，PyCharm 社区版无 FastAPI 专属配置）。

    ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/12c8f49931e24bf6b3d3957186a2cf32.jpeg#pic_center)

###### 3.4.3.2.配置运行参数（关键！）

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/af6fdf24b258499ca98a49d1608cdf9d.jpeg#pic_center)

当前 FastAPI 运行配置的参数说明:

| 参数项                  | 当前值                                 | 作用说明                                                     | 易忽略 / 注意点 ⚠️                                            |
| ----------------------- | -------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 名称 (N)                | main                                   | 配置的名称（自定义，方便区分不同运行配置）                   | 无实际功能影响，仅用于标识配置                               |
| 应用程序文件            | D:\Workspaces\python\fastapi02\main.py | FastAPI 的入口文件（代码所在的 Python 文件）                 | 必须是你的 FastAPI 代码文件（如`main.py`），路径错误会导致找不到代码 |
| 应用程序名称            | <自动检测>                             | 自动识别代码中 FastAPI 的应用实例名（即`app = FastAPI()`中的`app`） | 无需手动填写，PyCharm 会自动检测代码里的实例名（如`app`/`api`） |
| Uvicorn 选项            | –reload                                | Uvicorn 的运行参数：`--reload`表示代码修改后自动重启服务（开发环境必备） | 若需指定端口，可补充为`--reload --port 8000`（多个参数用空格分隔） |
| 环境变量 (H)            | （空）                                 | 配置运行时的环境变量（如数据库地址、密钥等）                 | 新手暂时无需配置，复杂项目可在此添加（如`DATABASE_URL=sqlite:///data.db`） |
| Python 解释器 §         | Python 3.13 (fastapi02) …              | 运行 FastAPI 使用的 Python 解释器（包含已安装的`fastapi`/`uvicorn`依赖） | 必须是已安装 FastAPI 依赖的解释器，否则会报 “模块找不到” 错误 |
| 工作目录 (W)            | （空）                                 | 程序运行时的工作目录（默认是项目根目录）                     | 建议留空，PyCharm 会自动使用项目根目录；若填写，需确保是代码所在的目录 |
| 将内容添加到 PYTHONPATH | 勾选                                   | 将当前项目路径添加到 Python 的模块搜索路径，确保代码能正确导入本地模块 | 必须勾选，否则可能出现 “本地模块导入失败” 的错误             |
| 将源根添加到 PYTHONPATH | 勾选                                   | 将项目的 “源根目录”（代码所在目录）添加到 Python 搜索路径    | 必须勾选，作用同 “将内容添加到 PYTHONPATH”，保障模块导入     |

###### 3.4.3.3.保存配置

点击`Apply`（应用）→ `OK`（确定），完成运行配置。

##### 3.4.4.运行 FastAPI

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/693cc30c5d2d48698610b13018ed27f5.jpeg#pic_center)

## 三、基础入门

### 1.路由系统（定义接口路径与请求方法）

路由是 FastAPI 的 “骨架”—— 决定用户访问哪个 URL 能触发哪个功能，类比 Python 的 “函数调用”：URL 路径 = 函数名，请求方法 = 调用方式。

#### 1.1.核心知识点拆解

| 知识点         | 核心内容                                                     | 易忽略 / 易错点 ⚠️                                            |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 请求方法装饰器 | 1. @app.get ()：查询数据（如查用户、查商品） 2. @app.post ()：新增数据（如注册、添加商品） 3. @app.put ()：修改数据（如改密码） 4. @app.delete ()：删除数据（如删订单） | 1. 同一 URL 可绑定不同请求方法：比如`/users`既可以用 GET 查，也可以用 POST 加，FastAPI 会根据请求方法区分； 2. 装饰器名大小写敏感：必须写`@app.get()`，而非`@app.GET()`； 3. 函数名无强制要求：只要语义清晰即可（如`get_users`/`query_users`） |
| 路径参数       | 1. 格式：`/路径/{参数名}`（如`/users/{user_id}`） 2. 类型注解：指定参数类型（int/str 等） 3. 自动校验：类型不匹配直接返回错误 | 1. 类型注解是核心：比如`user_id: int`，传字符串会自动返回 422 错误（无需手动写 if 判断）； 2. 参数名必须一致：URL 里是`{user_id}`，函数参数必须是`user_id`（不能写成 uid）； 3. 路径参数仅适合简单值：复杂数据（如 JSON）需用请求体传递 |

#### 1.2.实操示例

##### 示例 1：不同请求方法的路由

修改`main.py`，添加以下代码：

```python
# GET请求：查询所有用户
@app.get("/users")
def get_users():
    return {"msg": "查询所有用户成功"}

# POST请求：新增用户
@app.post("/users")
def add_user():
    return {"msg": "新增用户成功"}

# PUT请求：修改指定用户
@app.put("/users/1")
def update_user():
    return {"msg": "修改ID为1的用户成功"}

# DELETE请求：删除指定用户
@app.delete("/users/1")
def delete_user():
    return {"msg": "删除ID为1的用户成功"}
一键获取完整项目代码python12345678910111213141516171819
```

##### 示例 2：路径参数的使用

```python
# 基础路径参数（提取user_id，注解为int类型）
@app.get("/users/{user_id}")
def get_user(user_id: int):
    return {"user_id": user_id, "msg": "查询用户成功"}

# 多路径参数（同时提取order_id和item_id）
@app.get("/orders/{order_id}/items/{item_id}")
def get_order_item(order_id: int, item_id: str):
    return {"order_id": order_id, "item_id": item_id}
一键获取完整项目代码python123456789
```

启动服务后，可访问以下 URL 测试：

- `http://127.0.0.1:8000/users/123` → 提取 user_id=123
- `http://127.0.0.1:8000/orders/1001/items/phone` → 提取 order_id=1001、item_id=phone

### 2.请求参数（接收前端传递的数据）

请求参数是 FastAPI 与前端 “沟通” 的核心，类比 Python 函数的 “参数传递”—— 前端给 FastAPI 传数据，就像给函数传参数一样。FastAPI 支持 3 种常用参数类型，覆盖 90% 的场景。

#### 2.1.核心知识点拆解

| 参数类型 | 核心内容                                                     | 易忽略 / 易错点 ⚠️                                            |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 查询参数 | 1. 格式：URL 后加`?参数名=值`（如`/items?skip=0&limit=10`）2. 函数内直接定义参数，支持默认值3. 不加默认值即为必选参数 | 1. 必选参数不传会报错：比如`q: str`不加默认值，访问`/search`会返回 422 错误；2. 类型注解生效：`skip: int`传字符串会自动校验失败；3. 多个参数用 & 分隔：正确格式是`?skip=0&limit=10`，而非`?skip=0 limit=10` |
| 请求体   | 1. 用于传递复杂数据（如 JSON、表单）2. 需用 Pydantic 的 BaseModel 定义参数结构3. 仅支持 POST/PUT/PATCH 方法（GET 无请求体） | 1. 必须导入 BaseModel：新手常忘写`from pydantic import BaseModel`，导致报错；2. 请求体仅支持 POST/PUT：用 GET 接收请求体会违反 HTTP 规范，直接报错；3. 字段名必须一致：前端传`{"userName":"admin"}`，模型里是`username`会解析失败 |
| 混合参数 | 路径参数 + 查询参数 + 请求体组合使用                         | 1. 参数顺序不影响：FastAPI 按类型自动识别，无需按顺序定义；2. 请求体只能有一个：同一接口不能定义多个请求体参数 |

#### 2.2.实操示例

##### 示例 1：查询参数

```python
# 带默认值的查询参数（可选）
@app.get("/items")
def get_items(skip: int = 0, limit: int = 10):
    # 访问/items → skip=0, limit=10
    # 访问/items?skip=5&limit=20 → skip=5, limit=20
    return {"skip": skip, "limit": limit, "items": ["商品1", "商品2"]}

# 必选查询参数（不加默认值）
@app.get("/search")
def search(q: str):
    # 必须传q参数，如/search?q=手机
    return {"q": q, "msg": f"搜索关键词：{q}"}
一键获取完整项目代码python123456789101112
```

##### 示例 2：请求体（需导入 BaseModel）

```python
from pydantic import BaseModel

# 1. 定义请求体模型（数据模板）
class User(BaseModel):
    username: str  # 必选字段
    password: str  # 必选字段
    age: int = 18   # 可选字段，默认值18

# 2. POST请求接收请求体
@app.post("/login")
def login(user: User):
    # FastAPI自动把前端传的JSON转成User对象
    if user.username == "admin" and user.password == "123456":
        return {"code": 200, "msg": "登录成功", "age": user.age}
    else:
        return {"code": 400, "msg": "用户名或密码错误"}
一键获取完整项目代码python12345678910111213141516
```

Pydantic 美式音标/paɪˈdæntɪk/ 通俗易记: 拆解为 3 个音节，重音落在第二个音节上：**「派 - 丹 - 提克」**（拼音参考：pài - dān - tī kè）

##### 示例 3：混合参数（路径 + 查询 + 请求体）

```python
# 定义请求体模型
class ItemUpdate(BaseModel):
    name: str
    price: float

# 路径参数：item_id；查询参数：is_verify；请求体：ItemUpdate
@app.put("/items/{item_id}")
def update_item(item_id: int, is_verify: bool = True, item: ItemUpdate):
    return {
        "item_id": item_id,
        "is_verify": is_verify,
        "item_name": item.name,
        "item_price": item.price
    }
一键获取完整项目代码python1234567891011121314
```

### 3.响应处理（返回前端的内容）

响应处理是 FastAPI 把处理结果返回给前端的环节，核心是 “返回格式 + 状态码 + 自定义配置”，FastAPI 默认处理了大部分场景，新手只需掌握基础用法。

#### 3.1.核心知识点拆解

| 知识点     | 核心内容                                                     | 易忽略 / 易错点 ⚠️                                            |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 基础响应   | 1. 直接返回字典（自动转 JSON） 2. 返回字符串 / 数字（自动封装） 3. 返回列表（需注意 JSON 规范） | 1. 返回字典时 key 建议用字符串：符合 JSON 规范，避免解析错误； 2. 返回非字典类型时，Content-Type 会自动调整（如字符串返回 text/plain） |
| 响应状态码 | 1. 装饰器加 status_code 参数（推荐） 2. 用 JSONResponse 指定状态码 + 响应头 | 1. 状态码需符合 HTTP 规范：201（创建成功）、400（参数错误）、404（资源不存在）； 2. 自定义响应头必须用 JSONResponse：直接返回字典无法设置头信息 |

#### 3.2.实操示例

##### 示例 1：基础响应

```python
# 返回字典（推荐，自动转JSON）
@app.get("/dict")
def resp_dict():
    return {"code": 200, "msg": "成功", "data": [1,2,3]}

# 返回字符串
@app.get("/str")
def resp_str():
    return "Hello FastAPI"

# 返回数字
@app.get("/num")
def resp_num():
    return 200
一键获取完整项目代码python1234567891011121314
```

##### 示例 2：自定义响应状态码

```python
from fastapi.responses import JSONResponse

# 方式1：装饰器指定状态码（推荐）
@app.post("/users", status_code=201)  # 201表示创建成功
def add_user():
    return {"msg": "用户创建成功"}

# 方式2：返回JSONResponse（自定义响应头）
@app.get("/custom")
def custom_resp():
    return JSONResponse(
        content={"code": 200, "msg": "自定义响应"},
        status_code=200,
        headers={"X-Token": "123456"}  # 自定义响应头
    )
一键获取完整项目代码python123456789101112131415
```

### 4.自动 API 文档（FastAPI 核心亮点）

FastAPI 最贴心的功能之一 —— 写完接口自动生成交互式文档，无需手动编写，新手调试接口无需额外工具（如 Postman）。

#### 4.1.核心知识点拆解

| 知识点              | 核心内容                                                     | 易忽略 / 易错点 ⚠️                                            |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Swagger UI（/docs） | 1. 访问`http://127.0.0.1:8000/docs`2. 交互式调试（Try it out）3. 自动识别参数 / 状态码 | 1. 零配置生成：无需像其他框架那样加注解，基于类型注解自动生成；2. 生产环境可关闭：`app = FastAPI(docs_url=None)`；3. 接口描述可增强：通过 summary/description 参数添加说明 |
| ReDoc（/redoc）     | 更简洁的文档样式，适合展示给非开发人员                       | 无特殊易错点，按需选择 /docs 或 /redoc 即可                  |

#### 4.2.实操示例

##### 示例 1：访问自动文档

启动服务后，直接访问以下 URL：

- Swagger UI：`http://127.0.0.1:8000/docs`（推荐，支持交互式调试）
- ReDoc：`http://127.0.0.1:8000/redoc`（简洁展示）

##### 示例 2：增强接口文档描述

```python
# 给接口加summary（简短描述）和description（详细描述）
@app.get("/users/{user_id}", summary="查询单个用户", description="根据用户ID查询用户信息，ID必须是数字类型，支持1-1000范围内的ID")
def get_user(user_id: int):
    return {"user_id": user_id, "msg": "查询成功"}
一键获取完整项目代码python1234
```

访问`/docs`能看到接口的描述信息，调试时更清晰。

### 5.中间件

#### 5.1.核心概念

中间件是在**请求到达路由处理函数之前**和**响应返回给客户端之后**执行的代码，相当于请求 / 响应的 “拦截器”。它可以统一处理日志、认证、跨域、请求耗时统计等通用逻辑，是 FastAPI 实现请求生命周期管控的核心机制。

FastAPI 基于 Starlette 框架，其中间件系统完全继承自 Starlette，支持同步 / 异步两种写法。

#### 5.2.核心特点

- 链式执行：多个中间件按注册顺序执行（请求阶段从上到下，响应阶段从下到上）
- 可修改请求 / 响应：可以修改请求头、响应体、状态码等
- 全局生效：默认对所有路由生效，也可通过路径匹配实现局部生效

#### 5.3.代码示例

```python
from fastapi import FastAPI, Request
from fastapi.responses import JSONResponse
import time

app = FastAPI()


# 1. 基础中间件：统计请求耗时
@app.middleware("http")
async def add_process_time_header(request: Request, call_next):
    print("Middleware 1 start...")
    # 请求到达时执行（前置逻辑）
    start_time = time.time()

    # 调用下一个中间件/路由处理函数
    response = await call_next(request)

    # 响应返回时执行（后置逻辑）
    process_time = time.time() - start_time
    response.headers["X-Process-Time"] = str(process_time)  # 给响应加自定义头
    print("Middleware 1 end...")
    return response


# 2. 中间件：全局异常捕获
@app.middleware("http")
async def global_exception_handler(request: Request, call_next):
    print("Middleware 2 start...")
    try:
        response = await call_next(request)
    except Exception as e:
        return JSONResponse(
            status_code=500,
            content={"detail": f"服务器内部错误: {str(e)}"}
        )

    print("Middleware 2 end...")
    return response

# 测试路由
@app.get("/test")
async def test():
    return {"message": "Hello Middleware"}
一键获取完整项目代码python12345678910111213141516171819202122232425262728293031323334353637383940414243
```

执行输出:

```cmd
Middleware 2 start...
Middleware 1 start...
Middleware 1 end...
Middleware 2 end...
INFO:     127.0.0.1:61945 - "GET /test HTTP/1.1" 200 OK
一键获取完整项目代码cmd12345
```

#### 5.4.常用内置中间件

```python
from fastapi.middleware.cors import CORSMiddleware
from fastapi.middleware.gzip import GZipMiddleware

# 跨域中间件（最常用）
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # 允许的源，生产环境需指定具体域名
    allow_credentials=True,
    allow_methods=["*"],  # 允许的请求方法
    allow_headers=["*"],  # 允许的请求头
)

# Gzip压缩中间件（优化响应体积）
app.add_middleware(GZipMiddleware, minimum_size=1000)  # 仅压缩大于1000字节的响应
一键获取完整项目代码python1234567891011121314
```

### 6.依赖注入

#### 6.1.核心概念

依赖注入是一种设计模式，允许你将函数 / 类的依赖项 “注入” 到函数中，而不是在函数内部硬编码创建。FastAPI 的依赖注入系统是其核心优势之一，支持：

- 路径操作函数的参数依赖
- 全局 / 路由级别的依赖
- 依赖的嵌套调用
- 带参数的依赖

#### 6.2.核心使用场景

- 认证鉴权（如验证 Token）
- 数据库连接获取
- 请求参数校验 / 解析
- 资源复用（如复用数据库连接池）

#### 6.3.基础用法示例

```python
from fastapi import FastAPI, Depends, HTTPException
from pydantic import BaseModel
from typing import Optional

app = FastAPI()

# 定义依赖函数（无参数）
async def get_token_header(x_token: str = Depends()):
    """验证请求头中的X-Token"""
    if x_token != "fake-super-secret-token":
        raise HTTPException(status_code=400, detail="X-Token header invalid")

# 定义带参数的依赖类
class PaginationParams(BaseModel):
    page: int = 1
    size: int = 10

async def get_pagination_params(params: PaginationParams = Depends()):
    """解析分页参数"""
    if params.size > 100:
        params.size = 100  # 限制最大页大小
    return params

# 1. 单个依赖注入
@app.get("/items/")
async def read_items(token: str = Depends(get_token_header)):
    return {"token": token, "items": [{"id": 1}, {"id": 2}]}

# 2. 多个依赖注入 + 嵌套依赖
async def get_current_user(token: str = Depends(get_token_header)):
    """嵌套依赖：先验证token，再获取当前用户"""
    return {"username": "admin", "token": token}

@app.get("/users/me/")
async def read_current_user(
    user: dict = Depends(get_current_user),
    pagination: PaginationParams = Depends(get_pagination_params)
):
    return {"user": user, "pagination": pagination}

# 3. 路由级依赖（对该路由下所有操作生效）
from fastapi import APIRouter

router = APIRouter(dependencies=[Depends(get_token_header)])

@router.get("/private/")
async def private_route():
    return {"message": "This is a private route"}

app.include_router(router)

# 4. 全局依赖（对所有路由生效）
# app = FastAPI(dependencies=[Depends(get_token_header)])
一键获取完整项目代码python1234567891011121314151617181920212223242526272829303132333435363738394041424344454647484950515253
```

#### 6.4.依赖的高级用法：依赖项作为类

```python
from fastapi import Depends

class DatabaseConnection:
    def __init__(self):
        # 模拟创建数据库连接
        self.conn = "db_connection_123"
    
    async def __aenter__(self):
        # 异步上下文管理器（配合async with）
        return self.conn
    
    async def __aexit__(self, exc_type, exc_val, exc_tb):
        # 关闭连接
        self.conn = None

# 依赖函数返回类实例
async def get_db():
    db = DatabaseConnection()
    try:
        yield db.conn  # 使用yield实现依赖的生命周期管理（请求结束后执行后续逻辑）
    finally:
        # 请求处理完成后执行（如关闭连接）
        await db.__aexit__(None, None, None)

@app.get("/db/")
async def use_db(db_conn: str = Depends(get_db)):
    return {"db_connection": db_conn}
一键获取完整项目代码python123456789101112131415161718192021222324252627
```

### 7.ORM

#### 7.1.核心概念

ORM（Object-Relational Mapping，对象关系映射）是将数据库表结构映射为 Python 类，通过操作类 / 对象来实现数据库的增删改查，无需编写原生 SQL。

FastAPI 本身不内置 ORM，但最常用的组合是：

- **SQLAlchemy**（老牌 ORM，支持同步 / 异步）
- **Peewee**（轻量级 ORM）
- **Tortoise-ORM**（专为异步设计的 ORM）

这里重点讲解最主流的 **SQLAlchemy 2.0 + FastAPI** 组合。

#### 7.2.完整实战示例（SQLAlchemy + FastAPI）

##### 步骤 1：安装依赖

```bash
pip install fastapi uvicorn sqlalchemy asyncpg python-dotenv
一键获取完整项目代码bash1
```

##### 步骤 2：项目结构

```plaintext
project/
├── main.py          # FastAPI 主程序
├── database.py      # 数据库配置
└── models.py        # 数据模型
一键获取完整项目代码plaintext1234
```

##### 步骤 3：数据库配置（database.py）

```python
from sqlalchemy import create_engine
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker
from sqlalchemy.ext.asyncio import create_async_engine, AsyncSession

# 同步数据库URL（SQLite示例）
SQLALCHEMY_DATABASE_URL = "sqlite:///./test.db"
# 异步数据库URL（PostgreSQL示例）
# SQLALCHEMY_DATABASE_URL = "postgresql+asyncpg://user:password@postgresserver/db"

# 同步引擎
engine = create_engine(
    SQLALCHEMY_DATABASE_URL, connect_args={"check_same_thread": False}  # SQLite必需
)
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)

# 异步引擎
async_engine = create_async_engine(SQLALCHEMY_DATABASE_URL)
AsyncSessionLocal = sessionmaker(
    async_engine, class_=AsyncSession, expire_on_commit=False
)

Base = declarative_base()

# 依赖函数：获取同步数据库会话
def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

# 依赖函数：获取异步数据库会话
async def get_async_db():
    async with AsyncSessionLocal() as db:
        yield db
        await db.commit()
一键获取完整项目代码python12345678910111213141516171819202122232425262728293031323334353637
```

##### 步骤 4：数据模型（models.py）

```python
from sqlalchemy import Column, Integer, String, Boolean
from database import Base

# 定义数据库模型（映射到数据库表）
class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True, index=True)
    username = Column(String, unique=True, index=True)
    email = Column(String, unique=True, index=True)
    hashed_password = Column(String)
    is_active = Column(Boolean, default=True)
一键获取完整项目代码python123456789101112
```

##### 步骤 5：FastAPI 中使用 ORM（main.py）

```python
from fastapi import FastAPI, Depends, HTTPException
from sqlalchemy.orm import Session
from sqlalchemy.ext.asyncio import AsyncSession
from sqlalchemy.future import select
import models
import database
from pydantic import BaseModel

# 创建数据库表
models.Base.metadata.create_all(bind=database.engine)

app = FastAPI()

# Pydantic 模型（数据校验/序列化）
class UserCreate(BaseModel):
    username: str
    email: str
    password: str

class UserResponse(BaseModel):
    id: int
    username: str
    email: str
    is_active: bool

    class Config:
        orm_mode = True  # 支持从ORM对象转换为Pydantic模型

# 1. 同步ORM操作
@app.post("/users/", response_model=UserResponse)
def create_user(user: UserCreate, db: Session = Depends(database.get_db)):
    # 检查用户是否已存在
    db_user = db.query(models.User).filter(models.User.email == user.email).first()
    if db_user:
        raise HTTPException(status_code=400, detail="Email already registered")
    
    # 创建新用户
    new_user = models.User(
        username=user.username,
        email=user.email,
        hashed_password=user.password  # 生产环境需加密密码
    )
    db.add(new_user)
    db.commit()
    db.refresh(new_user)  # 刷新获取自增ID
    return new_user

# 2. 异步ORM操作（推荐）
@app.get("/users/{user_id}", response_model=UserResponse)
async def get_user(user_id: int, db: AsyncSession = Depends(database.get_async_db)):
    result = await db.execute(select(models.User).where(models.User.id == user_id))
    db_user = result.scalars().first()
    if not db_user:
        raise HTTPException(status_code=404, detail="User not found")
    return db_user
一键获取完整项目代码python12345678910111213141516171819202122232425262728293031323334353637383940414243444546474849505152535455
```

### 8.目录结构

#### 8.1.核心原则

FastAPI 没有强制的目录结构，但遵循以下原则能让项目更易维护：

1. **分离关注点**：路由、模型、依赖、配置等分开存放
2. **可扩展性**：便于新增功能模块
3. **清晰性**：新手能快速定位代码位置

#### 8.2.不同规模的目录结构

##### 8.2.1.小型项目（单文件 / 极简结构）

适合接口少（<10 个）、功能简单的项目，核心代码集中在主文件，快速开发：

```cmd
project/
├── main.py          # 主程序（路由、依赖、配置都在这里）
├── requirements.txt # 依赖清单
└── .env             # 环境变量（可选）
一键获取完整项目代码cmd1234
```

##### 8.2.2.中大型项目（标准化结构）

这是最常用的结构，适配绝大多数生产级项目，支持多模块、多环境、可测试：

```cmd
project/
├── alembic/                # 数据库迁移（SQLAlchemy 配套工具）
├── app/                    # 核心应用代码（项目主包）
│   ├── __init__.py         # 包初始化
│   ├── main.py             # FastAPI 应用实例创建、全局配置
│   ├── core/               # 核心配置（全局生效）
│   │   ├── __init__.py
│   │   ├── config.py       # 环境变量、配置项（数据库URL、密钥等）
│   │   ├── dependencies.py # 全局依赖（如数据库连接、认证）
│   │   └── middleware.py   # 全局中间件（跨域、日志等）
│   ├── api/                # 路由与接口（按功能模块划分）
│   │   ├── __init__.py
│   │   ├── deps.py         # 接口级依赖（如局部认证、参数校验）
│   │   ├── v1/             # API 版本控制（可选，推荐）
│   │   │   ├── __init__.py
│   │   │   ├── items.py    # 商品相关接口
│   │   │   └── users.py    # 用户相关接口
│   ├── models/             # 数据库模型（ORM 模型）
│   │   ├── __init__.py
│   │   ├── base.py         # 所有模型的基类（如继承 SQLAlchemy Base）
│   │   ├── item.py         # 商品模型
│   │   └── user.py         # 用户模型
│   ├── schemas/            # Pydantic 模型（数据校验/序列化）
│   │   ├── __init__.py
│   │   ├── item.py         # 商品的请求/响应模型
│   │   └── user.py         # 用户的请求/响应模型
│   ├── crud/               # 数据库操作（CRUD 逻辑）
│   │   ├── __init__.py
│   │   ├── base.py         # 通用 CRUD 方法（如增删改查封装）
│   │   ├── crud_item.py    # 商品的具体 CRUD
│   │   └── crud_user.py    # 用户的具体 CRUD
│   ├── utils/              # 工具函数（通用功能）
│   │   ├── __init__.py
│   │   ├── logger.py       # 日志配置
│   │   └── security.py     # 加密、Token 生成等
│   └── db/                 # 数据库连接
│       ├── __init__.py
│       └── session.py      # 数据库会话创建（同步/异步）
├── tests/                  # 测试用例（按模块划分）
│   ├── __init__.py
│   ├── test_items.py
│   └── test_users.py
├── .env                    # 环境变量（开发环境）
├── .env.prod               # 生产环境变量（不提交到仓库）
├── .gitignore              # Git 忽略文件
├── alembic.ini             # Alembic 配置
├── requirements.txt        # 生产依赖
├── requirements-dev.txt    # 开发依赖（测试、格式化等）
├── Dockerfile              # Docker配置文件（如果使用Docker）
└── README.md               # 项目说明
一键获取完整项目代码cmd1234567891011121314151617181920212223242526272829303132333435363738394041424344454647484950
```

在Python项目中，`__init__.py` 文件的主要作用是将目录标识为一个Python包。它使得目录中的模块可以被导入和使用。在一些情况下，`__init__.py` 可以不仅仅是一个空文件，还可以包含一些初始化代码。

对于Python 3.3及以上版本，`__init__.py` 文件不是强制性的，即使没有 `__init__.py` 文件，Python解释器也可以识别包。然而，添加 `__init__.py` 文件仍然是一个良好的习惯，可以避免某些情况下的意外行为，并且明确表示该目录是一个包。

##### 8.2.3.超大型项目（微服务 / 多应用）

适合多团队协作、功能复杂的项目，进一步拆分模块：

```cmd
project/
├── apps/                   # 多应用拆分（如用户服务、订单服务）
│   ├── user/               # 用户应用（包含自己的 api/models/crud）
│   ├── order/              # 订单应用
│   └── payment/            # 支付应用
├── common/                 # 公共模块（跨应用复用）
│   ├── config/
│   ├── db/
│   └── utils/
├── gateway/                # API 网关（统一路由、鉴权）
├── scripts/                # 脚本（数据初始化、定时任务等）
├── tests/
└── ...（其他配置文件）
一键获取完整项目代码cmd12345678910111213
```

#### 8.3.关键目录 / 文件详解

##### 8.3.1. `app/core/`：核心配置

- `config.py`：用 `pydantic-settings` 管理环境变量，示例：

    ```python
    from pydantic_settings import BaseSettings, SettingsConfigDict
    
    class Settings(BaseSettings):
        API_V1_STR: str = "/api/v1"
        DB_URL: str = "sqlite:///./test.db"
        SECRET_KEY: str = "your-secret-key"
        ACCESS_TOKEN_EXPIRE_MINUTES: int = 30
    
        model_config = SettingsConfigDict(env_file=".env")
    
    settings = Settings()
    一键获取完整项目代码python1234567891011
    ```

- `dependencies.py`：全局依赖（如获取当前用户、数据库会话）

- `middleware.py`：全局中间件（如日志、跨域）

##### 8.3.2. `app/api/`：路由管理

- 按功能模块拆分路由（如 `users.py` / `items.py`），并在 `v1/__init__.py` 中汇总：

    ```python
    # app/api/v1/__init__.py
    from fastapi import APIRouter
    from app.api.v1 import items, users
    
    api_router = APIRouter()
    api_router.include_router(users.router, prefix="/users", tags=["users"])
    api_router.include_router(items.router, prefix="/items", tags=["items"])
    一键获取完整项目代码python1234567
    ```

- 在 `app/main.py` 中注册路由：

    ```python
    from fastapi import FastAPI
    from app.api.v1 import api_router
    from app.core.config import settings
    
    app = FastAPI(title="My API")
    app.include_router(api_router, prefix=settings.API_V1_STR)
    一键获取完整项目代码python123456
    ```

##### 8.3.3. `app/models/` vs `app/schemas/`

- `models/`：数据库表映射（ORM 模型），只和数据库交互；

- `schemas/`：接口的请求 / 响应数据模型（Pydantic），用于数据校验和序列化，示例：

    ```python
    # app/schemas/user.py
    from pydantic import BaseModel, EmailStr
    from datetime import datetime
    
    # 请求模型（创建用户）
    class UserCreate(BaseModel):
        username: str
        email: EmailStr
        password: str
    
    # 响应模型（返回用户信息）
    class UserResponse(BaseModel):
        id: int
        username: str
        email: EmailStr
        create_time: datetime
    
        class Config:
            orm_mode = True  # 支持从ORM模型转换
    一键获取完整项目代码python12345678910111213141516171819
    ```

##### 8.3.4. `app/crud/`：数据库操作封装

- 抽离 CRUD 逻辑，避免路由函数中写大量数据库操作，示例：

    ```python
    # app/crud/crud_user.py
    from sqlalchemy.orm import Session
    from app.models.user import User
    from app.schemas.user import UserCreate
    from app.utils.security import get_password_hash
    
    def create_user(db: Session, user: UserCreate):
        hashed_password = get_password_hash(user.password)
        db_user = User(
            username=user.username,
            email=user.email,
            hashed_password=hashed_password
        )
        db.add(db_user)
        db.commit()
        db.refresh(db_user)
        return db_user
    
    def get_user_by_email(db: Session, email: str):
        return db.query(User).filter(User.email == email).first()
    一键获取完整项目代码python1234567891011121314151617181920
    ```

#### 8.4.开发 / 部署建议

1. **环境隔离**：用 `.env`/`.env.prod` 区分开发 / 生产环境，不要把敏感信息（如数据库密码）硬编码；

2. **依赖管理**：`requirements.txt` 只放生产依赖，`requirements-dev.txt` 放 `pytest`、`black` 等开发工具；

3. **数据库迁移**：用 Alembic 管理数据库表结构变更，避免手动改表；

4. **测试**：`tests/` 目录按接口模块划分，用 `pytest` 编写测试用例，保证接口稳定性；

5. **启动方式**：生产环境用 `uvicorn` 加进程管理（如 `gunicorn`），示例：

    ```bash
    # 开发环境
    uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
    
    # 生产环境
    gunicorn app.main:app -w 4 -k uvicorn.workers.UvicornWorker --bind 0.0.0.0:8000
    一键获取完整项目代码bash12345
    ```

    极少数情况下 `Ctrl + C` 没反应（比如服务卡死），可以：

    - 在 PyCharm 终端中输入 `taskkill /f /im python.exe`（Windows）或 `pkill -f uvicorn`（Mac/Linux），强制终止 Python 进程；
    - 或打开系统任务管理器（Windows）/ 活动监视器（Mac），结束 Python 相关进程。

## 四、框架推荐

### 1.全功能脚手架

#### 1.1.FastAPI 官方推荐模板（最基础）

- **地址**：<https://github.com/tiangolo/full-stack-fastapi-template>
- 核心特点：
  - 官方维护，严格遵循 FastAPI 最佳实践；
  - 内置：SQLAlchemy 2.0（异步）、Pydantic 2.x、JWT 认证、依赖注入、数据库迁移（Alembic）；
  - 包含前端（Vue3 + Vite）、Docker 部署、测试用例；
  - 结构清晰：拆分 `api/v1`、`models`、`schemas`、`crud`、`core` 等目录（和之前讲的标准化结构一致）。
- **适用场景**：从零搭建标准化 FastAPI 项目，不想过度封装。

#### 1.2.FastAPI Admin（后台管理面板）

- **地址**：<https://github.com/fastapi-admin/fastapi-admin>
- 核心特点：
  - 对标「若依」的后台管理功能，内置 CRUD 生成、权限管理、数据可视化；
  - 基于 Vue3 + Element Plus 前端，无需写前端代码；
  - 支持多种数据库（MySQL/PostgreSQL/SQLite）、自定义表单 / 操作；
  - 内置：JWT 认证、角色权限、数据导出、日志管理。
- **适用场景**：快速搭建后台管理系统，需要可视化操作数据库。

#### 1.3.FastAPI-Base（企业级后台脚手架）

- **地址**：<https://github.com/ycd/manabie-fastapi>
- 核心特点：
  - 企业级封装，内置：
    - 认证：JWT + OAuth2、刷新令牌、密码加密；
    - 权限：RBAC 角色权限、接口级权限控制；
    - 工具：日志、异常统一处理、接口文档、限流、缓存；
    - 部署：Docker + Nginx + Gunicorn 配置；
  - 配套前端模板（React/Element UI）。
- **适用场景**：开发生产级后台系统，需要完善的权限 / 安全 / 部署能力。

### 2.选型建议（对标若依框架）

如果你的需求是「像若依一样的全栈后台管理系统」，优先选：

1. **FastAPI Admin**：可视化后台面板，前端开箱即用；
2. **FastAPI-Base**：企业级封装，权限 / 部署更完善；
3. 基础模板 + FastAPI CRUD Router：自定义程度高，灵活扩展。

### 3.使用建议

1. **轻量需求**：用官方 `full-stack-fastapi-template` 初始化项目，自己扩展权限 / 业务；
2. **快速后台**：直接用 `FastAPI Admin`，5 分钟搭建可视化后台；
3. **企业级需求**：基于 `FastAPI-Base` 二次开发，补充业务模块。

## 五、项目实战

### 1.准备工作

#### 1.1.项目介绍

这是一个仿今日头条的新闻系统后端API服务，采用异步Python框架FastAPI开发，使用MySQL作为数据库存储，通过SQLAlchemy ORM进行数据访问。系统提供完整的用户管理、新闻浏览、收藏和历史记录功能。

- **后端框架**: FastAPI
- **数据库**: MySQL
- **ORM**: SQLAlchemy (异步)
- **数据库驱动**: aiomysql
- **密码加密**: passlib + bcrypt
- **缓存系统**: Redis
- **异步支持**: Python asyncio

#### 1.2.目录结构

创建好FastAPI项目后，目录结构如下:

```cmd
D:\Workspaces\python\test\Project1
│   .gitignore                  # Git忽略规则文件（配置无需提交的文件/目录，如__pycache__、venv等）
│   requirements.txt            # 项目依赖清单（记录所有第三方包，如fastapi、uvicorn、sqlalchemy等）
│
├───app                         # 项目核心应用目录（FastAPI 主程序入口+业务逻辑）
│   │   clean_pycache.py        # Python缓存清理脚本（批量删除项目中所有__pycache__目录）
│   │   main.py                 # FastAPI 入口文件（创建app实例、注册路由、挂载中间件/异常处理器等）
│   │   __init__.py             # 标记app为Python包（使子模块可被导入）
│   │
│   ├───api                     # API接口层（统一管理接口路由、请求/响应处理）
│   │   │   endpoints.py        # 接口入口汇总（可选：统一导入所有routers并注册到app）
│   │   │   __init__.py         # 标记api为Python包
│   │   │
│   │   └───routers             # 路由拆分目录（按业务模块拆分接口，符合RESTful规范）
│   │           favorite.py     # 收藏相关接口（如新增收藏、删除收藏、查询收藏列表）
│   │           history.py      # 历史记录相关接口（如查询浏览历史、清空历史）
│   │           news.py         # 新闻相关接口（如获取新闻列表、新闻详情、新增/编辑新闻）
│   │           users.py        # 用户相关接口（如登录、注册、修改密码、获取用户信息）
│   │           __init__.py     # 标记routers为Python包
│   │
│   ├───cache                   # 缓存层（封装缓存相关逻辑，如Redis操作封装）
│   │       news.py             # 新闻缓存逻辑（如新闻列表缓存、新闻详情缓存的增删改查）
│   │       __init__.py         # 标记cache为Python包
│   │
│   ├───core                    # 核心配置层（项目全局配置、基础组件）
│   │   │   __init__.py         # 标记core为Python包
│   │   │
│   │   ├───config              # 配置管理目录（全局配置项、日志配置等）
│   │   │       logging_config.py # 日志配置文件（定义日志格式、存储路径、清理规则等）
│   │   │       settings.py     # 项目核心配置（如数据库地址、Redis地址、JWT密钥、跨域配置等）
│   │   │       __init__.py     # 标记config为Python包
│   │   │
│   │   ├───exception           # 异常处理目录（自定义异常、全局异常处理器）
│   │   │       error_code.py   # 错误码定义（如业务错误码、HTTP状态码映射）
│   │   │       exceptions.py   # 自定义异常类（如BusinessException、ValidationException等）
│   │   │       handlers.py     # 全局异常处理器（统一捕获并处理各类异常，返回标准化响应）
│   │   │       __init__.py     # 标记exception为Python包
│   │   │
│   │   ├───middleware          # 中间件目录（自定义FastAPI中间件）
│   │   │       access_log.py   # 访问日志中间件（记录所有接口的请求/响应日志）
│   │   │       cors.py         # 跨域中间件（配置CORS规则，允许前端跨域请求）
│   │   │       __init__.py     # 标记middleware为Python包
│   │   │
│   │   └───response            # 响应格式化目录（统一接口响应格式）
│   │           models.py       # 响应模型（定义标准化响应体，如SuccessResponse、FailResponse）
│   │           utils.py        # 响应工具函数（如封装success/fail函数，快速返回标准化响应）
│   │           __init__.py     # 标记response为Python包
│   │
│   ├───crud                    # 数据操作层（封装数据库CRUD逻辑，与models对应）
│   │       favorite.py         # 收藏数据操作（如新增收藏到数据库、查询用户收藏）
│   │       history.py          # 历史记录数据操作（如新增浏览历史、删除历史记录）
│   │       news.py             # 新闻数据操作（如查询新闻、新增新闻、更新新闻状态）
│   │       news_cache.py       # 新闻缓存+数据库联动操作（如先查缓存，缓存失效查数据库）
│   │       users.py            # 用户数据操作（如查询用户、创建用户、修改用户密码）
│   │       __init__.py         # 标记crud为Python包
│   │
│   ├───db                      # 数据库连接层（封装数据库/Redis连接）
│   │       redis_client.py     # Redis连接封装（创建Redis客户端、封装常用Redis操作）
│   │       session.py          # 数据库会话封装（如SQLAlchemy的Session创建、数据库连接池配置）
│   │       __init__.py         # 标记db为Python包
│   │
│   ├───helper                  # 业务辅助层（封装通用业务逻辑，解耦路由与核心逻辑）
│   │       auth.py             # 认证辅助逻辑（如JWT生成/解析、权限校验、密码加密）
│   │       favorite.py         # 收藏业务逻辑（如收藏权限校验、收藏去重逻辑）
│   │       history.py          # 历史记录业务逻辑（如历史记录去重、过期清理）
│   │       news.py             # 新闻业务逻辑（如新闻过滤、排序、权限校验）
│   │       users.py            # 用户业务逻辑（如用户注册校验、密码复杂度校验）
│   │       __init__.py         # 标记helper为Python包
│   │
│   ├───models                  # 数据模型层（数据库表结构映射，如SQLAlchemy模型）
│   │       favorite.py         # 收藏模型（映射收藏表，定义字段、关联关系）
│   │       history.py          # 历史记录模型（映射历史记录表，定义字段）
│   │       news.py             # 新闻模型（映射新闻表，定义标题、内容、发布时间等字段）
│   │       users.py            # 用户模型（映射用户表，定义用户名、密码、邮箱等字段）
│   │       __init__.py         # 标记models为Python包
│   │
│   ├───schemas                 # 数据校验层（Pydantic模型，校验请求/响应数据）
│   │       favorite.py         # 收藏相关校验模型（如新增收藏的请求体、收藏列表响应体）
│   │       history.py          # 历史记录校验模型（如查询历史的参数、清空历史的请求体）
│   │       news.py             # 新闻相关校验模型（如新增新闻的请求体、新闻详情响应体）
│   │       users.py            # 用户相关校验模型（如登录请求体、注册请求体、修改密码请求体）
│   │       __init__.py         # 标记schemas为Python包
│   │
│   └───utils                   # 通用工具层（项目通用工具函数，与业务无关）
│           security.py         # 安全相关工具（如密码哈希、随机字符串生成、数据加密/解密）
│           __init__.py         # 标记utils为Python包
│
└───tests                       # 测试目录（接口测试、单元测试）
        test_main.http          # HTTP测试文件（PyCharm/VSCode可直接运行，测试接口请求）
        __init__.py             # 标记tests为Python包
一键获取完整项目代码cmd123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263646566676869707172737475767778798081828384858687888990
```

#### 1.3.安装依赖

完整的 requirements.txt:

```cmd
# 核心 Web 框架
fastapi==0.133.1
# ASGI 框架
starlette~=0.50.0
# 数据验证
pydantic==2.12.5
pydantic-settings~=2.13.1
# ASGI 服务器
uvicorn==0.41.0
# ORM 框架
sqlalchemy==2.0.47
# 异步 MySQL 驱动
aiomysql==0.3.2
# 密码验证
passlib==1.7.4
# 密码加密
bcrypt~=4.3.0
# Redis
redis==7.3.0
# 清理工具
pyclean==3.5.0
一键获取完整项目代码cmd123456789101112131415161718192021
```

安装依赖:

```cmd
# 升级 pip 到最新版
python -m pip install --upgrade pip

# 安装 requirements.txt 中的依赖
python -m pip install -r requirements.txt --encoding=utf-8

# 国内安装加速
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
一键获取完整项目代码cmd12345678
```

版本兼容性:

PyPI（Python 包索引）是所有第三方库的发布平台，每个库的页面都会标注支持的 Python 版本。

1. 打开目标库的 PyPI 页面：
    - FastAPI：<https://pypi.org/project/fastapi/>
    - uvicorn：<https://pypi.org/project/uvicorn/>
    - SQLAlchemy：<https://pypi.org/project/SQLAlchemy/>
    - aiomysql：<https://pypi.org/project/aiomysql/>
    - passlib：<https://pypi.org/project/passlib/>
2. 找到「Python Versions」区域（通常在页面下方）：
    - 示例：FastAPI 的 PyPI 页面会显示「Python :: 3.8 | 3.9 | … | 3.13」，表示支持这些版本。
    - 若想查看特定版本的支持情况，可点击页面上的「Release history」，选择对应版本后查看其「Metadata」中的 Python 版本约束。

#### 1.4.导入数据库

```sql
mysql> source D:\Downloads\database.sql;
mysql> show tables;
+--------------------+
| Tables_in_news_app |
+--------------------+
| ai_chat            |
| favorite           |
| history            |
| news               |
| news_category      |
| related_news       |
| user               |
| user_token         |
+--------------------+
8 rows in set (0.00 sec)
一键获取完整项目代码sql123456789101112131415
```

1. **用户表 (user)**
    - 用户基本信息存储
    - 包含用户名、密码(加密)、昵称、头像等字段
2. **用户令牌表 (user_token)**
    - 用户认证令牌管理
    - 支持令牌过期机制
3. **新闻分类表 (news_category)**
    - 新闻分类信息
4. **新闻表 (news)**
    - 新闻内容存储
    - 包含标题、内容、作者、浏览量等字段
5. **收藏表 (favorite)**
    - 用户收藏记录
    - 关联用户和新闻
6. **浏览历史表 (history)**
    - 用户浏览历史记录
    - 关联用户和新闻

#### 1.5.运行前端项目

```cmd
# 进入项目根目录（确保有 package.json 文件）
cd /d D:\Downloads\news

# 安装所有依赖（包括 vite）
npm install
# 如果没有 vite 依赖，手动安装并保存到开发依赖
npm install vite --save-dev

# 执行 dev 脚本
npm run dev
一键获取完整项目代码cmd12345678910
```

- `/d`：关键参数，作用是**同时切换驱动器和目录**

如果运行失败，则执行以下步骤:

1. 彻底清理依赖（关键）

先删除损坏的依赖文件：

```bash
# 删除 node_modules 文件夹
rmdir /s /q node_modules

# 删除 package-lock.json 文件
del package-lock.json
一键获取完整项目代码bash12345
```

1. 重新安装依赖

```bash
# 重新安装所有依赖
npm install

# 如果网络慢，用淘宝镜像
npm install --registry=https://registry.npmmirror.com
一键获取完整项目代码bash12345
```

1. 验证修复

```bash
npm run dev
一键获取完整项目代码bash1
```

### 2.统一认证鉴权

系统使用基于令牌(Token)的认证机制：

1. 用户登录成功后返回访问令牌
2. 需要认证的接口在请求头中添加 `Authorization: token值`
3. 令牌有效期为7天

#### 2.1.用户登录路由

```python
@router.post("/login")
async def user_login(dto: UserDTO, db: AsyncSession = Depends(get_db)):
    """
    用户登录
    """

    # 1. 检查用户是否存在
    user = await users.get_user_by_username(db, dto.username)
    if not user:
        raise UserNotExistException()  # 触发「用户不存在」异常

    # 2. 校验密码
    if not security.verify_password(dto.password, user.password):
        raise PasswordErrorException()  # 触发「密码错误」异常

    # 3. 登录成功，获取用户 Token
    token = await users.get_token(db, user.id)
    if not token:
        # raise BusinessException(code=status.HTTP_500_INTERNAL_SERVER_ERROR, message="未生成 Token")  # 抛出自定义业务异常
        raise_business_error("未生成 Token")  # 通用的抛出函数

    # 4. 返回用户信息
    vo = to_user_auth_vo(user, token)

    # 5. 调用成功函数，自动封装统一格式
    # return success(data=vo, message="登录成功")
    return success(vo, "登录成功")


@router.get("/info")
async def user_info(user: User = Depends(get_current_user)):
    """
    获取用户信息
    """

    # 1. 获取用户信息
    vo = to_user_info_vo(user)

    # 2. 调用成功函数，自动封装统一格式
    return success(data=vo, message="获取用户信息成功")
一键获取完整项目代码python12345678910111213141516171819202122232425262728293031323334353637383940
```

#### 2.2.创建并获取Token

```python
async def get_token(db: AsyncSession, user_id: int) -> str:
    """
    创建用户 Token
    :param db: 数据库会话
    :param user_id: 用户ID
    :return:
    """

    # 查询数据库当前用户是否有 Token, 调用 async 函数时使用 await
    user_token = await get_token_by_userid(db, user_id)

    # 判断是否有 Token
    if user_token:
        # 有 Token，判断 Token 是否过期
        if user_token.expires_at > datetime.now():
            # Token 未过期，返回 Token
            return user_token.token
        else:
            # Token 过期，删除 Token
            await db.delete(user_token)  # 必须加 await，核心原因是：它们都是异步操作（协程），需要等待数据库完成操作后，才能继续执行后续逻辑。
            await db.commit()

    # 重新生成 Token
    token = str(uuid.uuid4())
    # 设置 Token 过期时间: 7 天
    expires_at = datetime.now() + timedelta(days=7)
    # 创建用户 Token
    user_token = UserToken(user_id=user_id, token=token, expires_at=expires_at)
    db.add(user_token)
    await db.commit()  # 必须加 await，否则报: 未等待协程 'commit'
    await db.refresh(user_token)
    return token
一键获取完整项目代码python1234567891011121314151617181920212223242526272829303132
```

#### 2.3.验证当前用户

```python
async def get_current_user(
        authorization: str = Header(..., alias="Authorization"),
        db: AsyncSession = Depends(get_db)) -> User:
    """
    获取当前用户
    """

    # 获取用户 Token
    token = authorization
    if authorization.startswith("Bearer "):
        token = authorization.split(" ")[1]

    # 通过 Token 获取用户信息
    user = await users.get_user_by_token(db, token)

    # 判断用户是否存在
    if not user:
        raise TokenErrorException()

    return user
一键获取完整项目代码python1234567891011121314151617181920
```

### 3.统一返回

接口返回统一的 JSON 格式

#### 3.1.定义通用响应模型

```python
"""
模块名称：定义通用响应模型
功能描述：用 Pydantic 模型规范所有接口的返回格式（如 code/message/data 结构）
"""

from typing import Generic, TypeVar, Optional

from pydantic import BaseModel

# 泛型类型，支持任意数据类型的 data 字段
T = TypeVar("T")


class BaseResponse(BaseModel, Generic[T]):
    """通用响应模型（所有接口返回格式统一）"""
    # 状态码（200=成功，其他=失败）
    code: int
    # 提示信息
    message: str
    # 业务数据（可选，支持任意类型）
    data: Optional[T] = None

    class Config:
        # 支持 ORM 对象序列化（如 SQLAlchemy 模型）
        from_attributes = True


# 带数据的成功响应（泛型）
DataResponse = BaseResponse[T]


# 无数据返回的成功响应
class SuccessResponse(BaseModel):
    code: int
    message: str
    data: None = None


# 失败响应（通常无数据）
class ErrorResponse(BaseModel):
    code: int
    message: str
    data: None = None

一键获取完整项目代码python1234567891011121314151617181920212223242526272829303132333435363738394041424344
```

#### 3.2.封装返回工具函数

```python
"""
模块名称：封装返回工具函数
功能描述：提供快捷函数（如 success()/fail()），一键生成符合模型的响应对象
"""

from typing import Any, Optional

from starlette import status

from app.core.response.models import BaseResponse


def success(
        data: Optional[Any] = None,
        message: str = "操作成功",
        code: int = status.HTTP_200_OK
) -> BaseResponse:
    """
    成功响应快捷函数
    :param data: 业务数据（可选）
    :param message: 提示信息（默认“操作成功”）
    :param code: 状态码（默认200）
    :return: 统一响应对象
    """
    return BaseResponse(
        code=code,
        message=message,
        data=data
    )


def fail(
        message: str = "操作失败",
        code: int = status.HTTP_400_BAD_REQUEST,
        data: Optional[Any] = None
) -> BaseResponse:
    """
    失败响应快捷函数
    :param message: 错误提示
    :param code: 错误码（默认400）
    :param data: 错误附加数据（可选）
    :return: 统一响应对象
    """
    return BaseResponse(
        code=code,
        message=message,
        data=data
    )

一键获取完整项目代码python12345678910111213141516171819202122232425262728293031323334353637383940414243444546474849
```

#### 3.3.使用统一返回函数

```python
@router.post("/register")
async def user_register(dto: UserDTO, db: AsyncSession = Depends(get_db)):
    """
    用户注册
    """

    # 1. 通过用户名查询用户信息
    exist_user = await users.get_user_by_username(db, dto.username)
    if exist_user:
        raise UserExistException()  # 抛出自定义异常

    # 2. 创建用户
    user = await users.create_user(db, dto)

    # 3. 获取用户 Token
    token = await users.get_token(db, user.id)

    # 4. 返回用户信息
    vo = to_user_auth_vo(user, token)

    # 5. 调用成功函数，自动封装统一格式
    return success(data=vo, message="注册成功")
一键获取完整项目代码python12345678910111213141516171819202122
```

### 4.统一异常处理

系统提供统一的错误处理机制：

- 用户认证失败返回 401 状态码
- 资源不存在返回 404 状态码
- 服务器内部错误返回 500 状态码

#### 4.1.统一的异常码

```python
"""
模块名称：全局统一的异常码
功能描述：
    1. 定义项目全局统一的异常码体系，包含通用异常码和业务异常码；
    2. 异常码规则：HTTP状态码+业务细分码（如40001=400+01），便于前端识别；
    3. 提供通用业务异常类，关联异常码和提示信息。
"""
from enum import Enum

from fastapi import status


class ErrorCode(Enum):
    """
    异常码枚举类：
    - 格式：(业务码, 提示信息, HTTP状态码)
    - 通用异常码：10001-99999
    - 业务异常码：按模块划分（如用户模块50001+，订单模块60001+）
    """
    # ===================== 通用异常（1xxxx） =====================
    SUCCESS = (0, "操作成功", status.HTTP_200_OK)
    FAILURE = (1, "操作失败", status.HTTP_500_INTERNAL_SERVER_ERROR)
    PARAM_ERROR = (40001, "参数校验失败", status.HTTP_400_BAD_REQUEST)
    TOKEN_INVALID = (40101, "Token无效或已过期", status.HTTP_401_UNAUTHORIZED)
    PERMISSION_DENY = (40301, "无操作权限", status.HTTP_403_FORBIDDEN)
    RESOURCE_NOT_FOUND = (40401, "请求资源不存在", status.HTTP_404_NOT_FOUND)
    SERVER_ERROR = (50001, "服务器内部错误", status.HTTP_500_INTERNAL_SERVER_ERROR)

    # ===================== 业务异常 - 用户模块（5xxxx） =====================
    USER_EXIST = (50001, "用户名已存在，无法注册", status.HTTP_400_BAD_REQUEST)
    USER_NOT_EXIST = (50002, "用户不存在，请检查用户ID", status.HTTP_404_NOT_FOUND)
    USER_PASSWORD_ERROR = (50003, "密码错误，请重新输入", status.HTTP_400_BAD_REQUEST)

    # ===================== 业务异常 - 订单模块（6xxxx） =====================
    ORDER_NOT_FOUND = (60001, "订单不存在", status.HTTP_404_NOT_FOUND)
    ORDER_STATUS_ERROR = (60002, "订单状态异常，无法操作", status.HTTP_400_BAD_REQUEST)

一键获取完整项目代码python12345678910111213141516171819202122232425262728293031323334353637
```

#### 4.2.创建自定义异常

```python
"""
模块名称：自定义异常
功能描述：如果有自定义业务异常，也放在这个目录下，保持结构统一
"""
from starlette import status

from app.core.exception.error_code import ErrorCode


class BusinessException(Exception):
    """通用业务异常类：关联异常码、提示信息、HTTP状态码
    支持两种入参方式：
    1. 传入 ErrorCode 枚举（推荐）：自动解析业务码、默认提示信息
    2. 传入字符串/数字型业务码：自定义业务码和提示信息
    """

    def __init__(self, code: ErrorCode | str | int, message: str = None):
        # 初始化HTTP状态码（默认500）
        self.status_code = status.HTTP_500_INTERNAL_SERVER_ERROR

        # 条件1：传入的是 ErrorCode 枚举类型
        if isinstance(code, ErrorCode):
            self.code = code.value[0]  # 提取枚举中的业务码
            # 优先用自定义message，否则用枚举默认提示
            self.message = message or code.value[1]
            # 提取枚举中的HTTP状态码
            self.status_code = code.value[2]

        # 条件2：传入的是字符串/数字型业务码
        elif isinstance(code, (str, int)):
            self.code = code  # 直接使用自定义业务码
            self.message = message or "业务异常"  # 无自定义message则用默认提示

        # 非法入参：抛出明确错误，便于调试
        else:
            raise TypeError(f"code参数仅支持 ErrorCode 枚举、字符串、数字类型，当前类型：{type(code)}")

        # 保留原生Exception的message属性
        super().__init__(self.message)


class ParamErrorException(BusinessException):
    """参数错误（动态提示）"""

    def __init__(self):
        super().__init__(code=ErrorCode.PARAM_ERROR)


# 具体业务异常（按需定义）
class UserExistException(BusinessException):
    """用户已存在异常"""

    def __init__(self):
        super().__init__(code=ErrorCode.USER_EXIST)


class UserNotExistException(BusinessException):
    """用户不存在异常"""

    def __init__(self):
        super().__init__(code=ErrorCode.USER_NOT_EXIST)


class TokenErrorException(BusinessException):
    """"无效的令牌或令牌已过期"""

    def __init__(self):
        super().__init__(code=ErrorCode.TOKEN_INVALID)


class PasswordErrorException(BusinessException):
    """密码错误异常"""

    def __init__(self):
        super().__init__(code=ErrorCode.USER_PASSWORD_ERROR)


# 通用抛出函数
def raise_business_exception(message: str = None, code: ErrorCode | int = None):
    """
    抛出业务异常（兼容两种调用方式）：
    方式1：传入 ErrorCode 枚举（优先推荐）
        raise_business_exception(ErrorCode.USER_NOT_EXIST)
        raise_business_exception(ErrorCode.USER_PASSWORD_ERROR, "密码错误，请重试")
    方式2：传入 业务码+提示信息（兼容自定义场景）
        raise_business_exception(40001, "参数格式错误")
        raise_business_exception(code=50001, message="服务器内部错误")
    """
    # 场景1：第一个参数是 ErrorCode 枚举（优先处理）
    if isinstance(code, ErrorCode):
        raise BusinessException(code, message)

    # 场景2：传入 业务码（int）+ 提示信息（兼容原有逻辑）
    elif isinstance(code, int):
        # 若只传message、不传code（如 raise_business_exception(message="xxx")）
        if code is None and message is not None:
            code = status.HTTP_500_INTERNAL_SERVER_ERROR
        raise BusinessException(code, message)

    # 场景3：仅传message（简化调用）
    elif code is None and message is not None:
        raise BusinessException(status.HTTP_500_INTERNAL_SERVER_ERROR, message)

    # 非法入参防护
    else:
        raise TypeError("入参错误！支持：1.ErrorCode枚举 2.业务码(int)+提示信息(str)")


# 专属场景函数
def raise_bad_request(message: str):
    """抛出400错误（参数/业务逻辑错误）"""
    # 场景：参数格式错误、必传参数缺失、业务逻辑不合法（如提现金额超余额）
    raise_business_exception(message=message, code=status.HTTP_400_BAD_REQUEST)


def raise_unauthorized(message: str):
    """抛出401错误（未授权/Token过期）"""
    # 场景：无Token、Token过期/无效、未登录访问需授权接口
    raise_business_exception(message=message, code=status.HTTP_401_UNAUTHORIZED)


def raise_forbidden(message: str):
    """抛出403错误（权限不足）"""
    # 场景：普通用户访问管理员接口、无权限操作他人资源、账号被封禁
    raise_business_exception(message=message, code=status.HTTP_403_FORBIDDEN)


def raise_not_found(message: str):
    """抛出404错误（资源不存在）"""
    # 场景：查询的用户/商品/订单ID不存在、访问不存在的接口路径
    raise_business_exception(message=message, code=status.HTTP_404_NOT_FOUND)


def raise_unprocessable_entity(message: str):
    """抛出422错误（数据验证错误）"""
    # 场景：参数格式正确但规则不符（如密码复杂度不够、开始时间大于结束时间）
    raise_business_exception(message=message, code=status.HTTP_422_UNPROCESSABLE_ENTITY)


def raise_conflict(message: str):
    """抛出409错误（资源冲突：如重复创建、唯一键冲突）"""
    # 场景：创建用户时手机号已存在、提交重复订单、修改已锁定的资源
    raise_business_exception(message=message, code=status.HTTP_409_CONFLICT)


def raise_gone(message: str):
    """抛出410错误（资源永久删除：如已注销的账号、已下架的商品）"""
    # 场景：访问已被永久删除的用户资料、已下架且不再恢复的商品
    raise_business_exception(message=message, code=status.HTTP_410_GONE)


def raise_internal_server_error(message: str = "服务器内部错误"):
    """抛出500错误（服务端内部错误：如数据库连接失败、代码逻辑异常）"""
    # 场景：数据库查询报错、第三方服务调用失败、代码未捕获的异常
    raise_business_exception(message=message, code=status.HTTP_500_INTERNAL_SERVER_ERROR)


def raise_not_implemented(message: str = "接口暂未实现"):
    """抛出501错误（接口未实现：如规划中的接口、暂未开发的功能）"""
    # 场景：前端调用了后端还未开发的接口、功能迭代中临时占位
    raise_business_exception(message=message, code=status.HTTP_501_NOT_IMPLEMENTED)


def raise_bad_gateway(message: str = "网关错误：依赖服务不可用"):
    """抛出502错误（网关错误：如调用第三方服务失败、微服务依赖不可用）"""
    # 场景：调用支付接口超时、依赖的用户服务宕机、缓存服务连接失败
    raise_business_exception(message=message, code=status.HTTP_502_BAD_GATEWAY)


def raise_service_unavailable(message: str = "服务暂不可用，请稍后重试"):
    """抛出503错误（服务不可用：如系统维护、服务过载）"""
    # 场景：系统升级维护中、服务器负载过高暂时拒绝请求、数据库主从切换
    raise_business_exception(message=message, code=status.HTTP_503_SERVICE_UNAVAILABLE)


def raise_gateway_timeout(message: str = "网关超时：依赖服务响应过慢"):
    """抛出504错误（网关超时：如调用第三方服务超时、微服务响应超时）"""
    # 场景：调用物流接口超过30秒未响应、数据库查询超时、Redis连接超时
    raise_business_exception(message=message, code=status.HTTP_504_GATEWAY_TIMEOUT)

一键获取完整项目代码python123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263646566676869707172737475767778798081828384858687888990919293949596979899100101102103104105106107108109110111112113114115116117118119120121122123124125126127128129130131132133134135136137138139140141142143144145146147148149150151152153154155156157158159160161162163164165166167168169170171172173174175176177178179180
```

#### 4.3.创建异常处理器

```python
"""
模块名称：异常处理器
功能描述：把所有异常处理器逻辑集中放在这里，对外暴露一个「注册异常处理器」的函数
"""
import traceback
from typing import Dict, List

from fastapi import HTTPException, Request
from fastapi.exceptions import RequestValidationError
from fastapi.responses import JSONResponse
from sqlalchemy.exc import IntegrityError, SQLAlchemyError
from starlette import status

from app.core.config.settings import settings
from app.core.exception.exceptions import BusinessException
from app.core.response.utils import fail


def register_exception_handlers(app):
    """
    注册所有全局异常处理器到 FastAPI 应用实例
    :param app: FastAPI 应用实例
    """

    @app.exception_handler(BusinessException)
    async def business_exception_handler(request: Request, exc: BusinessException):
        """
        处理自定义业务异常
        :param request: 请求对象
        :param exc: 异常对象
        :return: 响应对象
        """
        return JSONResponse(
            status_code=exc.status_code,  # 标准 HTTP 码
            content=fail(code=exc.code, message=exc.message).model_dump()
        )

    @app.exception_handler(HTTPException)
    async def http_exception_handler(request: Request, exc: HTTPException):
        """
        处理 FastAPI 内置 HTTPException
        :param request: 请求对象
        :param exc: 异常对象
        :return: 响应对象
        """
        return JSONResponse(
            status_code=exc.status_code,
            content=fail(code=exc.status_code, message=exc.detail).model_dump()
        )

    @app.exception_handler(RequestValidationError)
    async def validation_exception_handler(request: Request, exc: RequestValidationError):
        """
        处理参数校验异常
        :param request: 请求对象
        :param exc: 异常对象
        :return: 响应对象
        触发示例
        class UserRegisterDTO(BaseModel):
            username: str = Field(..., min_length=3, max_length=20, description="用户名，3-20字符")
            password: str = Field(..., min_length=6, description="密码，至少6字符")
            email: EmailStr = Field(..., description="邮箱，格式必须合法")
        """
        # return JSONResponse(
        #     status_code=422,
        #     content=fail(code=422, message=f"参数校验失败：{exc.errors()}").model_dump()
        # )
        # 返回统一格式
        # {
        #     "code": 422,
        #     "message": "参数校验失败：[{'type': 'string_too_long', 'loc': ('body', 'username'), 'msg': 'String should have at most 5 characters', 'input': 'bbbbbb', 'ctx': {'max_length': 5}}]",
        #     "data": null
        # }

        # 1. 解析原生错误信息，提取关键内容
        error_details: List[Dict] = []
        simple_msg: str = ""
        for err in exc.errors():
            # 打印错误信息
            print(f"参数校验错误：{err}")
            # err 结构示例：
            # 自定义 ValueError 提示:
            # {'type': 'value_error', 'loc': ('body', 'newPassword'), 'msg': 'Value error, 新密码必须是6位数字', 'input': '11', 'ctx': {'error': ValueError('新密码必须是6位数字')}}
            # Pydantic 原生错误提示:
            # {'type': 'string_too_short', 'loc': ('body', 'newPassword'), 'msg': 'String should have at least 6 characters', 'input': '11', 'ctx': {'min_length': 6}}

            # 1. 提取字段名（兼容原生loc和自定义字段）
            if "loc" in err:
                field = ".".join(map(str, err["loc"]))
            else:
                field = "unknown"

            # 2. 优先解析自定义 ValueError 提示（核心修改）
            if "ctx" in err and "error" in err["ctx"] and hasattr(err["ctx"]["error"], "args"):
                # 提取 ValueError 的自定义提示信息
                message = err["ctx"]["error"].args[0]
            # 3. 解析 Pydantic 原生错误提示（兜底）
            else:
                message = err["msg"]

            # 4. 构建错误详情（关键：将解析后的提示存入）
            error_details.append({
                "field": field,  # 错误字段（如 body.password、query.username）
                "message": message,  # 错误提示
                "type": err["type"]  # 错误类型（可选，供前端定位问题）
            })

        # 2. 构造最终友好提示（复用 error_details 中的信息）
        # simple_msg = f"参数错误：{'; '.join([f'{item['field']}: {item['message']}' for item in error_details])}"   # 字段+错误信息
        simple_msg = f"参数错误：{'; '.join([f'{item['message']}' for item in error_details])}"  # 仅提示错误信息

        # 3. 返回统一格式（code=422 是 HTTP 标准的参数校验错误码）
        return JSONResponse(
            status_code=status.HTTP_422_UNPROCESSABLE_CONTENT,  # HTTP 状态码与业务码一致
            content=fail(
                message=simple_msg,
                code=status.HTTP_422_UNPROCESSABLE_CONTENT,
                data=error_details  # 可选：返回详细错误信息，供前端精准处理
            ).model_dump()
        )

    @app.exception_handler(IntegrityError)
    async def integrity_error_handler(request: Request, exc: IntegrityError):
        """
        处理数据库唯一索引冲突异常
        :param request: 请求对象
        :param exc: 异常对象
        :return: 响应对象
        """
        # 1. 获取错误信息
        # 错误信息示例：
        # (sqlite3.IntegrityError) UNIQUE constraint failed: users.username
        # [SQL: INSERT INTO users (username, password, email) VALUES (?, ?, ?)]
        # [parameters: ('bbbbbb', '123456', 'bbbbbb@example.com')]
        error_msg = str(exc.orig)

        # 判断具体的约束错误类型
        if "UNIQUE constraint failed" in error_msg or "Duplicate entry" in error_msg:
            message = "数据已存在，请检查输入"
        elif "FOREIGN KEY constraint failed" in error_msg:
            message = "外键约束冲突，请检查输入"
        else:
            message = "数据约束冲突，请检查输入"

        # 开发模式下返回详细错误信息
        error_data = None
        if settings.DB_DEBUG:
            error_data = {
                "error_type": type(exc).__name__,  # 错误类型
                "error_detail": str(exc),  # 错误信息
                "path": str(request.url),  # 请求路径
                "traceback": traceback.format_exc(),  # 堆栈信息，格式化异常信息为字符串，方便日志记录和调试
            }

        return JSONResponse(
            status_code=status.HTTP_400_BAD_REQUEST,
            content=fail(
                message=message,
                code=status.HTTP_400_BAD_REQUEST,
                data=error_data
            ).model_dump()
        )

    @app.exception_handler(SQLAlchemyError)
    async def sqlalchemy_error_handler(request: Request, exc: SQLAlchemyError):
        """
        处理 SQLAlchemy 异常
        :param request: 请求对象
        :param exc: 异常对象
        :return: 响应对象
        """
        # 1. 获取错误信息
        # 错误信息示例：
        # sqlalchemy.exc.OperationalError: (sqlite3.OperationalError) no such table: users
        # [SQL: SELECT users.id AS users_id, users.username AS users_username, users.password AS users_password, users.email AS users_email]

        # 开发模式下返回详细错误信息
        error_data = None
        if settings.DB_DEBUG:
            error_data = {
                "error_type": type(exc).__name__,  # 错误类型
                "error_detail": str(exc),  # 错误信息
                "path": str(request.url),  # 请求路径
                "traceback": traceback.format_exc(),  # 堆栈信息，格式化异常信息为字符串，方便日志记录和调试
            }

        return JSONResponse(
            status_code=status.HTTP_500_INTERNAL_SERVER_ERROR,
            content=fail(
                message="数据库操作异常，请检查输入",
                code=status.HTTP_500_INTERNAL_SERVER_ERROR,
                data=error_data
            ).model_dump()
        )

    @app.exception_handler(Exception)
    async def global_exception_handler(request: Request, exc: Exception):
        """
        处理全局未知异常
        :param request: 请求对象
        :param exc: 异常对象
        :return: 响应对象
        """
        # 记录异常日志
        import logging
        logging.error(f"全局未捕获异常：{exc}", exc_info=True)

        # 开发模式下返回详细错误信息
        error_data = None
        if settings.DB_DEBUG:
            error_data = {
                "error_type": type(exc).__name__,  # 错误类型
                "error_detail": str(exc),  # 错误信息
                "path": str(request.url),  # 请求路径
                "traceback": traceback.format_exc(),  # 堆栈信息，格式化异常信息为字符串，方便日志记录和调试
            }

        return JSONResponse(
            status_code=status.HTTP_500_INTERNAL_SERVER_ERROR,
            content=fail(
                code=status.HTTP_500_INTERNAL_SERVER_ERROR,
                message="服务器内部错误",
                data=error_data
            ).model_dump()
        )

一键获取完整项目代码python123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263646566676869707172737475767778798081828384858687888990919293949596979899100101102103104105106107108109110111112113114115116117118119120121122123124125126127128129130131132133134135136137138139140141142143144145146147148149150151152153154155156157158159160161162163164165166167168169170171172173174175176177178179180181182183184185186187188189190191192193194195196197198199200201202203204205206207208209210211212213214215216217218219220221222223224225226
```

#### 4.4.使用自定义异常

```python
async def update_user(db: AsyncSession, user_id: int, dto: UserUpdateDTO) -> User:
    """
    更新用户信息
    :param db: 数据库会话
    :param user_id: 用户ID
    :param dto: 用户更新信息
    :return: 用户信息
    """

    # 1. 先查询用户是否存在
    user = await db.get(User, user_id)
    if not user:
        raise_not_found(f"用户ID: {user_id} 不存在，无法更新")

    # 2. 执行更新
    for key, value in dto.model_dump(exclude_unset=True).items():
        setattr(user, key, value)

    await db.commit()
    await db.refresh(user)  # 刷新对象，获取最新数据
    return user
一键获取完整项目代码python123456789101112131415161718192021
```

### 5.统一日志

#### 5.1.日志相关参数

把日志路径、级别等参数抽离到配置文件（`core/config/settings.py`）

```python
import logging

from pydantic_settings import BaseSettings, SettingsConfigDict


# 配置文件
class Settings(BaseSettings):
    """ 项目配置 """
    # 项目名称
    PROJECT_NAME: str = "FastAPI Project"
    # 项目版本
    PROJECT_VERSION: str = "1.0.0"
    # 接口前缀
    API_PREFIX: str = "/api"
    # 服务主机
    SERVER_HOST: str = "0.0.0.0"
    # 服务端口
    SERVER_PORT: int = 8000
    # 是否热重载
    RELOAD: bool = True

    """ 数据库配置 """
    # 数据库连接字符串
    DB_URL: str = "mysql+aiomysql://root:123456@localhost:3306/news_app?charset=utf8mb4"
    # 是否调试模式
    DB_DEBUG: bool = True
    # 数据库连接池大小
    DB_POOL_SIZE: int = 10
    # 数据库连接池最大连接数
    DB_MAX_OVERFLOW: int = 20

    """ Redis配置 """
    # Redis 服务器地址
    REDIS_HOST: str = "localhost"
    # Redis 端口
    REDIS_PORT: int = 6379
    # 数据库编号（默认0）
    REDIS_DB: int = 0
    # Redis密码
    REDIS_PASSWORD: str = "yibao"
    # 编码
    REDIS_ENCODING: str = "utf-8"
    # 连接超时时间（秒）
    REDIS_TIMEOUT: int = 10
    # 是否自动解码
    REDIS_DECODE_RESPONSES: bool = True
    # 限制最大连接数，避免压垮Redis
    REDIS_MAX_CONNECTIONS: int = 10
    # 键前缀
    REDIS_KEY_PREFIX: str = "app:"

    """ 日志配置 """
    LOG_DIR: str = "/usr/local/app/project"  # 日志目录，可通过.env文件覆盖
    LOG_LEVEL: str = "INFO"  # 日志级别：DEBUG/INFO/WARNING/ERROR/CRITICAL
    LOG_RETENTION_DAYS: int = 7  # 日志保留天数

    # .env文件配置
    model_config = SettingsConfigDict(env_file=".env", env_file_encoding="utf-8")


# 单例，全局复用
settings: Settings = Settings()

一键获取完整项目代码python123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263
```

#### 5.2.日志配置文件

在项目中新建 `core/logging_config.py` 文件

```python
"""
模块名称：日志配置文件
功能描述：
    1. 为Python项目（适配FastAPI）实现生产级日志配置，支持日志按年月日分层存储（logs/yyyy/MM/dd/）；
    2. 自定义日志文件切割规则：单个文件达到10MB后按序号递增生成新文件（yyyyMMdd-i.log），服务重启时复用未写满的日志文件；
    3. 自动清理超过指定天数（默认7天）的过期日志目录及文件，避免磁盘空间占用过高；
    4. 同时输出日志到控制台和文件，日志格式包含时间、模块、日志级别、文件/函数/行号等关键信息；
    5. 降低第三方库（uvicorn/redis/sqlalchemy）日志级别，减少冗余日志输出，提升日志可读性。
适用场景：
    - FastAPI/异步Python项目的日志统一管理
    - 需要按大小切割日志、自动清理过期日志的生产环境
依赖说明：
    - Python内置logging模块，无额外第三方依赖
    - app.core.config.settings：项目配置模块（需包含日志目录、保留天数等配置项）
"""

import logging
from datetime import datetime, timedelta
from logging.handlers import RotatingFileHandler
from pathlib import Path

from app.core.config.settings import settings  # 导入项目配置

# 新增：日志保留天数（从配置读取，默认7天）
LOG_RETENTION_DAYS = getattr(settings, "LOG_RETENTION_DAYS", 7)
# 新增：单个日志文件大小阈值（10MB）
LOG_MAX_SIZE = 10 * 1024 * 1024  # 10MB


def get_today_log_path():
    """
    生成当日日志目录和基础文件名：
    - 目录：logs/yyyy/MM/dd/
    - 基础文件名：yyyyMMdd（后续拼接序号）
    """
    today = datetime.now()
    # 按年/月/日分层创建目录
    year = today.strftime("%Y")
    month = today.strftime("%m")
    day = today.strftime("%d")
    # 日志根目录（从配置读取，默认logs）
    log_root = Path(settings.LOG_DIR) if hasattr(settings, "LOG_DIR") else Path("logs")
    # 当日目录：logs/2026/03/09/
    today_log_dir = log_root / year / month / day
    # 确保目录存在（不存在则递归创建）
    today_log_dir.mkdir(parents=True, exist_ok=True)
    # 基础文件名：20260309
    base_filename = today.strftime("%Y%m%d")
    return today_log_dir, base_filename


def get_next_log_file_number(log_dir: Path, base_filename: str) -> int:
    """
    获取当日下一个日志文件的序号（i）：
    - 扫描目录下所有 yyyyMMdd-i.log 文件，取最大序号
    - 检查最大序号文件的大小，若未达阈值则复用该序号，否则+1
    """
    max_num = 0
    # 遍历目录下的日志文件
    for file in log_dir.glob(f"{base_filename}-*.log"):
        try:
            # 提取文件名中的序号（如 20260309-2.log → 2）
            file_num = int(file.name.split("-")[-1].split(".")[0])
            if file_num > max_num:
                max_num = file_num
        except (IndexError, ValueError):
            # 文件名格式异常则跳过
            continue

    # 若存在最大序号文件，检查其大小是否未达阈值
    if max_num > 0:
        latest_log_file = log_dir / f"{base_filename}-{max_num}.log"
        if latest_log_file.exists() and latest_log_file.stat().st_size < LOG_MAX_SIZE:
            return max_num  # 复用当前序号

    return max_num + 1  # 序号+1


def clean_expired_logs():
    """
    清理超过指定天数的日志文件/目录：
    - 遍历日志根目录下的年/月/日目录
    - 删除早于 LOG_RETENTION_DAYS 天的目录及文件
    """
    log_root = Path(settings.LOG_DIR) if hasattr(settings, "LOG_DIR") else Path("logs")
    if not log_root.exists():
        return

    # 计算过期时间阈值
    expire_threshold = datetime.now() - timedelta(days=LOG_RETENTION_DAYS)

    # 遍历年目录（如 logs/2026）
    for year_dir in log_root.glob("*"):
        if not year_dir.is_dir() or not year_dir.name.isdigit():
            continue

        # 遍历月目录（如 logs/2026/03）—— 外层循环
        for month_dir in year_dir.glob("*"):
            if not month_dir.is_dir() or not month_dir.name.isdigit() or len(month_dir.name) != 2:
                continue

            # ========== 关键修复：将日目录循环缩进至此 ==========
            # 遍历日目录（如 logs/2026/03/09）—— 内层循环，嵌套在month_dir循环内
            for day_dir in month_dir.glob("*"):
                if not day_dir.is_dir() or not day_dir.name.isdigit() or len(day_dir.name) != 2:
                    continue

                # 拼接日期字符串并解析
                try:
                    dir_date_str = f"{year_dir.name}{month_dir.name}{day_dir.name}"
                    dir_date = datetime.strptime(dir_date_str, "%Y%m%d")
                except ValueError:
                    continue

                # 如果目录日期早于阈值，删除整个目录（包含所有日志文件）
                if dir_date < expire_threshold:
                    # 递归删除目录及文件
                    for file in day_dir.glob("*"):
                        if file.is_file():
                            file.unlink(missing_ok=True)
                    day_dir.rmdir(missing_ok=True)
                    # 清理空的月/年目录
                    if not any(month_dir.iterdir()):
                        month_dir.rmdir(missing_ok=True)
                    if not any(year_dir.iterdir()):
                        year_dir.rmdir(missing_ok=True)


class DateRotatingFileHandler(RotatingFileHandler):
    """
    自定义文件处理器：按年月日分目录 + 同日内按大小切割（序号递增）
    """

    def __init__(self, *args, **kwargs):
        # 初始化时先清理过期日志
        clean_expired_logs()
        # 初始化时生成当日日志路径和初始序号
        self.today_log_dir, self.base_filename = get_today_log_path()
        self.current_num = get_next_log_file_number(self.today_log_dir, self.base_filename)
        # 拼接初始日志文件名：20260309-1.log
        initial_log_file = self.today_log_dir / f"{self.base_filename}-{self.current_num}.log"
        super().__init__(str(initial_log_file), maxBytes=LOG_MAX_SIZE, backupCount=0, encoding="utf-8", mode="a")

    def doRollover(self):
        """
        重写切割逻辑：文件达到大小限制时，序号+1生成新文件
        """
        # 切割时清理过期日志
        clean_expired_logs()
        # 检查是否跨日（跨日则重新生成目录和基础文件名）
        new_log_dir, new_base_filename = get_today_log_path()
        if new_log_dir != self.today_log_dir or new_base_filename != self.base_filename:
            self.today_log_dir = new_log_dir
            self.base_filename = new_base_filename
            self.current_num = 1  # 跨日重置序号为1
        else:
            self.current_num += 1  # 同日内序号+1

        # 关闭当前文件句柄
        if self.stream:
            self.stream.close()
            self.stream = None  # type: ignore[assignment]

        # 生成新的日志文件名
        new_log_file = self.today_log_dir / f"{self.base_filename}-{self.current_num}.log"
        self.baseFilename = str(new_log_file)

        # 重新打开新文件
        if not self.delay:
            self.stream = self._open()


def setup_logging():
    """
    最终日志配置：
    - 控制台输出：INFO及以上
    - 文件输出：按年月日分目录，同日内按大小切割（10MB/个），命名格式 yyyyMMdd-i.log
    - 自动清理超过指定天数的日志文件
    """
    # 1. 基础格式配置
    log_format = logging.Formatter(
        "%(asctime)s | %(name)s | %(levelname)s | %(filename)s:%(funcName)s:%(lineno)d | %(message)s",
        datefmt="%Y-%m-%d %H:%M:%S"
    )

    # 2. 控制台处理器
    console_handler = logging.StreamHandler()
    console_handler.setFormatter(log_format)
    console_handler.setLevel(logging.INFO)

    # 3. 自定义文件处理器（按年月日分目录+序号+自动清理）
    file_handler = DateRotatingFileHandler()
    file_handler.setFormatter(log_format)
    file_handler.setLevel(logging.INFO)

    # 4. 根日志器配置
    root_logger = logging.getLogger()
    root_logger.setLevel(logging.WARNING)
    # 避免重复添加处理器
    if not root_logger.handlers:
        root_logger.addHandler(console_handler)
        root_logger.addHandler(file_handler)

    # 5. 降低第三方库日志级别（减少冗余）
    logging.getLogger("uvicorn").setLevel(logging.WARNING)
    logging.getLogger("redis").setLevel(logging.WARNING)
    logging.getLogger("sqlalchemy").setLevel(logging.WARNING)

一键获取完整项目代码python123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263646566676869707172737475767778798081828384858687888990919293949596979899100101102103104105106107108109110111112113114115116117118119120121122123124125126127128129130131132133134135136137138139140141142143144145146147148149150151152153154155156157158159160161162163164165166167168169170171172173174175176177178179180181182183184185186187188189190191192193194195196197198199200201202203204205206207208
```

#### 5.3.引入日志配置

在 FastAPI 主文件（如 `main.py`）的**最顶部**引入并执行日志配置（确保日志配置优先加载）：

```python
import uvicorn
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

from app.api.endpoints import router as api_endpoint_router
from app.core.config.logging_config import setup_logging
from app.core.config.settings import settings
from app.core.exception import register_exception_handlers

# 第一步：先配置日志（必须在其他导入之前）
setup_logging()

# 创建FastAPI实例
app = FastAPI(title=settings.PROJECT_NAME, version=settings.PROJECT_VERSION)

# 添加CORS中间件
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # 允许的源，开发阶段允许所有源，生产环境需要指定源
    allow_credentials=True,  # 允许携带cookie
    allow_methods=["*"],  # 允许的请求方法
    allow_headers=["*"],  # 允许的请求头
)

# 注册全局异常处理器
register_exception_handlers(app)

# 注册路由
app.include_router(api_endpoint_router, prefix=settings.API_PREFIX)

if __name__ == "__main__":
    # 启动服务
    uvicorn.run(
        app="main:app",
        host=settings.SERVER_HOST,
        port=settings.SERVER_PORT,
        reload=settings.DEBUG,
        log_level=settings.LOGGING_LEVEL,
    )

一键获取完整项目代码python12345678910111213141516171819202122232425262728293031323334353637383940
```

#### 5.4.使用日志

业务代码无需修改，直接使用即可，日志会自动输出到控制台和文件：

```python
# 业务代码（如 app/crud/category.py）
import logging
logger = logging.getLogger(__name__)

async def get_category_list(db: AsyncSession, skip: int = 0, limit: int = 100):
    """
    获取新闻分类列表
    """
    # 读取缓存
    category_list = await news_cache.get_category_list_cache()
    if category_list:
        logger.info("读取分类列表缓存成功")  # 会输出到控制台+logs/app.log
        return category_list

    # 查询数据库...
    logger.info("分类列表缓存未命中，查询数据库")
    # ... 其他逻辑 ...
一键获取完整项目代码python1234567891011121314151617
```

### 6.注册中间件

#### 6.1.统一跨域配置

解决前端跨域请求问题：

```python
"""
模块名称：cors
功能描述：实现FastAPI跨域中间件配置，解决前后端分离场景下的跨域请求问题
"""
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

# 生产环境建议替换为具体的前端域名列表（如 ["https://www.xxx.com"]）
ALLOWED_ORIGINS = ["*"]
# 生产环境建议限制METHODS/HEADERS，仅开放必要的
ALLOWED_METHODS = ["*"]
ALLOWED_HEADERS = ["*"]


def register_cors_middleware(app: FastAPI):
    """
    注册跨域中间件（封装为函数，方便配置调整）
    """

    app.add_middleware(
        CORSMiddleware,  # type: ignore  # 关键：忽略类型提示
        allow_origins=ALLOWED_ORIGINS,
        allow_credentials=True,  # 允许携带Cookie
        allow_methods=ALLOWED_METHODS,
        allow_headers=ALLOWED_HEADERS,
        # 可选：暴露自定义响应头（如X-Token）
        # expose_headers=["X-Token"]
    )

一键获取完整项目代码python1234567891011121314151617181920212223242526272829
```

#### 6.2.统一日志埋点

除了基础日志配置，还需要记录**接口访问日志**（请求参数、响应结果、耗时）：

```python
"""
模块名称：access_log
功能描述：实现FastAPI访问日志中间件，记录每个接口的请求IP、方法、URL、响应状态码、耗时等信息
"""
import logging
import time

from fastapi import Request, Response
from starlette.middleware.base import BaseHTTPMiddleware

# 专属日志器（方便区分访问日志和其他日志）
logger = logging.getLogger("api.access")


class AccessLogMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request: Request, call_next) -> Response:
        """
        核心逻辑：记录请求前信息 → 执行请求 → 记录响应后信息
        """
        # 1. 记录请求开始时间和基础信息
        start_time = time.time()
        client_ip = request.client.host if request.client else "unknown"
        method = request.method
        url = request.url.path
        # 可选：记录请求参数（GET/POST），生产环境敏感参数需脱敏
        # query_params = dict(request.query_params)
        # body = await request.body() if method in ["POST", "PUT"] else ""

        try:
            # 2. 执行实际的接口请求
            response = await call_next(request)
        except Exception as e:
            # 3. 捕获请求异常，记录错误日志
            cost = round(time.time() - start_time, 3)
            logger.error(
                f"请求IP:{client_ip} | 方法:{method} | URL:{url} | 响应状态码:500 | 耗时:{cost}s | 错误:{str(e)}"
            )
            raise  # 重新抛出异常，让统一异常处理器处理

        # 4. 记录正常响应信息
        cost = round(time.time() - start_time, 3)
        status_code = response.status_code
        logger.info(
            f"请求IP:{client_ip} | 方法:{method} | URL:{url} | 响应状态码:{status_code} | 耗时:{cost}s"
        )

        return response

一键获取完整项目代码python123456789101112131415161718192021222324252627282930313233343536373839404142434445464748
```

#### 6.3.统一注册中间件

`app/core/middleware/__init__.py` 统一导出，简化引入

```python
"""
模块名称：middleware
功能描述：汇总所有自定义中间件，提供统一的注册入口
"""
from .access_log import AccessLogMiddleware
from .cors import register_cors_middleware


# 统一注册所有中间件的函数（对外暴露的核心方法）
def register_all_middlewares(app):
    """
    注册项目所有中间件，按执行顺序排列：
    1. 跨域中间件（优先执行，解决预检请求问题）
    2. 访问日志中间件（记录所有请求）
    """
    # 1. 注册跨域中间件
    register_cors_middleware(app)
    # 2. 注册访问日志中间件
    app.add_middleware(AccessLogMiddleware)


# 导出核心类/函数，方便外部直接使用
__all__ = ["AccessLogMiddleware", "register_cors_middleware", "register_all_middlewares"]

一键获取完整项目代码python123456789101112131415161718192021222324
```

#### 6.4.main 引入并注册

```python
"""
模块名称：应用入口文件
功能描述：
    1. FastAPI项目的核心入口文件，负责应用的初始化、组件注册和服务启动；
    2. 按「配置优先、组件分层注册」原则，依次完成日志初始化、应用实例化、中间件/异常处理器/路由注册；
    3. 统一管理项目启动参数（监听地址、端口、热重载、日志级别），所有配置从全局设置模块读取；
    4. 提供开发环境直接启动入口，同时兼容生产环境 uvicorn 命令行启动方式。
核心依赖：
    - FastAPI：Web框架核心
    - uvicorn：ASGI服务器
    - 自定义模块：日志配置、全局异常、中间件、路由、项目配置
"""

import uvicorn
from fastapi import FastAPI

from app.api.endpoints import router as api_endpoint_router
from app.core.config.logging_config import setup_logging
from app.core.config.settings import settings
from app.core.exception import register_exception_handlers
from app.core.middleware import register_all_middlewares

# 1. 全局基础配置：先初始化日志（最高优先级）
setup_logging()

# 2. 实例化FastAPI应用
app = FastAPI(title=settings.PROJECT_NAME, version=settings.PROJECT_VERSION)

# 3. 注册全局中间件
register_all_middlewares(app)

# 4. 注册全局异常处理器
register_exception_handlers(app)

# 5. 注册业务路由
app.include_router(api_endpoint_router, prefix=settings.API_PREFIX)

# ===================== 应用启动入口 =====================
if __name__ == "__main__":
    """
    开发环境启动入口（生产环境建议用 uvicorn 命令行启动：uvicorn main:app --host 0.0.0.0 --port 8000）
    """
    uvicorn.run(
        app="main:app",  # 指向当前文件的app实例
        host=settings.SERVER_HOST,  # 服务监听地址（0.0.0.0允许外网访问）
        port=settings.SERVER_PORT,  # 服务端口
        reload=settings.RELOAD,  # 开发环境开启热重载（生产环境务必关闭）
        log_level=settings.LOG_LEVEL  # 日志级别（与自定义日志配置联动）
    )

一键获取完整项目代码python1234567891011121314151617181920212223242526272829303132333435363738394041424344454647484950
```

### 7.统一参数校验

FastAPI 原生依赖 Pydantic 做参数校验，但需要封装**通用校验规则**和**自定义校验器**，避免重复代码：

#### 7.1.异常处理器拦截

通过异常处理器拦截 `ValidationError`，将其转换为标准化 API 响应格式

```python
def register_exception_handlers(app):
    
    @app.exception_handler(RequestValidationError)
    async def validation_exception_handler(request: Request, exc: RequestValidationError):
        """
        处理参数校验异常
        :param request: 请求对象
        :param exc: 异常对象
        :return: 响应对象
        触发示例
        class UserRegisterDTO(BaseModel):
            username: str = Field(..., min_length=3, max_length=20, description="用户名，3-20字符")
            password: str = Field(..., min_length=6, description="密码，至少6字符")
            email: EmailStr = Field(..., description="邮箱，格式必须合法")
        """
        # return JSONResponse(
        #     status_code=422,
        #     content=fail(code=422, message=f"参数校验失败：{exc.errors()}").model_dump()
        # )
        # 返回统一格式
        # {
        #     "code": 422,
        #     "message": "参数校验失败：[{'type': 'string_too_long', 'loc': ('body', 'username'), 'msg': 'String should have at most 5 characters', 'input': 'bbbbbb', 'ctx': {'max_length': 5}}]",
        #     "data": null
        # }

        # 1. 解析原生错误信息，提取关键内容
        error_details: List[Dict] = []
        simple_msg: str = ""
        for err in exc.errors():
            # 打印错误信息
            print(f"参数校验错误：{err}")
            # err 结构示例：
            # 自定义 ValueError 提示:
            # {'type': 'value_error', 'loc': ('body', 'newPassword'), 'msg': 'Value error, 新密码必须是6位数字', 'input': '11', 'ctx': {'error': ValueError('新密码必须是6位数字')}}
            # Pydantic 原生错误提示:
            # {'type': 'string_too_short', 'loc': ('body', 'newPassword'), 'msg': 'String should have at least 6 characters', 'input': '11', 'ctx': {'min_length': 6}}

            # 1. 提取字段名（兼容原生loc和自定义字段）
            if "loc" in err:
                field = ".".join(map(str, err["loc"]))
            else:
                field = "unknown"

            # 2. 优先解析自定义 ValueError 提示（核心修改）
            if "ctx" in err and "error" in err["ctx"] and hasattr(err["ctx"]["error"], "args"):
                # 提取 ValueError 的自定义提示信息
                message = err["ctx"]["error"].args[0]
            # 3. 解析 Pydantic 原生错误提示（兜底）
            else:
                message = err["msg"]

            # 4. 构建错误详情（关键：将解析后的提示存入）
            error_details.append({
                "field": field,  # 错误字段（如 body.password、query.username）
                "message": message,  # 错误提示
                "type": err["type"]  # 错误类型（可选，供前端定位问题）
            })

        # 2. 构造最终友好提示（复用 error_details 中的信息）
        # simple_msg = f"参数错误：{'; '.join([f'{item['field']}: {item['message']}' for item in error_details])}"   # 字段+错误信息
        simple_msg = f"参数错误：{'; '.join([f'{item['message']}' for item in error_details])}"  # 仅提示错误信息

        # 3. 返回统一格式（code=422 是 HTTP 标准的参数校验错误码）
        return JSONResponse(
            status_code=status.HTTP_422_UNPROCESSABLE_CONTENT,  # HTTP 状态码与业务码一致
            content=fail(
                message=simple_msg,
                code=status.HTTP_422_UNPROCESSABLE_CONTENT,
                data=error_details  # 可选：返回详细错误信息，供前端精准处理
            ).model_dump()
        )
一键获取完整项目代码python123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263646566676869707172
```

#### 7.2.自定义验证异常

```python
def raise_unprocessable_entity(message: str):
    """抛出422错误（数据验证错误）"""
    # 场景：参数格式正确但规则不符（如密码复杂度不够、开始时间大于结束时间）
    raise_business_exception(message=message, code=status.HTTP_422_UNPROCESSABLE_ENTITY)
一键获取完整项目代码python1234
```

#### 7.3.校验应用

字段约束校验、字段级校验器、模型级校验器

```python
import re
from datetime import datetime
from typing import Optional

from pydantic import BaseModel, Field, model_validator, field_validator

from app.core.exception.error_code import ErrorCode
from app.core.exception.exceptions import raise_unprocessable_entity, BusinessException, raise_business_exception
from app.schemas import COMMON_CONFIG


class PwdUpdateDTO(BaseModel):
    """
    修改密码请求参数
    """
    old_password: str = Field(..., max_length=50, alias="oldPassword", description="旧密码")
    # 使用 @field_validator 和 @model_validator 时, new_password 不能使用 Field 关键字参数
    new_password: str = Field(..., alias="newPassword", description="新密码")

    # 优先级（执行顺序）:
    # 字段约束校验 > 字段级校验器 > 模型级校验器（前一级失败则后一级不执行）

    # 字段约束校验
    # 基于 Field 关键字参数的基础校验（长度、格式、范围等），Pydantic 内置最基础的校验规则
    # new_password: str = Field(..., min_length=6, alias="newPassword", description="新密码")

    # 字段级校验器
    # 针对单个字段的自定义逻辑校验，可覆盖 / 补充字段约束的不足（如密码格式、自定义规则）
    @field_validator("new_password")
    def validate_new_password_field(cls, v):  # cls=模型类，v=字段值
        """
        字段级（仅针对 new_password 单个字段）字段关联精准、语法简洁、无需手动提取值
        单个字段解析完成后立即执行，优先级高于模型级校验。同时定义了 field_validator 和 model_validator，field_validator 会先执行
        """
        if not (len(v) > 6):
            raise ValueError("新密码至少 6 位字符") # {"code":422,"message":"参数错误：新密码至少 6 位字符","data":[{"field":"body.newPassword","message":"新密码至少 6 位字符","type":"value_error"}]}
            # raise raise_unprocessable_entity("新密码至少 6 位字符") # {"code":422,"message":"新密码必须是不少于6位的数字","data":null}
            # raise raise_business_exception("新密码至少 6 位字符", ErrorCode.PARAM_ERROR)   # {"code":40001,"message":"新密码至少 6 位字符","data":null}
            # raise BusinessException(ErrorCode.PARAM_ERROR, "新密码至少 6 位字符")   # {"code":40001,"message":"新密码至少 6 位字符","data":null}
        return v

    # 模型级校验器
    # 针对整个模型的自定义校验，可访问所有字段，支持多字段联动逻辑
    @model_validator(mode='after')
    def validate_password_model(self):  # self = 模型实例
        """
        模型级（可访问所有字段）、支持复杂业务规则
        需等所有字段的 field_validator 执行完成、模型初始化完毕后才执行；
        如果两个校验器方法名相同，field_validator 被 model_validator 覆盖，导致只执行后者
        """
        # 校验新密码：等价于原field_validator的逻辑
        v = self.new_password  # 获取new_password字段值
        if not (len(v) > 6):
            # 手动标注错误字段，让前端能精准定位（比原field_validator更友好）
            raise ValueError("新密码必须不少于 6 位字符")
        return self  # 必须返回模型实例，否则校验失败

    ######################## 其它场景的校验方式 ##########################

    # 批量校验：同时处理 old_password + new_password
    @field_validator("old_password", "new_password")
    # noinspection PyMethodParameters
    def strip_whitespace(cls, v):
        """批量去除密码首尾空格（避免用户输入多余空格）"""
        if isinstance(v, str):
            return v.strip()  # 处理后返回清洗后的值
        return v

    # 预处理原始数据（mode='before'）
    @model_validator(mode='before')
    def preprocess_raw_data(cls, values):
        """
        预处理：
        1. 兼容前端可能传的「new_password」（下划线）而非「newPassword」（驼峰）
        2. 为空的密码字段填充默认值（或抛错）
        """
        # 字段别名兼容：若前端传了 new_password，映射到 newPassword
        if "new_password" in values and "newPassword" not in values:
            values["newPassword"] = values.pop("new_password")
        # 空值处理：旧密码不能为空
        if not values.get("oldPassword"):
            raise ValueError("oldPassword: 旧密码不能为空")
        return values  # 必须返回处理后的字典

一键获取完整项目代码python123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263646566676869707172737475767778798081828384
```

### 8.缓存策略

系统采用 Redis 作为缓存层，对高频访问的数据进行缓存，以提升系统性能和响应速度。

#### 8.1.缓存相关参数

```python
import logging

from pydantic_settings import BaseSettings, SettingsConfigDict


# 配置文件
class Settings(BaseSettings):
    """ 项目配置 """
    # 项目名称
    PROJECT_NAME: str = "FastAPI Project"
    # 项目版本
    PROJECT_VERSION: str = "1.0.0"
    # 接口前缀
    API_PREFIX: str = "/api"
    # 服务主机
    SERVER_HOST: str = "0.0.0.0"
    # 服务端口
    SERVER_PORT: int = 8000
    # 日志等级
    LOGGING_LEVEL: int = logging.INFO

    """ 数据库配置 """
    # 数据库连接字符串
    DB_URL: str = "mysql+aiomysql://root:123456@localhost:3306/news_app?charset=utf8mb4"
    # 是否调试模式
    DB_DEBUG: bool = True
    # 数据库连接池大小
    DB_POOL_SIZE: int = 10
    # 数据库连接池最大连接数
    DB_MAX_OVERFLOW: int = 20

    """ Redis配置 """
    # Redis 服务器地址
    REDIS_HOST: str = "localhost"
    # Redis 端口
    REDIS_PORT: int = 6379
    # 数据库编号（默认0）
    REDIS_DB: int = 0
    # Redis密码
    REDIS_PASSWORD: str = "yibao"
    # 编码
    REDIS_ENCODING: str = "utf-8"
    # 连接超时时间（秒）
    REDIS_TIMEOUT: int = 10
    # 是否自动解码
    REDIS_DECODE_RESPONSES: bool = True
    # 限制最大连接数，避免压垮Redis
    REDIS_MAX_CONNECTIONS: int = 10
    # 键前缀
    REDIS_KEY_PREFIX: str = "app:"

    """ 日志配置 """
    LOG_DIR: str = "logs"  # 日志目录，可通过.env文件覆盖
    LOG_LEVEL: str = "INFO"  # 日志级别：DEBUG/INFO/WARNING/ERROR/CRITICAL
    LOG_RETENTION_DAYS: int = 7

    # .env文件配置
    model_config = SettingsConfigDict(env_file=".env", env_file_encoding="utf-8")


# 单例，全局复用
settings: Settings = Settings()
一键获取完整项目代码python1234567891011121314151617181920212223242526272829303132333435363738394041424344454647484950515253545556575859606162
```

#### 8.2.缓存操作工具

```python
"""
模块名称：Redis 缓存操作工具
功能描述：
    1. 基于Redis异步客户端实现通用缓存操作封装，适配FastAPI异步项目；
    2. 提供Redis连接池单例管理，避免频繁创建/销毁连接导致性能损耗；
    3. 封装缓存的增（set）、查（get）、删（delete）核心操作，包含完善的异常处理和日志记录；
    4. 内置缓存键前缀机制，避免不同业务模块的缓存键冲突；
    5. 支持缓存值的JSON序列化/反序列化，兼容中文和复杂数据类型（dict/list）；
    6. 提供参数校验、过期时间管控等健壮性保障，适配生产环境使用。
适用场景：
    - FastAPI项目中各类业务数据的缓存读写（如新闻列表、分类信息、用户数据等）
    - 需要统一管理Redis连接和缓存操作的异步场景
依赖说明：
    - redis[asyncio]：Redis异步客户端
    - app.core.config.settings：项目配置模块（需包含Redis连接参数、键前缀等配置项）
"""

import json
import logging
from functools import lru_cache
from typing import Any, Optional

import redis.asyncio as redis
from redis.exceptions import RedisError  # 精准捕获Redis异常

from app.core.config.settings import settings

# 配置日志（替换print，适配生产环境）
logger = logging.getLogger(__name__)


# ===================== 核心优化：连接池管理 =====================
@lru_cache()  # 单例，避免重复创建
def get_redis_pool() -> redis.ConnectionPool:
    """创建Redis连接池（单例模式）"""
    return redis.ConnectionPool(
        host=settings.REDIS_HOST,
        port=settings.REDIS_PORT,
        db=settings.REDIS_DB,
        password=settings.REDIS_PASSWORD,
        socket_timeout=settings.REDIS_TIMEOUT,
        encoding=settings.REDIS_ENCODING,
        decode_responses=settings.REDIS_DECODE_RESPONSES,  # 是否将字节数据解码为字符串
        max_connections=settings.REDIS_MAX_CONNECTIONS  # 限制最大连接数，避免压垮Redis
    )


async def get_redis_client() -> redis.Redis:
    """获取Redis客户端（FastAPI依赖注入用）"""
    pool = get_redis_pool()
    return redis.Redis(connection_pool=pool)


# ===================== 缓存操作封装（核心功能） =====================
def _add_cache_prefix(key: str) -> str:
    """给缓存键添加统一前缀，避免键冲突"""
    prefix = settings.REDIS_KEY_PREFIX or "app:"  # 建议在settings中配置前缀，如"news:"
    return f"{prefix}{key}"


async def get_cache(key: str) -> Optional[Any]:
    """
    获取缓存（优化：精准异常捕获+日志+键前缀）

    :param key: 原始缓存键
    :return: 反序列化后的缓存值，无缓存/失败返回None
    """
    # 入参校验
    if not isinstance(key, str) or not key.strip():
        logger.warning("缓存键必须为非空字符串")
        return None

    full_key = _add_cache_prefix(key)
    redis_client = await get_redis_client()

    try:
        value = await redis_client.get(full_key)
        if value is None:
            logger.debug(f"缓存未命中：{full_key}")
            return None

        # 反序列化JSON（兼容非JSON格式）
        try:
            return json.loads(value)
        except json.JSONDecodeError:
            logger.debug(f"缓存值非JSON格式，返回原始值：{full_key}")
            return value
    except RedisError as e:  # 仅捕获Redis相关异常，不吞其他错误
        logger.error(f"读取缓存失败：key={full_key}，错误：{str(e)}", exc_info=True)
        return None
    except Exception as e:  # 兜底异常（非预期错误）
        logger.critical(f"读取缓存发生未知错误：key={full_key}，错误：{str(e)}", exc_info=True)
        return None


async def set_cache(
        key: str,
        value: Any,
        expire: Optional[int] = None
) -> bool:
    """
    设置缓存（优化：入参校验+JSON序列化优化+过期时间校验）

    :param key: 原始缓存键
    :param value: 缓存值（支持dict/list/str/int等，None会被过滤）
    :param expire: 过期时间（秒），None表示永不过期
    :return: 设置成功返回True，失败返回False
    """
    # 入参校验
    if not isinstance(key, str) or not key.strip():
        logger.warning("缓存键必须为非空字符串")
        return False
    if value is None:
        logger.warning("缓存值不能为None，跳过写入")
        return False
    if expire is not None and (not isinstance(expire, int) or expire <= 0):
        logger.warning(f"过期时间必须为正整数，当前值：{expire}")
        return False

    full_key = _add_cache_prefix(key)
    redis_client = await get_redis_client()

    try:
        # 序列化处理（兼容不同类型）
        if isinstance(value, (dict, list)):
            # 优化：ensure_ascii=False 保留中文，sort_keys=True 保证序列化结果一致
            serialized_value = json.dumps(value, ensure_ascii=False, sort_keys=True)
        elif isinstance(value, (str, int, float, bool)):
            serialized_value = str(value)
        else:
            logger.warning(f"不支持的缓存值类型：{type(value)}，key={full_key}")
            return False

        # 写入缓存
        if expire:
            await redis_client.setex(full_key, expire, serialized_value)
        else:
            await redis_client.set(full_key, serialized_value)

        logger.debug(f"缓存设置成功：key={full_key}，过期时间={expire}秒")
        return True
    except RedisError as e:
        logger.error(f"写入缓存失败：key={full_key}，错误：{str(e)}", exc_info=True)
        return False
    except Exception as e:
        logger.critical(f"写入缓存发生未知错误：key={full_key}，错误：{str(e)}", exc_info=True)
        return False


async def delete_cache(key: str) -> bool:
    """新增：删除缓存（常用操作补充）"""
    if not isinstance(key, str) or not key.strip():
        logger.warning("缓存键必须为非空字符串")
        return False

    full_key = _add_cache_prefix(key)
    redis_client = await get_redis_client()

    try:
        result = await redis_client.delete(full_key)
        logger.debug(f"缓存删除结果：key={full_key}，是否成功={bool(result)}")
        return bool(result)
    except RedisError as e:
        logger.error(f"删除缓存失败：key={full_key}，错误：{str(e)}", exc_info=True)
        return False

一键获取完整项目代码python123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263646566676869707172737475767778798081828384858687888990919293949596979899100101102103104105106107108109110111112113114115116117118119120121122123124125126127128129130131132133134135136137138139140141142143144145146147148149150151152153154155156157158159160161162163164165166
```

#### 8.3.设置缓存函数

```python
"""
模块名称：新闻缓存模块
功能描述：设置和获取新闻相关缓存
"""

from typing import Optional

from app.db.redis_client import get_cache, set_cache
from app.models.news import Category, News

# 分类、配置: 7200; 列表:600; 详情:1800; 验证码:120 -- 数据越稳定，缓存越持久
CONFIG_CACHE_EXPIRE: int = 7200
DETAIL_CACHE_EXPIRE: int = 1800
LIST_CACHE_EXPIRE: int = 600
VERIFY_CODE_CACHE_EXPIRE: int = 120

# 新闻分类列表缓存键
NEWS_CATEGORY_LIST_KEY: str = "news:category_list"
# 新闻列表缓存键
NEWS_LIST_KEY: str = "news:list:{category_id}:{page}:{page_size}"
# 新闻详情缓存键
NEWS_DETAIL_KEY: str = "news:detail:{news_id}"
# 相关新闻缓存缓存键
NEWS_RELATED_NEWS_KEY: str = "news:related_news:{news_id}:{category_id}"


async def get_category_list_cache() -> list[Category]:
    """
    获取新闻分类列表缓存
    :return: 分类列表
    """
    return await get_cache(NEWS_CATEGORY_LIST_KEY)


async def set_category_list_cache(category_list: list[Category], expire: int = CONFIG_CACHE_EXPIRE) -> bool:
    """
    设置新闻分类列表缓存
    :param category_list: 分类列表
    :param expire: 过期时间
    :return: 设置成功返回True，失败返回False
    """
    return await set_cache(NEWS_CATEGORY_LIST_KEY, category_list, expire)


async def get_news_list_cache(category_id: Optional[int], page: int, page_size: int) -> list[News]:
    """
    获取新闻列表缓存
    :param category_id: 分类ID
    :param page: 页码
    :param page_size: 每页数量
    :return: 新闻列表
    """
    return await get_cache(
        NEWS_LIST_KEY.format(category_id=get_category_id(category_id), page=page, page_size=page_size))


async def set_news_list_cache(
        category_id: Optional[int],
        page: int,
        page_size: int,
        news_list: list[News],
        expire: int = LIST_CACHE_EXPIRE) -> bool:
    """
    设置新闻列表缓存
    :param category_id: 分类ID
    :param page: 页码
    :param page_size: 每页数量
    :param news_list: 新闻列表
    :param expire: 过期时间
    :return: 设置成功返回True，失败返回False
    """
    return await set_cache(
        NEWS_LIST_KEY.format(category_id=get_category_id(category_id), page=page, page_size=page_size),
        news_list, expire)


def get_category_id(category_id: Optional[int]) -> int | str:
    """
    获取分类ID，如果为None则返回"all"
    :param category_id: 分类ID
    :return: 分类ID
    """
    return category_id or "all"


async def get_news_detail_cache(news_id: int) -> News:
    """
    获取新闻详情缓存
    :param news_id: 新闻ID
    :return: 新闻详情
    """
    return await get_cache(NEWS_DETAIL_KEY.format(news_id=news_id))


async def set_news_detail_cache(news_id: int, news_detail: News, expire: int = DETAIL_CACHE_EXPIRE) -> bool:
    """
    设置新闻详情缓存
    :param news_id: 新闻ID
    :param news_detail: 新闻详情
    :param expire: 过期时间
    :return: 设置成功返回True，失败返回False
    """
    return await set_cache(NEWS_DETAIL_KEY.format(news_id=news_id), news_detail, expire)


async def get_related_news_cache(news_id: int, category_id: int) -> list[News]:
    """
    获取相关新闻缓存
    :param news_id: 新闻ID
    :param category_id: 分类ID
    :return: 相关新闻列表
    """
    return await get_cache(NEWS_RELATED_NEWS_KEY.format(news_id=news_id, category_id=category_id))


async def set_related_news_cache(
        news_id: int,
        category_id: int,
        related_news: list[News],
        expire: int = DETAIL_CACHE_EXPIRE) -> bool:
    """
    设置相关新闻缓存
    :param news_id: 新闻ID
    :param category_id: 分类ID
    :param related_news: 相关新闻列表
    :param expire: 过期时间
    :return: 设置成功返回True，失败返回False
    """
    return await set_cache(NEWS_RELATED_NEWS_KEY.format(news_id=news_id, category_id=category_id), related_news, expire)

一键获取完整项目代码python123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263646566676869707172737475767778798081828384858687888990919293949596979899100101102103104105106107108109110111112113114115116117118119120121122123124125126127128129130
```

#### 8.4.调用缓存函数

```python
# 配置日志
import logging
from typing import Sequence

from fastapi.encoders import jsonable_encoder
from sqlalchemy import select, func, update
from sqlalchemy.ext.asyncio import AsyncSession

import app.cache.news as news_cache
from app.models.news import Category, News

logger = logging.getLogger(__name__)


async def get_category_list(db: AsyncSession, skip: int = 0, limit: int = 100) -> list[Category]:
    """
    获取新闻分类列表
    """

    # 读取缓存
    category_list: list[Category] = await news_cache.get_category_list_cache()
    if category_list:
        logger.warning("[新闻分类] 读取缓存成功")
        return category_list

    # 查询数据库
    query = select(Category).offset(skip).limit(limit)  # 查询语句
    result = await db.execute(query)  # 执行查询
    db_result: Sequence[Category] = result.scalars().all()  # 获取结果
    # 转为具体的 list，消除类型提示
    category_list: list[Category] = list(db_result)

    # 写入缓存
    if category_list:
        success: bool = await news_cache.set_category_list_cache(jsonable_encoder(category_list))
        if success:
            logger.warning("[新闻分类] 写入缓存成功")
        else:
            logger.error("[新闻分类] 写入缓存失败")

    # 返回结果
    return category_list


async def get_news_list(db: AsyncSession, category_id: int, page: int, page_size: int) -> list[News]:
    """
    获取新闻列表
    """

    # 读取缓存
    news_list: list[News] = await news_cache.get_news_list_cache(category_id, page, page_size)
    if news_list:
        logger.warning("[新闻列表] 读取缓存成功")
        return news_list

    # 查询数据库
    query = select(News).where(News.category_id == category_id).offset((page - 1) * page_size).limit(page_size)
    result = await db.execute(query)
    # Sequence 是对「有序集合」的抽象描述, SQLAlchemy 为了性能和通用性, 不会直接返回 list
    db_result: Sequence[News] = result.scalars().all()
    # 转为具体的 list，消除类型提示
    news_list: list[News] = list(db_result)

    # 写入缓存
    if news_list:
        logger.warning("[新闻列表] 缓存写入...")
        success: bool = await news_cache.set_news_list_cache(category_id, page, page_size, jsonable_encoder(news_list))
        if success:
            logger.warning("[新闻列表] 写入缓存成功")
        else:
            logger.error("[新闻列表] 写入缓存失败")

    # 返回结果
    return news_list


async def get_news_count(db: AsyncSession, category_id: int) -> int:
    """
    获取新闻总数
    """
    query = select(func.count(News.id)).where(News.category_id == category_id)
    result = await db.execute(query)
    return result.scalar_one()  # 要求结果必须 1 条（0 条 / 多条抛异常）


async def get_news_detail(db: AsyncSession, news_id: int) -> News:
    """
    获取新闻详情
    """

    # 读取缓存
    news_detail: News = await news_cache.get_news_detail_cache(news_id)
    if news_detail:
        logger.warning("[新闻详情] 读取缓存成功")
        return news_detail

    # 查询数据库
    query = select(News).where(News.id == news_id)
    result = await db.execute(query)
    news_detail: News = result.scalar_one_or_none()  # 允许结果 0 条或 1 条（多条仍抛异常）

    # 写入缓存
    if news_detail:
        success: bool = await news_cache.set_news_detail_cache(news_id, jsonable_encoder(news_detail))
        if success:
            logger.warning("[新闻详情] 写入缓存成功")
        else:
            logger.error("[新闻详情] 写入缓存失败")

    # 返回结果
    return news_detail


async def increase_news_views(db: AsyncSession, news_id: int) -> bool:
    """
    浏览次数加1
    """
    query = update(News).where(News.id == news_id).values(views=News.views + 1)
    result = await db.execute(query)
    await db.commit()
    # 更新 → 检查数据库是否真的命中了数据 → 命中了返回True
    return result.rowcount > 0  # type: ignore[attr-defined]


async def get_related_news(db: AsyncSession, news_id: int, category_id: int, limit: int = 5) -> list[News]:
    """
    获取相关新闻
    """

    # 读取缓存
    related_news = await news_cache.get_related_news_cache(news_id, category_id)
    if related_news:
        logger.warning("[相关新闻] 读取缓存成功")
        return related_news

    # 查询数据库
    # 1. 构建查询语句
    query = (select(News)
             .where(News.id != news_id, News.category_id == category_id)
             .order_by(News.views.desc(), News.publish_time.desc())
             .limit(limit))

    # 2. 执行查询，获取数据库模型对象列表
    result = await db.execute(query)
    # 类型说明：scalars().all() 返回 Sequence[News]，显式转为 list[News]
    related_news = list(result.scalars().all())

    # 写入缓存
    if related_news:
        # jsonable_encoder 能正确序列化Pydantic模型/自定义对象
        success: bool = await news_cache.set_related_news_cache(news_id, category_id, jsonable_encoder(related_news))
        if success:
            logger.warning("[相关新闻] 写入缓存成功")
        else:
            logger.error("[相关新闻] 写入缓存失败")

    # 返回结果
    return related_news
```
