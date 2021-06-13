# CNN_Nogizaka46
## 【ライブラリ】

- ### <Nogizaka_Scraping_byChrome>
    - selenium
    - chromedriver_binary : ChromeDriver をダウンロードせず使用できる.
    - beautifulsoup
    - lxml
    - urllib
    - requests

- ### <Remake_Pic>
    - opencv-python


## 【流れ】

    1. 名前別で画像スクレイピング

    2. 画像を 顔識別加工

    3. 手動で選別をする （選別前のフォルダはない)

    4. テスト用データ(20%) , 訓練用データ前データ(80%) に分ける

    5. 訓練用データを作成 (角度を変え,閾値・ぼかし・オリジナル) , データ量が前データの 9倍 になる




## 【画像枚数】

- スクレイピング Pic 
    白石 : 283 , 斎藤 : 306 , 山下 : 236 , 西野 : 290 , 生田 : 248
    
- 顔識別+選別 face
    白石 : 174 , 斎藤 : 175 , 山下 : 123 , 西野 : 163 , 生田 : 177
    
- 訓練用データの元データ face_after
    face * 0.8 (80%)
    
- テストデータ test
    face * 0.2 (20%)
    
- 訓練用データ train
    face_after * 3(角度) * 3(オリジナル・閾値・ぼかし) 




## 【詰まったところ】

- ### <Nogizaka_Scraping_byChrome>
    - Google 画像検索のパラメータ (顔)
    - ライブラリ chromedriver_binary の役割
    - Chrome のバージョン違い → 使っている Chrome のバージョンを上げる
    - for j, src in enumerate(srcs):　からはコピペ.内容を理解できていな

- ### <Remake_Pic>
    - cv2 のインストールするときのライブラリ名が opencv-python
    - 同じ階層のでディレクトリ
        - Test → × , ./Test → ○
    - 保存用ファイル(プログラムで作成)と,加工後画像を保存させるファイル名の違い
    - 顔検出用のファイル haarcascade_frontalface_default.xml を github からダウンロード.
    - github → 保存したいファイル → raw → URLコピー → ターミナル →  cd ~~~ → wget URL
    - 保存するディレクトリに注意 cascade = cv2.CascadeClassifier("デイレクトリ")
    - 顔検出後の画像を選別し, face_after に順番をつけ直して保存
    - 一つのみフォルダ作成 : os.mkdir()
    - 階層型のフォルダ作成 : os.makedirs()


- ### <devide_test_train>
    - テスト用に画像を分けるとき,実行するたびにテスト用画像が増加し,訓練用データは減少する
    - os.path.join("/A/B/C", "file.py"))   # /A/B/C/file.py

- ### <Make_traindates>
    - in_jpg=glob.glob(in_dir) : フォルダ内要素全ての ディレクトリ を抜き出す リスト型
    - 回転させてから オリジナル・閾値・ぼかし の処理を行うこと.効率よく加工できる.
    - 加工のライブラリ , 関数 , 引数
    - データを引き出す・保存するときの path




- ### <learn>
    - history.history の中身が acc → accuracy , val_acc → val_accuracy に変更
    - print(history.history) で確認できる
