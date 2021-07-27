<Title>私のポートフォリオ</Title>

# 自己紹介
* ### 氏名 
    黒川　聖人（くろかわ　まさと）

* ### 所属
    河原電子ビジネス専門学校　ゲームクリエイター科　2年
    
<br></br> 

# 制作タイトル
* ### **BurgerPicker**  
    <br>
    <iframe width="600" height="370" src="https://www.youtube.com/embed/-KODHGPx7LI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br></br>

# ゲーム概要
### **BurgerPicker**  
* OverCookedを参考にした、2人対戦型ハンバーガー作成ゲームです。  
メビウスの輪状のコンベアに流れているハンバーガーの具材を取り、キッチンでメニュー通りのハンバーガーを作成します。  
メニューの制限時間内に正しいハンバーガーを提供しスコアを獲得します。  
最終的にどちらのプレイヤーが多くスコアを獲得できたかで勝敗を決めます。  
<br>


* ### 使用ゲームエンジン
    改造した学校ゲームエンジン  
<br>
* ### 使用言語  
    C++  
<br>
* ### 使用ツール  
    Visual Studio 2019  
    Effekseer  
<br>
* ### 使用ライブラリ  
    DirectXTK  
<br>
* ### 環境
    Windows10  
    DirectX12  
<br>
* ### 制作人数
    3人  
<br>
* ### 制作期間
    2021年2月～現在

<br></br>

# 目次
1. ### [**操作説明**](#Operation)
2. ### [**川瀬式ガウシアンブラー**](#GaussianBlur)
3. ### [**AOマップ**](#AOMap)
4. ### [**デプスシャドウ**](#DepthShadow)
5. ### [**被写界深度**](#DepthInView)  
6. ### [**PBR (Physically based rendering)**](#PBR)  
7. ### [**ディファードレンダリング**](#Deffered)

<br></br> 



<a id = 'Operation'></a>

# 1. 操作説明

![Operation](https://user-images.githubusercontent.com/54493763/126964230-02dca9ea-6da9-42c4-af7f-9b0ed3c606f1.png)


<a id = 'GaussianBlur'></a>

# 2. **川瀬式ガウシアンブラー**
![Burger](https://user-images.githubusercontent.com/54493763/126972389-5f797183-dbae-426e-bd7a-73c8f2b3a5be.png)  
今回はハンバーガーだけにガウシアンブラーをかけたいので、ハンバーガーのみを描画します。  
以下が、ガウシアンブラーを掛けたもので、ブラーがかかったものにさらにブラーを掛けています。  
最終的に
<span style="color: #ff0000; ">計4回</span>
のブラーが重ね掛ったものを用意しました。
<br>

![Blur_1](https://user-images.githubusercontent.com/54493763/126969972-63c8ca47-fb00-4d52-9b3a-c32ce21f765d.png)
![Blur_2](https://user-images.githubusercontent.com/54493763/126969975-5ad46a86-063e-429c-b7c2-906386308fc8.png)  
&emsp;&emsp;&emsp;&emsp;&ensp;
ブラー1回目
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;
ブラー2回目
<br>

![Blur_3](https://user-images.githubusercontent.com/54493763/126969976-7c659bc7-0609-48c0-a09f-381007c2471c.png)
![Blur4](https://user-images.githubusercontent.com/54493763/126969978-e153d724-069c-4c07-8ba5-03d15eb3ba8f.png)  
&emsp;&emsp;&emsp;&emsp;&ensp;
ブラー3回目
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;
ブラー4回目
<br>

ガウシアンブラーがかかった画像が計4枚できたところで、全てのブラー画像を合成し、画像の枚数（4）で除算しました。  
出来上がった1枚の画像と通常描画の画像を合成することでガウシアンブラーのかかった最終の画像を作成しました。

![Burger_Normal](https://user-images.githubusercontent.com/54493763/126969981-55873f4c-9744-4a5c-a9e0-f20c475e9d1b.png)
![Burger_Blur](https://user-images.githubusercontent.com/54493763/126969979-01bc583f-77fd-4dee-a638-e8251fa6345b.png)  
&emsp;&emsp;&emsp;&emsp;&emsp;
通常描画
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;
ブラー適用
<br></br>



<a id = 'AOMap'></a>

# 3. **AOマップ(実装方法違う可能性あり）**

<a id = 'DepthShadow'></a>

# 4. **デプスシャドウ**
![ProjectionShadow](https://user-images.githubusercontent.com/54493763/126988196-c52b6880-4acc-4776-8456-cef47c37b7e2.png)  
上の画像は投影シャドウマップを利用した影生成です。
分かりやすいように、特別にシャドウキャスターの上に板を設けて、影が映ってしまっている状況を確認しました。
<br>

![DepthShadow](https://user-images.githubusercontent.com/54493763/126988188-f0847d60-f3f9-4fdb-9c2c-5ed41dbdfda5.png)  
上の画像は深度を利用したデプスシャドウマップです。  
板には影が映っていないことが確認できます。  　
<br>


![UsingDepthShadow](https://user-images.githubusercontent.com/54493763/126989459-a776aab6-097b-45f3-8ef4-b622e16d403a.png)  
このゲームでは、具材の位置が上下になる箇所があります。  
上の具材に不自然な影が映ってしまわないようにするために役立っています。
<br></br>


<a id = 'DepthinView'></a>

# 5. **被写界深度**

![DepthInView ](https://user-images.githubusercontent.com/54493763/126992452-1b251d8b-b5f0-490b-9a4c-20c330351787.png)
![NonDepthInView ](https://user-images.githubusercontent.com/54493763/126992454-5208edbc-6062-455d-bdd6-cda18cc4f12d.png)  

&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;
通常描画
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;
被写界深度適用
<br></br>
左の画像が通常のゲーム画面です。右の画像が被写界深度を取り入れたゲーム画面です。  
<br></br>


<a id = 'PBR'></a>

# 6. **PBR (Physically based rendering)**
![nonPBR](https://user-images.githubusercontent.com/54493763/127108852-03125eda-be3e-4188-9573-6e199fa3729a.png)
![PBR](https://user-images.githubusercontent.com/54493763/127108847-204b00cb-e6b7-4284-8151-9e253cc681a6.png)
  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;
PBR非適用
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;
PBR適用
<br></br>
光を受ける物体の法線やライトから物体へのベクトル、カメラから物体へのベクトルを用いて光の影響度、鏡面反射率を計算しました。  
物体の窪んでいる部分など、何も工夫せずに描画したものと、PBRを用いて描画したものを比較するとかなりのビジュアルの向上が確認できました。
<br></br>
<a id = 'Deffered'></a>

# 7. **ディファードレンダリング（未完成）**


<!-- 
<details><summary>aaaa</summary>\
aaaaaa\
</details>\
これは<span style="color: #ff0000; ">赤文字</span>です\
-->