# 跟我寫 JPEG 解碼器

## 緣起
幾年前曾用 C++ 寫過一次 JPEG 解碼器，還記得當時網路上對 JPEG 格式的介紹都雜亂無章、少東缺西，而標準書爲求完整嚴謹，寫的是又臭又長。就沒有讓我趕快寫完作業的法子嗎？最後我在 github 上撈到了一份 python 寫的解碼器，透過 trace 這份程式碼，才好不容易地把網路文章寫的不清楚的地方弄懂了。

我在寫作本文時，特地又搜尋了一次網路文章，居然找到了一篇[簡體文章](https://www.jianshu.com/p/c4ab7f92d0e1)，寫得挺詳細的，有點打亂了我的寫作計劃，但最後還是決定挑戰看看，用自己的風格來講述一次。

如同前述，已經存在將標準書內容成功簡化的好文章了，因此我這次着重在實作上，**希冀讀者只要跟着本文的腳步，就能夠最快的打造出自己的 JPEG 解碼器**。此外，我也會在邊寫作本文邊再次實作 JPEG 解碼器的過程中，實作一些能協助除錯的小工具，一併開源讓讀者使用。

如果還有時間，我也會嘗試撰寫一份 JPEG 的理論基礎，畢竟，能夠實作算法，並不代表理解了算法的原理，我當年便是如此，寫完了，但卻感覺沒學到什麼。而理論方面的文章還很缺乏，我願做先鋒，雖千萬人吾往矣。

## 章節說明

爲了讓讀者有種過關斬將，一直有進度的感覺，也爲了便於閱讀，我將會把整套解碼過程切割成五個章節，還有一章附錄講解 JPEG 的理論基礎。

- （一）概述：簡介 JPEG 解碼流程、
- （二）簡介 JPEG 檔案結構，並讀取部分標頭檔
- （三）讀取、建立霍夫曼表格
- （四）讀取壓縮圖像數據
- （五）解碼
- （附錄一）理論基礎

## 配套程式碼

### 前置準備

- 本配套程式碼以 rust 撰寫，請先安裝 [rust 工具鏈](https://www.rust-lang.org/tools/install)。
- 安裝 libsdl2 ，通常可在發行版的套件管理器找到

### 下載程式碼
``` sh
git clone https://github.com/MROS/jpeg_tutorial
```

### 執行
``` sh
cd jpeg_tutorial
cargo run XXX.jpg           # 解碼並顯示 jpg 檔
cargo run XXX.jpg --marker  # 於標準輸出打印 jpg 檔的標記碼
```

### 幫助

想看本程式的更完整資訊，可以
```
cargo run -- --help
```
