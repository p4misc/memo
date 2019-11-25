# UnrealGameSyncのビルドメモ



## 使用したコンパイラ

Visual Studio 2017 Community Version 15.9.17



## ビルド手順

以下の手順でビルドします。

1. git clone https://github.com/EpicGames/UnrealEngine/ を実行
2. UnrealEngine\Setup.batを実行
3. Microsoft .NET Framework 4.6.2 Developer Packをインストール
4. UnrealEngine\Engine\Source\Programs\UnrealGameSync\UnrealGameSync.slnを開く
5. [ツール] > [NuGet パッケージ マネージャー] > [パッケージ マネージャー コンソール]を実行
   - コンソール内で次のコマンドを実行
     ```bash
     Install-Package WiX -Version 3.8
     ```
6. [プロジェクト] > [参照の追加] > [参照]にて次のDLLを選択
   - UnrealEngine\Engine\Source\Programs\UnrealGameSync\packages\WiX.3.8\tools\Microsoft.Deployment.WindowsInstaller.dll
7. UnrealGameSyncソリューション全体をビルド
