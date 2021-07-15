# Tips for comfortably using Jetson Nano  

## Reconfigure used micro SD card  
balenaEtcher で OS Image を焼いた マイクロ SD カードを再度初期化して OS Image を焼く場合、Windows でやろうとすると、ディスク管理で非常にたくさんのパーティションを削除しなければならず、とっても煩雑なので、Jetson Nano（Raspberry Pi も同様）上で初期化すると手間が省ける。  
Jetson Nano に SD カードリーダーを USB 接続して、以下のコマンドを実行  
```sh
sudo fdisk /dev/sda
```
d コマンドで順番に 2-12 の /dev/sda <i>n</i> を削除していく

---
## Run modules on SSD - How To  
Jetson Nano に SSD を接続して、その上で動くようにすると、体感的に爆速になる。  
SSD で Boot する環境の作成は、  
- https://www.miki-ie.com/nvidiajetsonnano/nvidia-jetson-nano-usb-root/  

ここに記載の通りにやればいい  

---
