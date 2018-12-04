基本```sudo```  

アプリをビルドする  
```docker build -t friendlyhello .```

アプリを起動させる(-d でバックグラウンド)  
```docker run -d -p 4000:80 friendlyhello```

起動中のコンテナ確認  
```docker container ls```  
すべてのコンテナ確認  
```docker container ls -a ```

コンテナのプロセス停止(ハッシュはコンテナID)  
```docker container stop 1fa4ab2cf395```

imageにタグを付ける  
```docker tag image username/repository:tag```  
```docker tag friendlyhello utaudeboo/hogehoge:part1```

imageをリモートリポジトリに公開する  
```docker push username/repository:tag```


リモートリポジトリからイメージを引き出して実行する  
```docker run -p 4000:80 username/repository:tag```

コンテナを削除する  
```docker container rm 1fa4ab2cf395```

imageを削除  
```docker rmi 1fa4ab2cf395```

Dockerfile からimageを作成  
```docker build . -t hoge/fuga:1.0```

イメージを実行(イメージをもとにコンテナを立ち上げる)  
```docker run -it hoge/fuga:1.0 /bin/bash```  
-t と -i の２つのフラグも付けました。-t フラグは、新しいコンテナの中に疑似ターミナル (pseudo-tty) を割り当てます。-i フラグは双方向に接続できるようにするため、コンテナの標準入力 (STDIN)を取得します。

コンテナを立ち上げるときにホストのvolディレクトリをdockerにマウントさせる  
```docker run -it --rm -p 5000:5000 -v $(pwd)/vol:/home hoge/fuga:1.0 /bin/bash```  
-pはコンテナのポートをホスト側に公開するオプション
```
practicing_django
 |-Dockerfile
 `-vol
    `-app.py
```
例

```shell
ytmbp:src yukihiro$ pwd
/Users/yukihiro/practicing_django/src
ytmbp:src yukihiro$ cd ..
ytmbp:sudo docker run -it -p 8000:8000 -v /Users/yukihiro/Documents/practicing_django/vol:/home/vol django_tutorial:latest /bin/bash
```

djangoサーバーを立ち上げる  
-> ubuntuコンテナ内で実行
```python
cd /home/vol
django-admin startproject mysite
cd mysite
python3 manage.py runserver 0:8000
```
下記アドレスにアクセス  
http://localhost:8080/
