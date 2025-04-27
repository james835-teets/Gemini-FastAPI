# Gemi2Api-Server
[HanaokaYuzu / Gemini-API](https://github.com/HanaokaYuzu/Gemini-API) 的服务端简单实现

## 直接运行

0. 填入 `SECURE_1PSID` 和 `SECURE_1PSIDTS`（登录 Gemini 在浏览器开发工具中查找 Cookie）
```properties
SECURE_1PSID = "COOKIE VALUE HERE"
SECURE_1PSIDTS = "COOKIE VALUE HERE"
```
1. `uv` 安装一下依赖
> uv init
> 
> uv add fastapi uvicorn gemini-webapi

> [!NOTE]  
> 如果存在`pyproject.toml` 那么就使用下面的命令：  
> uv sync

或者 `pip` 也可以

> pip install fastapi uvicorn gemini-webapi

2. 激活一下环境
> source venv/bin/activate

3. 启动
> uvicorn main:app --reload --host 127.0.0.1 --port 8000

> [!WARNING] 
> tips: 没有任何API Key，直接使用

## 使用Docker运行（推荐）

### 快速开始

1. 克隆本项目
   ```bash
   git clone https://github.com/zhiyu1998/Gemi2Api-Server.git
   ```

2. 创建 `.env` 文件并填入你的 Gemini Cookie 凭据:
   ```bash
   cp .env.example .env
   # 用编辑器打开 .env 文件，填入你的 Cookie 值
   ```

3. 启动服务:
   ```bash
   docker-compose up -d
   ```

4. 服务将在 http://0.0.0.0:8000 上运行

### 常见问题

如果遇到 `Failed to initialize client` 错误，这通常是因为 Cookie 已过期。请按以下步骤更新:

1. 访问 [Google Gemini](https://gemini.google.com/) 并登录
2. 打开浏览器开发工具 (F12)
3. 切换到 "Application" 或 "应用程序" 标签
4. 在左侧找到 "Cookies" > "gemini.google.com"
5. 复制 `__Secure-1PSID` 和 `__Secure-1PSIDTS` 的值
6. 更新 `.env` 文件
7. 重启容器: `docker-compose restart`

### 其他 Docker 命令

```bash
# 查看日志
docker-compose logs

# 重启服务
docker-compose restart

# 停止服务
docker-compose down

# 重新构建并启动
docker-compose up -d --build
```

## 环境变量配置

服务需要以下环境变量来与Gemini API进行通信：

- `SECURE_1PSID` - Google账号的身份验证Cookie
- `SECURE_1PSIDTS` - Google账号的身份验证Cookie

### Docker 环境变量配置

使用`.env`文件设置环境变量（推荐方式）：

1. 创建`.env`文件，参考`.env.example`：
```bash
# 复制示例文件
cp .env.example .env

# 编辑.env文件
nano .env  # 或使用其他编辑器
```

2. 在`.env`文件中设置变量（**注意：不要使用引号**）：
```
SECURE_1PSID=你的SECURE_1PSID值
SECURE_1PSIDTS=你的SECURE_1PSIDTS值
```

3. 确保值格式正确：
   - 不要在值两边加引号
   - 确保没有多余的空格
   - 复制时确保没有包含不可见字符

如果环境变量仍然没有被正确加载，可以尝试直接在`docker-compose.yml`中的`environment`部分设置。

## API端点

- `GET /`: 服务状态检查
- `GET /v1/models`: 获取可用模型列表
- `POST /v1/chat/completions`: 与模型聊天 (类似OpenAI接口)