Github-Docker
username: ipiaotu


//管理员终端

Login Succeeded

你现在要做的就两步：
在仓库 Settings → Secrets and variables → Actions 里，确认并保存好：
Variable DOCKER_USERNAME = 你的 Docker Hub 用户名（和网站上一致）
Secret DOCKERHUB_TOKEN = 你在 Docker Hub 生成的 PAT
回到 Actions 页面，手动重新运行一次这个 workflow（或向 main 分支再推一次提交），看日志确认
登录成功、镜像推送成功。

//想进目录要用 cd，不能直接敲路径：
  cd docker-demo\.github\workflows
返回上一级目录用：
  cd ..
而不是 ../（那是 Linux shell 的写法，在 PowerShell 里要加 cd）。

ping github.com

//网络正常时再推

Dockerfile路径目录:
 dir -Recurse -Filter Dockerfile


    目录: C:\Users\漂土\--\docker-demo


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----         2026/1/16      0:16             82 Dockerfile

//JSON文件中不允许有注释

终端中 Ctrl + C 停掉服务。

构建推送镜像:

当前 Dockerfile 已经是：
FROM node:20-alpineWORKDIR /appCOPY . .RUN npm installCMD ["npm", "start"]
有了 package.json 和 index.js，这份 Dockerfile 就是合法的了。
可以本地先试一下构建：
docker build -t test-root-app .docker run --rm -p 3000:3000 test-root-app
确认容器里也能访问 http://localhost:3000。

//index.js:
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello from docker-demo root app!漂土');
});

const port = process.env.PORT || 3000;
app.listen(port, () => {
  console.log(`Server listening on port ${port}`);
});

//package.json:
{
  "name": "docker-demo-root-app",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  }
}

让构建上下文指向 docker-demo 子目录

关键是这两行：
context: ./docker-demo
file: ./docker-demo/Dockerfile

//PUSH最新后ACTION,BUILD绿色! 
//ci add root node app

/*屏幕报错不够用, Cursor编写,删除错误预警再上传*/
