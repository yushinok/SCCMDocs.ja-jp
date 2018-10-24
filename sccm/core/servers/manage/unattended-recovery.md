---
title: 無人回復
titleSuffix: Configuration Manager
description: スクリプトを使用して、Configuration Manager でサイトを回復します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d868411b9e8bce171e8626e5a6ecab6125cc056e
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386033"
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Configuration Manager のサイトの無人回復   

*適用対象: System Center Configuration Manager (Current Branch)*

 Configuration Manager の中央管理サイト、またはプライマリ サイトの[無人回復](/sccm/protect/understand/recover-sites#site-recovery-procedures)を実行するには、無人インストール スクリプトを作成して、setup コマンドに **/script** オプションを付けて実行します。 このスクリプトで、セットアップ ウィザードで入力するのと同じ種類の情報を指定します。ただし、既定の設定はありません。 使用する回復方法に該当するセットアップ キーの値をすべて指定する必要があります。

 /script セットアップ コマンドライン オプションを使用するには、初期化ファイルを作成する必要があります。 次に、/script オプションの後にこのファイル名を指定します。 **.ini** というファイル名拡張子が付いている限り、ファイルの名前は重要ではありません。 コマンド ラインでセットアップ初期化ファイルを指定するときは、そのファイルの完全パスを入力する必要があります。 たとえば、セットアップ初期化ファイルが *setup.ini* という名前で、*C:\setup フォルダー*にある場合、コマンド ラインは 

 `setup /script c:\setup\setup.ini`

> [!IMPORTANT]  
>  セットアップを実行するには、管理者権限が必要です。 無人インストール用スクリプトを指定してセットアップを実行する場合は、**[管理者として実行]** を使用して、管理者コンテキストでコマンド プロンプトを開始します。

 スクリプトは、セクション名、キー名、値で構成します。 セクションの必須キーは、スクリプトを記述している回復の種類によって異なります。 セクション内でのキーの順序、およびファイル内でのセクションの順序は重要ではありません。 キー名の大文字と小文字は区別されません。 キーの値を指定するときは、キー名の後ろに等号 (=) 入力してから、キーの値を続けます。

 次のセクションにある表を、サイトの無人回復用スクリプトを記述するときの参考にしてください。 この表には、スクリプトで指定できるキーとその値、必須かどうかの別、該当するインストールの方法、およびキーの説明が示されています。

## <a name="recover-a-central-administration-site-unattended"></a>中央管理サイトの無人回復
 中央管理サイトを回復するための無人セットアップ用スクリプト ファイルを構成するには、次の情報を使用します。

 **Identification**

-   **キー名:** Action

    -   **必須:** はい
    -   **値:** RecoverCCAR
    -   **詳細:** 中央管理サイトを回復します


-   **キー名:** CDLatest

    -   **必須:** はい – CD.Latest フォルダーのメディアを使う場合のみ。
    -   **値:** 1。1 以外の値は CD.Latest を使わないものと見なされます。
    -   **詳細:** プライマリ サイトまたは中央管理サイトのインストールまたは回復を目的として、CD.Latest フォルダーのメディアからセットアップを実行するときは、スクリプトにこのキーと値が含まれる必要があります。 この値は、CD.Latest のメディアが使われていることを、セットアップに通知します。

**RecoveryOptions**   
-   **キー名:** ServerRecoveryOptions   

    -   **必須:** はい
    -   **値** : 1、2、または 4  
         1 = サイト サーバーと SQL Server を回復します。   
         2 = サイト サーバーだけを回復します。  
         4 = SQL Server だけを回復します。
    -   **詳細:** セットアップでサイト サーバーと SQL Server のどちらか、または両方を回復することを指定します。 ServerRecoveryOptions の設定値によって、関連するキーの設定が異なります。  
        -   **値 = 1** : **SiteServerBackupLocation** キーに値を指定して、サイトのバックアップを使ってサイトを回復することができます。 値を指定しなかった場合は、バックアップを使わずにサイトが再インストールされます。

             **DatabaseRecoveryOptions** キーを **10** に設定して、バックアップからサイト データベースが復元されるようにした場合は、 **BackupLocation** キーを指定する必要があります。

        -   **値 = 2** : **SiteServerBackupLocation** キーに値を指定して、サイトのバックアップを使ってサイトを回復することができます。 値を指定しなかった場合は、バックアップを使わずにサイトが再インストールされます。

        -   **値 = 4** インストールする **BackupLocation** キーを **10** に設定して、バックアップからサイト データベースが復元されるようにした場合は、 **BackupLocation** キーを指定する必要があります。

-   **キー名:** DatabaseRecoveryOptions

    -   **必須** : 状況によって異なる
    -   **値:**   
         - **10** = バックアップからサイト データベースを復元します。  
         - **20** = 別の方法を使って手動で回復されたサイト データベースを使用します。   
         - **40** = サイトの新しいデータベースを作成します。 サイト データベースのバックアップがない場合に、このオプションを使用してください。 グローバル データとサイト データは、別のサイトをレプリケートすることによって回復します。  
         - **80** = データベースの回復をスキップします。
    -   **詳細:** SQL Server のサイト データベースをセットアップでどのように回復するかを指定します。 このキーは、 **ServerRecoveryOptions** キーを **1** または **4**に設定したときに必要です。


-   **キー名:** ReferenceSite  

    -   **必須** : 状況によって異なる
    -   **値:** &lt;ReferenceSiteFQDN\>
    -   **詳細:** 基準プライマリ サイトを指定します。 データベースのバックアップが変更履歴のリテンション期間より前に作成されているか、バックアップなしでサイトを回復する場合、中央管理サイトでは基準サイトを使用してグローバル データを回復します。

         基準サイトを指定しておらず、バックアップが変更の追跡の保有期間より前に作成されている場合は、すべてのプライマリ サイトが、中央管理サイトから復元されたデータで再初期化されます。

         基準サイトを指定しておらず、バックアップが変更の追跡の保有期間内に作成されている場合は、バックアップ作成以降に加えられた変更だけが、プライマリ サイトからレプリケートされます。 プライマリ サイト同士の変更内容が競合している場合は、中央管理サイトで、最初に受け取った変更内容が採用されます。

         このキーは、 **DatabaseRecoveryOptions** キーを **40**に設定したときに必要です。

-   **キー名:** SiteServerBackupLocation

    -   **必須:** いいえ
    -   **値:** &lt;PathToSiteServerBackupSet\>
    -   **詳細:** サイト サーバーのバックアップ セットへのパスを指定します。 このキーは、 **ServerRecoveryOptions** キーを **1** か **2**に設定したときにオプションで指定するキーです。 サイトのバックアップを使ってサイトを回復したい場合に、 **SiteServerBackupLocation** キーでバックアップの場所を指定します。 値を指定しなかった場合は、バックアップを使わずにサイトが再インストールされます。


-   **キー名:** BackupLocation

    -   **必須** : 状況によって異なる
    -   **値:** &lt;PathToSiteDatabaseBackupSet\>
    -   **詳細:** サイト データベースのバックアップ セットへのパスを指定します。 **BackupLocation** キーは、 **ServerRecoveryOptions** キーを **1** か **4** に設定したときに必要です。このキーを指定したときは、 **DatabaseRecoveryOptions** キーを **10** に設定してください。


**Options**

-   **キー名:** ProductID
    -   **必須:** はい
    -   **値:**   
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - 評価版
    -   **詳細:** ダッシュを含む、インストールする Configuration Manager のプロダクト キー。 「**Eval**」と入力することで、Configuration Manager の評価版をインストールできます。  


-   **キー名:** SiteCode

    -   **必須:** はい
    -   **値:** &lt;サイト コード\>
    -   **詳細:** 階層内のサイトを一意に識別する英数字 3 文字。 障害が発生する前にサイトで使用されていたサイト コードを指定します。


-   **キー名:** SiteName

    -   **必須:** はい
    -   **値:** SiteName
    -   **詳細:** このサイトの説明。


-   **キー名:** SMSInstallDir

    -   **必須:** はい
    -   **値:** &lt;*ConfigMgrInstallationPath*>
    -   **詳細:** Configuration Manager のプログラム ファイルのインストール フォルダーを指定します。
        > [!NOTE]   
        >  Configuration Manager のインストールに使用する元のパスまたは新しいパスを指定できます。

-   **キー名:** SDKServer

    -   **必須:** はい
    -   **値:** &lt;*SMS プロバイダーの FQDN*>
    -   **詳細:** SMS プロバイダーをホストするサーバーの FQDN を指定します。 障害が発生する前に SMS プロバイダーをホストしていたサーバーを指定します。

         初期インストールが終わった後で、他の SMS プロバイダーを追加して構成することができます。

-   **キー名:** PrerequisiteComp

    -   **必須:** はい
    -   **値:** 0 または 1  
         0 = ダウンロードします。   
         1 = 既にダウンロードされています。
    -   **詳細:** セットアップの前提条件ファイルが既にダウンロード済みかどうかを指定します。 たとえば、0 の値を使用すると、セットアップ時にファイルがダウンロードされます。  


-   **キー名:** PrerequisitePath

    -   **必須:** はい
    -   **値:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **詳細:** セットアップの前提条件ファイルのパスを指定します。 このパスは、**PrerequisiteComp** キーに設定した値に応じて、ダウンロードしたファイルを保存するか、ダウンロード済みのファイルを見つけるために使われます。

-   **キー名:** AdminConsole

    -   **必須** : 状況によって異なる
    -   **値:** 0 または 1 0 = インストールしません。   
         1 = インストールします。
    -   **詳細:** Configuration Manager コンソールをインストールするかどうかを指定します。 このキーは、 **ServerRecoveryOptions** キーを **4**以外の値に設定した場合に必要です。


-   **キー名:** JoinCEIP   
    > [!Note]  
    > Configuration Manager バージョン 1802 以降では、CEIP 機能が製品から削除されます。

    -   **必須:** はい
    -   **値:** 0 または 1  
         0 = 参加しません。  
         1 = 参加します。
    -   **詳細:** カスタマー エクスペリエンス向上プログラムに参加するかどうかを指定します。

**SQLConfigOptions**

-   **キー名:** SQLServerName

    -   **必須:** はい
    -   **値:** *&lt;SQLServerName\>*
    -   **詳細:** サイト データベースをホストする SQL Server を実行しているサーバー、またはクラスター化されている場合はインスタンス名。 障害が発生する前にサイト データベースをホストしていたのと同じサーバーを指定します。


-   **キー名:** DatabaseName

    -   **必須:** はい
    -   **値:** *&lt;SiteDatabaseName\>* または *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*
    -   **詳細:** 中央管理サイト データベースをインストールするために作成または使用する SQL Server データベースの名前。 障害が発生する前に使用されていたデータベース名と同じ名前を指定します。

        > [!IMPORTANT]  
        >  既定のインスタンスを使用しない場合は、インスタンス名とサイト データベース名を指定する必要があります。

-   **キー名:** SQLSSBPort

    -   **必須:** いいえ
    -   **値:** &lt;*SSBPortNumber*>
    -   **詳細:** SQL Server で使用する SQL Server Service Broker (SSB) のポート番号を指定します。 通常、TCP ポート 4022 に構成しますが、別のポートもサポートされています。 障害が発生する前に使用されていたのと同じ SSB ポート番号を指定します。

## <a name="recover-a-primary-site-unattended"></a>プライマリ サイトの無人回復
 中央管理サイトを回復するための無人セットアップ用スクリプト ファイルを構成するには、次の情報を使用します。

 **Identification**

-   **キー名:** Action

    -   **必須:** はい
    -   **値:** RecoverPrimarySite
    -   **詳細:** プライマリ サイトを回復します


-   **キー名:** CDLatest

    -   **必須:** はい – CD.Latest フォルダーのメディアを使う場合のみ。
    -   **値:** 1。1 以外の値は CD.Latest を使わないものと見なされます。
    -   **詳細:** プライマリ サイトまたは中央管理サイトのインストールまたは回復を目的として、CD.Latest フォルダーのメディアからセットアップを実行するときは、スクリプトにこのキーと値が含まれる必要があります。 この値は、CD.Latest のメディアが使われていることを、セットアップに通知します。

**RecoveryOptions**

-   **キー名:** ServerRecoveryOptions

    -   **必須:** はい
    -   **値** : 1、2、または 4    
         1 = サイト サーバーと SQL Server を回復します。   
         2 = サイト サーバーだけを回復します。  
         4 = SQL Server だけを回復します。
    -   **詳細:** セットアップでサイト サーバーと SQL Server のどちらか、または両方を回復することを指定します。 ServerRecoveryOptions の設定値によって、関連するキーの設定が異なります。

        -   **値 = 1** : **SiteServerBackupLocation** キーに値を指定して、サイトのバックアップを使ってサイトを回復することができます。 値を指定しなかった場合は、バックアップを使わずにサイトが再インストールされます。

             **DatabaseRecoveryOptions** キーを **10** に設定して、バックアップからサイト データベースが復元されるようにした場合は、 **BackupLocation** キーを指定する必要があります。

        -   **値 = 2** : **SiteServerBackupLocation** キーに値を指定して、サイトのバックアップを使ってサイトを回復することができます。 値を指定しなかった場合は、バックアップを使わずにサイトが再インストールされます。

        -   **値 = 4** インストールする **BackupLocation** キーを **10** に設定して、バックアップからサイト データベースが復元されるようにした場合は、 **BackupLocation** キーを指定する必要があります。

-   **キー名:** DatabaseRecoveryOptions

    -   **必須** : 状況によって異なる
    -   **値:**   
         - **10** = バックアップからサイト データベースを復元します。  
         - **20** = 別の方法を使って手動で回復されたサイト データベースを使用します。     
         - **40** = サイトの新しいデータベースを作成します。 サイト データベースのバックアップがない場合に、このオプションを使用してください。 グローバル データとサイト データは、別のサイトをレプリケートすることによって回復します。  
         - **80** = データベースの回復をスキップします。
    -   **詳細:** SQL Server のサイト データベースをセットアップでどのように回復するかを指定します。 このキーは、 **ServerRecoveryOptions** キーを **1** または **4**に設定したときに必要です。


-   **キー名:** SiteServerBackupLocation

    -   **必須:** いいえ
    -   **値:** &lt;PathToSiteServerBackupSet\>
    -   **詳細:** サイト サーバーのバックアップ セットへのパスを指定します。 このキーは、 **ServerRecoveryOptions** キーを **1** か **2**に設定したときにオプションで指定するキーです。 サイトのバックアップを使ってサイトを回復したい場合に、 **SiteServerBackupLocation** キーでバックアップの場所を指定します。 値を指定しなかった場合は、バックアップを使わずにサイトが再インストールされます。     


-   **キー名:** BackupLocation

    -   **必須** : 状況によって異なる
    -   **値:** &lt;PathToSiteDatabaseBackupSet\>
    -   **詳細:** サイト データベースのバックアップ セットへのパスを指定します。 **BackupLocation** キーは、 **ServerRecoveryOptions** キーを **1** か **4** に設定したときに必要です。このキーを指定したときは、 **DatabaseRecoveryOptions** キーを **10** に設定してください。

**Options**

-   **キー名:** ProductID

    -   **必須:** はい
    -   **値:**     
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - 評価版     
    -   **詳細:** ダッシュを含む、インストールする Configuration Manager のプロダクト キー。 「**Eval**」と入力することで、Configuration Manager の評価版をインストールできます。  


-   **キー名:** SiteCode

    -   **必須:** はい
    -   **値:** &lt;サイト コード\>
    -   **詳細:** 階層内のサイトを一意に識別する英数字 3 文字。 障害が発生する前にサイトで使用されていたサイト コードを指定します。


-   **キー名:** SiteName

    -   **必須:** はい
    -   **値:** SiteName
    -   **詳細:** このサイトの説明。


-   **キー名:** SMSInstallDir

    -   **必須:** はい
    -   **値:** &lt;*ConfigMgrInstallationPath*>
    -   **詳細:** Configuration Manager のプログラム ファイルのインストール フォルダーを指定します。

        > [!NOTE]   
        >  Configuration Manager のインストールに使用する元のパスまたは新しいパスを指定できます。

-   **キー名:** SDKServer

    -   **必須:** はい
    -   **値:** &lt;*SMS プロバイダーの FQDN*>
    -   **詳細:** SMS プロバイダーをホストするサーバーの FQDN を指定します。 障害が発生する前に SMS プロバイダーをホストしていたサーバーを指定します。

         初期インストールが終わった後で、他の SMS プロバイダーを追加して構成することができます。

-   **キー名:** PrerequisiteComp

    -   **必須:** はい
    -   **値:** 0 または 1    
         0 = ダウンロードします。   
         1 = 既にダウンロードされています。   
    -   **詳細:** セットアップの前提条件ファイルが既にダウンロード済みかどうかを指定します。 たとえば、0 の値を使用すると、セットアップ時にファイルがダウンロードされます。


-   **キー名:** PrerequisitePath

    -   **必須:** はい
    -   **値:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **詳細:** セットアップの前提条件ファイルのパスを指定します。 このパスは、**PrerequisiteComp** キーに設定した値に応じて、ダウンロードしたファイルを保存するか、ダウンロード済みのファイルを見つけるために使われます。


-   **キー名:** AdminConsole

    -   **必須** : 状況によって異なる
    -   **値:** 0 または 1  
         0 = インストールしません。   
         1 = インストールします。  
    -   **詳細:** Configuration Manager コンソールをインストールするかどうかを指定します。 このキーは、 **ServerRecoveryOptions** キーを **4**以外の値に設定した場合に必要です。

-   **キー名:** JoinCEIP  
    > [!Note]  
    > Configuration Manager バージョン 1802 以降では、CEIP 機能が製品から削除されます。

    -   **必須:** はい
    -   **値:** 0 または 1    
         0 = 参加しません。  
         1 = 参加します。
    -   **詳細:** カスタマー エクスペリエンス向上プログラムに参加するかどうかを指定します。


**SQLConfigOptions**

-   **キー名:** SQLServerName

    -   **必須:** はい
    -   **値:** *&lt;SQLServerName\>*
    -   **詳細:** サイト データベースをホストする SQL Server を実行しているサーバー、またはクラスター化されている場合はインスタンス名。 障害が発生する前にサイト データベースをホストしていたのと同じサーバーを指定します。


-   **キー名:** DatabaseName

    -   **必須:** はい
    -   **値:** *&lt;SiteDatabaseName\>* または *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*
    -   **詳細:** 中央管理サイト データベースをインストールするために作成または使用する SQL Server データベースの名前。 障害が発生する前に使用されていたデータベース名と同じ名前を指定します。

        > [!IMPORTANT]    
        >  既定のインスタンスを使用しない場合は、インスタンス名とサイト データベース名を指定する必要があります。

-   **キー名:** SQLSSBPort

    -   **必須:** いいえ
    -   **値:** &lt;*SSBPortNumber*>
    -   **詳細:** SQL Server で使用する SQL Server Service Broker (SSB) のポート番号を指定します。 通常、TCP ポート 4022 に構成しますが、別のポートもサポートされています。 障害が発生する前に使用されていたのと同じ SSB ポート番号を指定します。

**Hierarchy ExpansionOption**

-   **キー名:** CCARSiteServer

    -   **必須** : 状況によって異なる
    -   **値:** &lt;*SiteCodeForCentralAdministrationSite*>
    -   **詳細:** プライマリ サイトを Configuration Manager 階層に含めるときに、アタッチする中央管理サイトを指定します。 障害が発生する前にプライマリ サイトが中央管理サイトにアタッチされていた場合は、この設定が必要です。 障害が発生する前に中央管理サイトで使用されていたサイト コードを指定します。

-   **キー名:** CASRetryInterval

    -   **必須:** いいえ
    -   **値:** &lt;*間隔*>
    -   **詳細:** 中央管理サイトとの接続が切断されたときに、接続を再試行する間隔 (分) を指定します。 たとえば、中央管理サイトへの接続が失敗すると、プライマリ サイトでは、CASRetryInterval で指定された時間 (分) だけ待機してから接続が再試行されます。


-   **キー名:** WaitForCASTimeout

    -   **必須:** いいえ
    -   **値:** &lt;*タイムアウト*>
    -   **詳細:** プライマリ サイトから中央管理サイトに接続するときのタイムアウトの最大値 (分) を指定します。 たとえば、プライマリ サイトから中央管理サイトに接続できなかった場合は、プライマリ サイトは、WaitForCASTimeout キーで指定された時間が経過するまで、CASRetryInterval キーの値に従って、中央管理サイトとの接続を再試行します。 0 ～ 100 に指定できます。