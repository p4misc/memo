## IISのインストール

[Visual Studio を使用した ASP.NET Web 配置](https://docs.microsoft.com/ja-jp/aspnet/web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis)の記事を参考にします。

1. [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)を入手してインストールします。

2. [コントロールパネル] > [プログラム] > [Windowsの機能の有効化または無効化]を開きます。  
   ![IIS_Config01.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/IIS_Config01.png)

3. [インターネット インフォメーション サービス] > [World Wide Web サービス] > [アプリケーション開発機能] > [ASP.NET 4.8]を有効にします。  
   [インターネット インフォメーション サービス] > [Web 管理ツール] > [IIS 管理コンソール]を有効にします。  
   [OK]を押すと有効にした機能がインストールされます。  
   ![IIS_Config02.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/IIS_Config02.png)

4. [コントロールパネル] > [システムとセキュリティ] > [管理ツール]を開きます。  
   ![IIS_Config03.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/IIS_Config03.png)

5. [インターネット インフォメーション サービス (IIS) マネージャー]をダブルクリックします。  
   ![IIS_Config04.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/IIS_Config04.png)

6. [アプリケーション プール]を選択して表示される[DefaultAppPool]のバージョンが[v4.0]であることを確認します。  
   [DefaultAppPool]を選択して、[基本設定...]をクリックします。  
   ![IIS_Config05.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/IIS_Config05.png)

7. [アプリケーション プールの編集]ダイアログボックスで、[.Net CLR バージョン]を[.Net CLR バージョン v4.0.30319]に変更します。
   [OK]を押します。
   ![IIS_Config06.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/IIS_Config06.png)


## MySQLのインストール

[UGS Reference](https://docs.unrealengine.com/en-US/Programming/Deployment/UnrealGameSync/Reference/index.html)の記事を参考にします。

1. [MySQL Installer](https://dev.mysql.com/downloads/installer/)を入手してインストールします。

2. [Choosing a Setup Type]で、[Server only]を選択して次に進みます。  
   ![MySQL_Config01.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/MySQL_Config01.png)

3. [Path Conflicts]では、何も変更せずに次に進みます。
   ![MySQL_Config02.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/MySQL_Config02.png)

4. [Installation]では、[Execute]をクリックします。  
   ![MySQL_Config03.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/MySQL_Config03.png)

5. [Product Configuration]では、単に次に進みます。
   ![MySQL_Config04.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/MySQL_Config04.png)

6. [High Availability]で、[Standalone MySql Server]を選択します。  
   ![MySQL_Config05.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/MySQL_Config05.png)

7. [Type and Networking]で、[Config Type] > [Server Computer]を選択します。  
   ![MySQL_Config06.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/MySQL_Config06.png)

8. [Authentication Method]で、[Use Strong Password Encryption for Authentication (RECOMMENDED)]を選択します。  
   ![MySQL_Config07.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/MySQL_Config07.png)

8. [Authentication Method]で、[Use Strong Password Encryption for Authentication (RECOMMENDED)]を選択します。  
   ![MySQL_Config07.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/MySQL_Config07.png)

9. [Account and Roles]で、Rootアカウントのパスワードを設定します。   
   ![MySQL_Config08.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/MySQL_Config08.png)

10. 続けて[Add User]をクリックしてサービスアカウントを作成します。  
   ここで作成するアカウントの[User Name]と[Password]は、MetadataServerへの接続に使用します。  
   ![MySQL_Config09.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/MySQL_Config09.png)

11. アカウントが追加されたことを確認します。
   ![MySQL_Config10.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/MySQL_Config10.png)

12. [Windows Service]では、単に次に進みます。
   ![MySQL_Config11.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/MySQL_Config11.png)

13. [Apply Configuration]では、[Execute]をクリックします。  
   ![MySQL_Config12.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/MySQL_Config12.png)

14. 最後に[Finish]をクリックして[Product Configuration]を終了します。
   ![MySQL_Config13.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/MySQL_Config13.png)

15. 次へ進みます。
   ![MySQL_Config14.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/MySQL_Config14.png)

16. [Installation Complete]で、[Finish]をクリックしてインストールを終了します。  
   ![MySQL_Config15.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/MySQL_Config15.png)
