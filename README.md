# Docker 常用指令

## 1. 建構與運行容器

# 構建映像
docker build -t <image_name> .

# 運行容器
docker run -d <image_name>

# 運行並映射端口
docker run -d -p <host_port>:<container_port> <image_name>

# 為容器指定名稱
docker run --name <container_name> <image_name>

# 運行並掛載本地資料夾到容器
docker run -v /local/path:/container/path <image_name>

# 容器停止後自動刪除
docker run --rm <image_name>

## 2. 容器管理

# 查看運行中的容器
docker ps

# 查看所有容器（包括停止的）
docker ps -a

# 停止容器
docker stop <container_id_or_name>

# 刪除容器
docker rm <container_id_or_name>

# 進入容器內部
docker exec -it <container_id_or_name> /bin/bash

## 3. 映像管理

# 列出本地所有映像
docker images

# 刪除映像
docker rmi <image_name>

# 標籤映像
docker tag <image_name> <new_image_name>

## 4. 推送與拉取映像

# 將映像推送到 Docker Hub 或其他遠端註冊中心
docker push <image_name>

# 從 Docker Hub 拉取映像
docker pull <image_name>

## 5. 查看與診斷

# 查看容器日誌
docker logs <container_id_or_name>

# 查看容器詳細信息
docker inspect <container_id_or_name>

## 6. 清理操作

# 刪除所有停止的容器
docker container prune

# 刪除所有未標記的映像（dangling images）
docker image prune

# 刪除所有未使用的資源（容器、網絡、映像等）
docker system prune
