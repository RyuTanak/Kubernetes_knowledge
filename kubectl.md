# kubectlとは  

yamlやコマンドをAPIリクエストに変えてapi-serverにHTTPリクエストを送る  

## kubectlの構文  

構文  

[リファレンス](https://kubernetes.io/ja/docs/reference/kubectl/overview/)  

kubectl [command] [TYPE] [NAME] [flags]  

- command:実行したい操作（get,create,patch,delete）  
- TYPE:リソースのタイプ（pod,node,service,deployment）  
- NAME:リソース名  
- flags:オプションのflag(--kubeconfigなど)

## リソースタイプ  

構文のTYPEにはどのようなモノが入るか  

kubectl api-resources  
カラムの紹介  
![image](./image/1.png)  

## 出力フォーマット  

kuebctl [command] [TYPE] [NAME] -o <output_format>  

![image](./image/2.png)  