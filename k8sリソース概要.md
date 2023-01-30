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


Kubernetesオブジェクトのフィールド  
このフィールドというのは2つあり
- spec: 理想状態(desired state)  
  - kubectlやプログラムにより変更する  
  - 例、kubectl apply -f pod.yaml  
- status: 現実状態(current state)  
  - Kubernetesにより更新される  

コントロールプレーンは、理想状態と現実状態が一致するように管理  

### Kubernetesオブジェクト作成に必須の情報（4つ）  
- apiVersion: どのバージョンのKubernetes APIかを指定する  
  例 v1  

- kind: どの種類のオブジェクトか  
  例 Pod,Deployment  

- metadata: オブジェクトを一意に識別する情報  
  例 name.,UID,namespace  

- spec: 理想状態  
  内容はオブジェクトごとに異なる  

pod作成時の例  
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-yaml
spec:
  containers:
    - image: nginx
      name: nginx
```

### Namespace  

リソースの一つ  
同一の物理クラスター上で複数の仮想クラスターの動作をサポートする。  
この「仮想クラスター」のことをNamespaceという。  

仮想クラスタとは、実際には同じマシン上で動いているかもしれないが、仮想的に環境が分けられている状態  


### 2種類のリソース：Namespace vs Cluster  

- Namespace-scoped リソース：  
  Namespaceに属しているリソースで、Namespace削除時には削除される  
  Namespace内で名前はUniqueである必要がある   
- Cluster-scoped リソース：
  Namespaceに属していないリソース  
  クラスタ全体で使われるもの  
  クラスタ内で名前はUniqueである必要がある  

### Namespaceのコントロール  

- Namespaceの作成・削除  
  kubectl create/delete namespace <Namespace名>  
- ある特定のNamespaceのオブジェクトを操作する  
  kubectl [command] [TYPE] --namespace <Namespace名> or -n <Namespace名>  


