# Kubernetes学習  

[参考github](https://github.com/nakamasato/kubernetes-basics/tree/v2.0)  

## Kubernetesで出てくる単語  

- Desired State(理想状態)  
- pod  
- Control Plane  
- kubelet  
- Worker  

## Kubernetesとは  

コンテナ化したアプリケーションのデプロイ、スケーリング、及び管理を行うための  
オープンソースのコンテナオーケストレーションシステム  

## Architecture  

- Worker Node  
  コンテナが実行されるマシン  
  Container runtimeがインストールされている必要がある  
  中身  
  - kubelet  
     Control Planeと疎通をするためのエージェントとなる  
  - k-proxy(クーベープロキシ)  
     ノードのネットワークの管理  

- Control Plane(マスター)  
  Worker Nodeの状態を保持・管理  
  中身（かっこよく言うとコンポーネント）5つ  
  - api  
    内部のやり取りをするAPIサーバ  
    Workerのkubletとやり取りを行う  
  - etcd  
    Kubernetes Clusterの状態を保存しておくためのKey-Valueストアのデータベース  
  - sched(クーベスケジューラー)  
    アプリケーションをどのWorker Nodeで実行するのかをスケジュールする  
  - controler-manager(クーベコントローラマネージャ)  
    理想状態と現状を比較し違いがあれば理想状態に近づけようとするもの  
  - cloud-control-manager  
    cloud APIと連携  

  - kubectl  
    kubeAPIサーバへの操作コマンドを実行するもの  

- Kuberbetes Cluster  
  上のWorker NodeとControl Planeを併せてKubernetes Clusterという  




