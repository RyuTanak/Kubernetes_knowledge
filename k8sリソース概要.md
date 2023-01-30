## Podの概要  

podとは  
Kubernetes上のデプロイの最小単位  

Dockerのデプロイ上の最小単位→コンテナ  
Kubernetes上のデプロイの最小単位→pod  

podは  
- 1つまたは複数のコンテナを持つ  
  →コンテナを複数持つことは基本的にはない  
    例えば、主コンテナのアプリケーションのログをサブコンテナが読み込む場合とか  
- 同一pod内では、ネットワークやストレージを共有リソースとして持つ  

## podを使って動かしてみる  

ファイルを使ったpod起動  
```
kubectl create -f pod.yml 
```
podが出来たことの確認  
```
kubectl get pod
```

イメージを使ったpod作成　　
```
kubectl run nginx --image=nginx
```

どちらもpodを作成できる  
作成自体は簡単であるが、設定できることが色々ある。  
設定の中を見てみるコマンド　　
```
kubectl get pod nginx -o jsonpath='{.spec}' | jq
```
「jp」はJSONを見やすくするコマンド  

設定をファイルに書き出すコマンド  
```
kubectl get pod nginx-yaml -o yaml > nginx-yaml.yaml
```


## kubernetesオブジェクト  

クラスタの状態を表現する  
- どんなコンテナアプリケーションが動いているか  
- 利用可能なリソースはどれだけか  
- アプリケーションの振る舞いに関するポリシー  

Podの作成＝Kubernetesオブジェクトを作成  
→？？？  

1つのクラスター内に存在するpodやnode＝kubernetesオブジェクト  
![image](./image/4.png)  



