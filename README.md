# 通常要先讓docker啟動載入全部的套件才能下載poetry

docker build -t my-app .

docker run

# 先創poetry

要使用 Poetry，你本機必須先安裝好 Python

poetry init

poetry add pandas numpy 先裝才有 

poetry.lock

----------------------------------------------------------------------------------------------

更新 poetry.lock 檔案：

poetry lock

# 小總結（重點流程快速版）

docker build -t my-app .

docker run my-app

# 進容器後

poetry init

poetry add pandas numpy

poetry lock

# 要進入一個已執行中的 Docker 容器指令：

docker exec -it my-app /bin/bash
