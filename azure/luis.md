## Language Understanding Intelligence Service

テキストを入力すると、事前に定義した意図(intent)と対象(entity)を推測して返してくれる。  
例えばファイル操作コマンドを定義する場合、以下のようにintentに操作種別、entityに対象を識別するパラメータを設定する。  

intentの例：  
- CreateFile(ファイルを作成)
- DeleteFile(ファイルを削除)

entityの例：  
- FileName(ファイル名)
- Owner(ファイル所有者)
- LastUpdated(最終更新日時)

### URL

https://www.luis.ai/

### 使い方

1. LUISにMicrosoftアカウントでログイン

2. 「New Application」ボタンでApplicationを作成。
  
  名前は任意、「Choose Application Culture」では処理したい言語の種類を選択する。  


3. Entityを定義
  
  作成したApplicationの編集画面に行き、左側のEntitiesの「＋」ボタンをクリックする。

  ![Application編集画面](https://raw.githubusercontent.com/r-stack/tutorial/images/azure/luis_dashboard.JPG)  
  
  ダイアログが出るので、任意の名前を設定してsaveする。

4. Intentを定義  

  1. 左側のIntentsの「＋」ボタンをクリックする。   
  2. ダイアログが出るので、任意の名前と、このIntentをトリガーする例文を入力してsaveする。
  3. New utternances画面に遷移するので、例文中でEntityを示す部分を選択して、「Submit」ボタンで登録する。

5. 例文を登録

  New utternances画面でコマンドの呼び出しに使いそうなフレーズを入力して、「→」ボタンをクリック。  
  文中でEntityを示す部分を選択し、どのIntentを呼び出すためのものか選んで「Submit」ボタンで登録する。  
  これ必要なだけ繰り返す。
  
6. 学習させて公開する  

  1. 画面左下の「Train」ボタンをクリックして、入力した例文やIntent, Entityに基づき学習させる。  
  2. 画面左上の「Publish」をクリックして、作成したApplicationを公開する。
  
