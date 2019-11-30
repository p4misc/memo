# UnrealGameSyncのMetadataServerの構築方法に関するメモ

このメモではMetadataServerの構築方法を紹介します。  
UnrealGameSyncの枠組みは下図を参照してください。

## UnrealGameSyncの枠組み

![IIS_Config01.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/UnrealGameSyncOverview.png)

## 各種バージョン
- OS: Windows 10 Pro 1903
- UE4: 4.23.1
- IIS: 10.0.18362.1
- MySQL: 8.0.18
- .NET SDK: 4.6.2
- Web Platform Installer: 5.0


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


## UnrealGameSyncの設定

1. UnrealGameSync.exeからMetadataServerに接続するために、`DeploymentSettings.cs`のApiUtilに接続先となるMetadataServerのURLを記述します。  
   ![Publish_Config01.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/Publish_Config01.png)

2. UnrealGameSyncプロジェクトをリビルドして、UnrealGameSync.exeをチームメンバに配布します。


## MetadataServerの配備

1. MetadataServerプロジェクトの直下に`Web.Release.config`と`Web.Debug.config`が存在します。  
   配備するMetadataServerのソリューション構成(`Release`/`Debug`)に合わせて一方を`NotForLicensees`ディレクトリに配置します。  
   配置する際に`Web.config`にリネームします。  

2. `Web.config`を編集してMySQLに接続するための接続文字列を入力します。  
   このとき、`UserId`と`password`にサービスアカウントの[User Name]と[Password]を記入します。  
   ```xml
   <connectionStrings>
      <add name="ConnectionString" connectionString="server=localhost;UserId=p4misc;password=xxxxx;" providerName="MySql.Data.Client"/>
   </connectionStrings>
   ```  
　　![Publish_Config02.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/Publish_Config02.png)  

3. MetadataServerノードを右クリックしてコンテキストメニューを開き、[発行]をクリックします。  
　　![Publish_Config03.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/Publish_Config03.png)  

4. 発行ダイアログに[サーバ]、[サイト名]、[宛先 URL]を入力します。  
   入力完了後に[接続の検証]を押して、接続確認をし、[保存]をクリックします。    
　　![Publish_Config04.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/Publish_Config04.png)  

5. 最後に[発行]をクリックすると、IISへの配備が完了します。
　　![Publish_Config05.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/Publish_Config05.png) 
  
6. 配備完了後に http://localhost/MetadataServer/api/latest にアクセスして以下のように表示されればOKです。  
   ```xml
   <LatestData xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.datacontract.org/2004/07/MetadataServer.Models">
     <LastBuildId>0</LastBuildId>
     <LastCommentId>0</LastCommentId>
     <LastEventId>0</LastEventId>
   </LatestData>
   ```

7. 配備成功時のIISマネジャーおよびディレクトリの状態例は下図のとおりです。
　　![Publish_Config06.png](https://github.com/p4misc/memo/blob/master/MetadataServerMemo/Publish_Config06.png)

## 補足

上記の手順では、`DeploymentSettings.cs`や[宛先 URL]に http://localhost/MetadataServer を指定していますが、実際はチームで共有するサーバになりますので、localhostを適切なFQDN / ホスト名 / IPアドレスにする必要があります。

