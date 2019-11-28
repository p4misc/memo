## IISのインストール

1. [ここ](https://docs.microsoft.com/ja-jp/aspnet/web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis)を参考にします。
2. [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)を入手してインストールします。
3. [コントロールパネル] > [プログラム] > [Windowsの機能の有効化または無効化]を開きます。
   1. [インターネット インフォメーション サービス] > [World Wide Web サービス] > [アプリケーション開発機能] > [ASP.NET 4.8]を有効にします。
   2. [インターネット インフォメーション サービス] > [Web 管理ツール] > [IIS 管理コンソール]を有効にします。
   3. [OK]を押すと有効にした機能がインストールされます。
4. [コントロールパネル] > [システムとセキュリティ] > [管理ツール]を開きます。
   1. [インターネット インフォメーション サービス (IIS) マネージャー]をダブルクリックします。
   2. [アプリケーション プール]を選択して表示される[DefaultAppPool]のバージョンが[v4.0]であることを確認します。
   3. [DefaultAppPool]を選択して、[基本設定...]をクリックします。
   4. [アプリケーション プールの編集]ダイアログボックスで、[.Net CLR バージョン]を[.Net CLR バージョン v4.0.30319]に変更します。
   5.  [OK]を押します。



## MySQLのインストール

1.  [ここ](https://docs.unrealengine.com/en-US/Programming/Deployment/UnrealGameSync/Reference/index.html)を参照
2. [MySQL Installer](https://dev.mysql.com/downloads/installer/)を入手してインストールします。
3. [Choosing a Setup Type]で、[Server only]を選択します。
4. [High Availability]で、[Standalone MySql Server]を選択します。
5. [Type and Networking]で、[Config Type] > [Server Computer]を選択します。
6. [Authentication Method]で、[Use Strong Password Encryption for Authentication (RECOMMENDED)]を選択します。
