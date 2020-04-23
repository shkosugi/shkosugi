# Windows10デバイスで、Intuneの登録制限（SIMなしのPC）

IntuneでBYODの利用を禁止し、会社支給デバイスのみ利用させたいという要件はよくあるかと思います。
この場合Intuneの登録制限機能を利用し、デバイスのシリアル番号を事前登録したデバイスだけ登録できるよう制御が可能です。
https://docs.microsoft.com/ja-jp/mem/intune/enrollment/corporate-identifiers-add

ただこの方法はWindowsPCではIMEI番号がある（＝SIMカード対応）の場合しか使えず、なかなか実際には難しい、というのがこれまでの通説でした。
しかしながらAutoPilotの機能を利用することにより、SIMなしのPCでも同様に指定したデバイスだけIntuneに登録可能とする方法がありますのでご紹介します。

## 準備

1) [Intune 管理ダッシュボード](https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade/) に全体管理者でサインインします
2) [デバイスの登録] - [Windows の登録] - [登録制限] をクリックします
3) [作成の制限] - [デバイスの種類の制限] をクリックします
4) 適当な名前を入力し、[次へ] をクリックします
5) 「Windows (MDM)」の「個人所有」を「ブロック」に変更し、[次へ] をクリックします
6) 検証ユーザーが含まれるグループを指定し、[次へ] をクリックします
7) [作成] をクリックします
  
## デバイスの登録
1) 登録したいデバイスのAutoPilot情報を取得します。詳細な手順は以下のぺーjが詳しいです。
https://qiita.com/Gikill/items/d821b455c90800c3b598

2) [Intune 管理ダッシュボード](https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade/) に全体管理者でサインインします

3) [デバイスの登録] - [Windows の登録] - [Windows AutoPilot Deployment プログラム] - [デバイス] をクリックします

4) [インポート] をクリックし、手順１でエキスポートしたCSVファイルを読み込みます。
読み込み完了まで10分適度かかりますので、しばらく待ちます。　

5) デバイスをAAD登録します。ここで登録済みのPCは登録に成功しますが、そうでないデバイスはエラーになります
