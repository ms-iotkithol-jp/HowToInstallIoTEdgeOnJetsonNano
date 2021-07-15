# How to Migrate from LVA on Edge to AVA on Edge  
既に、Live Video Analytics on Edge がインストールされた Jetson Nano 環境を Azure Video Analyzer on Edge に移行したい場合、以下の手順に従うと比較的簡単に移行できます。  

https://docs.microsoft.com/azure/azure-video-analyzer/video-analyzer-docs/get-started-detect-motion-emit-events-portal#preparing-your-iot-edge-device で紹介されている、https://aka.ms/ava/prepare-device を、Jetson Nano の Shell 上で以下のコマンドを実行して、一旦、ダウンロードします。  
```sh
curl -L https://aka.ms/ava/prepare-device -o prepare-device.sh
chmod u+x prepare-device.sh
```

ダウンロードしたファイルの中で、ユーザーとユーザーグループを登録するようになっているが、ID が Live Video Analytics on Edge で追加したユーザー・ユーザーグループの ID と同じなので、prepare-device.sh で ID を指定している部分を書き換えます。  

```sh
# create the local group and user for the edge module
# these are mapped from host to container in the deployment manifest in the desire properties for the module
sudo groupadd -g 1020 localedgegroup
sudo useradd --home-dir /home/localedgeuser --uid 1020 --gid 1020 localedgeuser
sudo mkdir -p /home/localedgeuser
```  

上の例では、オリジナルで <b><u>1010</u></b> となっている箇所を、<b><u>1020</u></b> に変えています。  

https://docs.microsoft.com/azure/azure-video-analyzer/video-analyzer-docs/get-started-detect-motion-emit-events-portal#deploying-video-analyzer-edge-module の <b><u>14</u></b>、<b><u>15</u></b> で環境変数としてユーザー・ユーザーグループを設定するので、変更した値を入力します。上の例では <b><u>1020</u></b> です。  

Azure Video Analyzer をデプロイする IoT Edge は、Live Video Analytics on Edge をインストールしていた IoT Edge の再利用（この場合は、"Set Modules" で Live Video Analytics on Edge モジュールを削除する事）でもいいし、新しく IoT Edge を一つ作成して、/etc/iotedge/config.yaml もしくは、/etc/aziot/config.toml の接続情報を書き換えるのでもよい。  

## 附記  
Azure Video Analyzer 用の VS Code Extesion も公開されているので、パイプラインのオーサリングの便利ツールとして活用いただきたい。その場合は、Live Video Analytics on Edge 用の Extension のアンインストールが必要。  
