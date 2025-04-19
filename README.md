# Gemi2Api-Server
HanaokaYuzu / Gemini-API 的服务端简单实现

## 直接运行

0. 填入 `Secure_1PSID` 和 `Secure_1PSIDTS`  （登录下 Gemini 去 Application - Cookie 里面找）
```properties
SECURE_1PSID = "COOKIE VALUE HERE"
SECURE_1PSIDTS = "COOKIE VALUE HERE"
```
1. `uv` 安装一下依赖
> uv init
> 
> uv add fastapi uvicorn gemini-webapi

或者 `pip` 也可以

> pip install fastapi uvicorn gemini-webapi

2. 激活一下环境
> source venv/bin/activate

3. 启动
> uvicorn main:app --reload --host 127.0.0.1 --port 8000

⚠️ tips: 没有任何API Key，直接使用

## 使用Docker运行

### 使用Docker Compose (推荐)

1. 确保安装了Docker和Docker Compose
2. 配置Gemini凭据（两种方式）:

   a. 创建 `.env` 文件（从示例复制并填入你的凭据）:
   ```bash
   cp .env.example .env
   # 然后编辑 .env 文件，填入你的真实凭据值
   ```
   
   b. 或直接在环境中设置变量:
   ```bash
   export SECURE_1PSID="你的凭据值"
   export SECURE_1PSIDTS="你的凭据值"
   ```

3. 在项目根目录运行:
```bash
docker-compose up -d
```

服务将在 http://localhost:8000 上运行

### 使用Dockerfile

1. 构建Docker镜像:
```bash
docker build -t gemini-api .
```

2. 运行容器并传入环境变量:
```bash
docker run -p 8000:8000 -e SECURE_1PSID="你的凭据值" -e SECURE_1PSIDTS="你的凭据值" gemini-api
```

## API端点

- `GET /`: 服务状态检查
- `GET /v1/models`: 获取可用模型列表
- `POST /v1/chat/completions`: 与模型聊天 (类似OpenAI接口)