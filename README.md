# 通常要先讓docker啟動載入全部的套件才能下載poetry

docker build -t my-poetry-app .

docker run -it --rm -v ${PWD}:/app my-poetry-app bash

# 先創poetry

要使用 Poetry，你本機必須先安裝好 Python

poetry init

poetry add pandas nump 先裝才有poetry.lock

----------------------------------------------------------------------------------------------

poetry.lock 檔案不匹配，Poetry 提示你需要重新生成 poetry.lock 檔案。

解決方案：

在本地執行 poetry lock 來更新 poetry.lock 檔案：

poetry lock

# 小總結（重點流程快速版）

docker build -t my-poetry-app .

docker run -it --rm -v ${PWD}:/app my-poetry-app bash

# 進容器後

poetry init

poetry add pandas numpy

poetry lock
