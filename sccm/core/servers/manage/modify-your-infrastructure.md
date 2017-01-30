---
title: "インフラストラクチャの変更 | Microsoft Docs"
description: "展開した Configuration Manager のインフラストラクチャに影響する変更を加えたりアクションを実行したりする方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
caps.latest.revision: 19
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 52d2e088b8db3c2e9a0af640ca3db72b9fd7af60
ms.openlocfilehash: a5228c4984347be4b115bfa5563791fa2fb7319c


---
# <a name="modify-your-system-center-configuration-manager-infrastructure"></a>System Center Configuration Manager インフラストラクチャの変更

*適用対象: System Center Configuration Manager (Current Branch)*

1 つ以上のサイトをインストールした後、構成を変更するか、展開したインフラストラクチャに影響を与えるアクションを取る必要があります。  


##  <a name="a-namebkmkmanagesmsprovidera-manage-the-sms-provider"></a><a name="BKMK_ManageSMSprovider"></a> SMS プロバイダーを管理する  
 SMS プロバイダー (ダイナミック リンク ライブラリ ファイル: smsprov.dll) は、1 つ以上の Configuration Manager コンソールの管理のための接続ポイントとなります。 複数の SMS プロバイダーをインストールすると、サイトおよび階層を管理するための冗長な接続ポイントを提供できます。  

 各 Configuration Manager サイトで、セットアップを再実行できます。  

-   SMS プロバイダーの追加インスタンスを追加します (SMS プロバイダーの各追加インスタンスは別々のコンピューターに配置する必要があります)  

-   SMS プロバイダーのインスタンスを削除します (サイトの最新の SMS プロバイダーを削除するには、サイトをアンインストールする必要があります)  

 SMS プロバイダーのインストールまたは削除を監視するには、セットアップを実行したサイト サーバーのルート フォルダーにある ConfigMgrSetup.log を表示します。 ****  

 サイトの SMS プロバイダーを変更する前に、「[System Center Configuration Manager の SMS プロバイダーの計画](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)」にある情報をよく理解しておいてください。  

#### <a name="to-manage-the-sms-provider-configuration-for-a-site"></a>サイトの SMS プロバイダーの構成を管理するには  

1.  **&lt;Configuration Manager サイトのインストール フォルダー\>\BIN\X64\setup.exe** から **Configuration Manager のセットアップ**を実行します。  

2.  **[作業の開始]** ページで、 **[サイトのメンテナンスを実施するか、このサイトをリセットする]**を選択し、 **[次へ]**をクリックします。  

3.  **[サイトのメンテナンス]** ページで、 **[SMS プロバイダーの構成を変更する]**を選択し、 **[次へ]**をクリックします。  

4.  [SMS プロバイダーの管理] ページで、次のいずれかのオプションを選択して、ウィザードを完了します。 ****  

    -   このサイトに SMS プロバイダーを追加するには  

         **[新しい SMS プロバイダーを追加する]**を選択し、SMS プロバイダーをホストする予定の (現在 SMS プロバイダーをホストしていない) コンピューターの FQDN を指定して、 **[次へ]**をクリックします。  

    -   サーバーから SMS プロバイダーを削除するには  

         **[指定した SMS プロバイダーをアンインストールする]**を選択し、SMS プロバイダーを削除するコンピューターの名前を選択して **[次へ]**をクリックし、操作を確定します。  

        > [!TIP]  
        >  2 つのコンピューター間で SMS プロバイダーを移動するには、新しいコンピューターに SMS プロバイダーをインストールして、元の場所から SMS プロバイダーを削除する必要があります。 一度の処理で SMS プロバイダーをコンピューター間で移動する専用のオプションはありません。  

 セットアップ ウィザードを終了すると、SMS プロバイダーの構成が完了します。 **[全般]** タブのサイトの **[プロパティ]** ダイアログ ボックスで、サイトの SMS プロバイダーがインストールされているコンピューターを確認できます。  

##  <a name="a-namebkmkconsolea-manage-the-configuration-manager-console"></a><a name="bkmk_Console"></a> Configuration Manager コンソールを管理する  
 Configuration Manager コンソールの管理で行えるタスクは、次のとおりです。  

-   **Configuration Manager コンソールに表示される言語を変更する**: インストールされている言語を変更するには、このトピックの「[Configuration Manager コンソールの言語の管理](#BKMK_ManageConsoleLanguages)」を参照してください。  

-   **追加コンソールをインストールする**: 追加コンソールをインストールするには、「[System Center Configuration Manager コンソールのインストール](/sccm/core/servers/deploy/install/install-consoles)」を参照してください。  

-   **DCOM を構成する**: サイト サーバーからリモートにあるコンソールが接続できるよう DCOM アクセス許可を構成するには、このトピックの「[リモートからの Configuration Manager コンソールに対する DCOM アクセス許可の構成](#BKMK_ConfigDCOMforRemoteConsole)」を参照してください。  

-   [**コンソールで管理ユーザーに表示される内容を制限するようアクセス許可を変更する**] 管理アクセス許可を変更するには (これによって、コンソールに表示される内容とコンソールで行える操作が制限される)、「[管理ユーザーの管理スコープの変更](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_ModAdminUser)」を参照してください。     

###  <a name="a-namebkmkmanageconsolelanguagesa-manage-configuration-manager-console-language"></a><a name="BKMK_ManageConsoleLanguages"></a> Configuration Manager コンソールの言語を管理する  
 サイト サーバーのインストール中に、Configuration Manager コンソールのインストール ファイルおよびサイトでサポートされる言語パックが、サイト サーバーの **&lt;Configuration Manager のインストール パス\>\Tools\ConsoleSetup** サブフォルダーにコピーされます。  

-   サイト サーバーのこのフォルダーから Configuration Manager コンソールのインストールを開始すると、Configuration Manager コンソールとサポートされる言語パック ファイルがコンピューターにコピーされます。  

-   コンピューターの現在の言語設定と同じ言語パックがある場合は、Configuration Manager コンソールがその言語で開きます。  

-   関連付けられている言語パックがない場合は、Configuration Manager コンソールが英語で開きます。  

たとえば、英語、ドイツ語、およびフランス語をサポートするサイト サーバーから Configuration Manager コンソールをインストールした場合を考えます。 フランス語の言語設定のコンピューターでは、Configuration Manager コンソールもフランス語で開きます。 一方、日本語の言語設定のコンピューターで Configuration Manager コンソールを開いた場合は、日本語の言語パックがないので、英語で表示されます。  

 Configuration Manager コンソールを開くたびに、コンピューターの言語設定と、該当する言語パックが Configuration Manager コンソールで使用できるかどうかが確認されて、適切な言語パックを使ってコンソールが表示されます。 コンピューターの言語設定に関係なく、Configuration Manager コンソールを英語で開きたい場合は、コンピューターの言語パック ファイルを手動で削除するか、名前を変更する必要があります。  

 コンピューターのロケール設定に関係なく Configuration Manager コンソールが常に英語で開くようにするには、次の手順に従います。  

##### <a name="to-install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>Configuration Manager コンソールの英語専用バージョンをコンピューターにインストールするには  

1.  エクスプローラーで **&lt;Configuration Manager のインストール パス\>\Tools\ConsoleSetup\LanguagePack** に移動します。  

2.  **.msp** ファイルと **.mst** ファイルの名前を変更します。 たとえば、**&lt;ファイル名\>.MSP** を**&lt; ファイル名\>.MSP.disabled** に変更します。  

3.  Configuration Manager コンソールをコンピューターにインストールします。  

    > [!IMPORTANT]  
    >  サイト サーバーで新しいサーバー言語が構成された場合は、.msp ファイルと .mst ファイルが **LanguagePack** フォルダーに再びコピーされるため、上記の手順を繰り返して、英語専用の新しい Configuration Manager コンソールをインストールする必要があります。  

##### <a name="to-temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>既存の Configuration Manager コンソールで言語を一時的に無効にするには  

1.  Configuration Manager コンソールを実行しているコンピューターで、Configuration Manager コンソールを閉じます。  

2.  エクスプローラーで、Configuration Manager コンソール コンピューターの &lt;*コンソールのインストール パス*>\Bin\ に移動します。  

3.  コンピューターで設定されている言語のフォルダーの名前を変更します。 たとえば、コンピューターでドイツ語が設定されている場合は、[ **de** ] フォルダーの名前を「 **de.disabled**」に変更します。  

4.  コンピューターで設定されている言語で Configuration Manager コンソールを開くには、フォルダーを元の名前に戻します。 たとえば、「 **de.disabled** 」を「 **de**」に変更します。  

##  <a name="a-namebkmkconfigdcomforremoteconsolea-configure-dcom-permissions-for-remote-configuration-manager-consoles"></a><a name="BKMK_ConfigDCOMforRemoteConsole"></a> リモート Configuration Manager コンソールに対する DCOM アクセス許可を構成する  
 Configuration Manager コンソールを実行するユーザー アカウントには、SMS プロバイダーを使用してサイト データベースにアクセスするためのアクセス許可が必要となります。 ただし、リモート Configuration Manager コンソールを使用する管理ユーザーには、次の場所での **リモート アクティブ化** DCOM アクセス許可も必要となります。  

-   サイト サーバー コンピューター  

-   SMS プロバイダーのインスタンスをホストする各コンピューター  

 **SMS 管理者** という名前のセキュリティ グループは、コンピューター上の SMS プロバイダーへのアクセス許可を付与します。また、必要な DCOM アクセス許可を付与するために使用できます。 このグループは、SMS プロバイダーがメンバー サーバーで実行されている場合は、そのコンピューターのローカルとなり、SMS プロバイダーがドメイン コントローラーで実行されている場合は、ドメインのローカル グループとなります。  

> [!IMPORTANT]  
>  Configuration Manager コンソールは Windows Management Instrumentation (WMI) を使用して SMS プロバイダーに接続し、WMI は内部的に DCOM を使用します。 このため、Configuration Manager では、Configuration Manager コンソールが SMS プロバイダー以外のコンピューターで実行されている場合、SMS プロバイダー コンピューターで DCOM サーバーをアクティブにするためのアクセス許可が必要です。 既定では、リモートでアクティブにするためのアクセス許可は、組み込みの管理者グループのメンバーにのみ付与されます。 SMS 管理者グループにリモートでアクティブにするためのアクセス許可を付与すると、このグループのメンバーは SMS プロバイダーのコンピューターに対して DCOM 攻撃を試みることができるようになります。 また、この構成ではコンピューターの脆弱性が増します。 この脅威を軽減するには、SMS 管理者グループのメンバーシップを慎重に監視します。  

 各中央管理サイト、プライマリ サイト サーバー、および SMS プロバイダーがインストールされている各コンピューターを構成し、リモートの Configuration Manager コンソールからのアクセス権を管理ユーザーに付与するには、次の手順に従います。  

#### <a name="to-configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>リモートからの Configuration Manager コンソール接続に対する DCOM アクセス許可を構成するには  

1.  **Dcomcnfg.exe** を実行して **コンポーネント サービス**を開きます。  

2.  **[コンポーネント サービス]** で **[コンソールのルート]** >  **[コンポーネント サービス]** > **[コンピューター]** の順にクリックし、**[マイ コンピューター]** をクリックします。 **[操作]** メニューの **[プロパティ]**をクリックします。  

3.  **[マイ コンピューターのプロパティ]** ダイアログ ボックスの **[COM セキュリティ]** タブで、 **[起動とアクティブ化のアクセス許可]** セクションにある **[制限の編集]**をクリックします。  

4.  **[起動とアクティブ化のアクセス許可]** ダイアログ ボックスで、 **[追加]**をクリックします。  

5.  **[ユーザー、コンピューター、サービス アカウントまたはグループの選択]** ダイアログ ボックスの **[選択するオブジェクト名を入力してください (例)]** ボックスに、「 **SMS Admins**」と入力し、 **[OK]**をクリックします。  

    > [!NOTE]  
    >  SMS 管理者グループを見つけるには、[検索場所] の設定を変更する必要がある場合があります。 **** このグループは、SMS プロバイダーがメンバー サーバーで実行されている場合は、そのコンピューターのローカルとなり、SMS プロバイダーがドメイン コントローラーで実行されている場合は、ドメインのローカル グループとなります。  

6.  **[SMS 管理者のアクセス許可]** セクションで、リモート アクティブ化を許可するために、 **[リモートからのアクティブ化]** チェック ボックスをオンにします。  

7.  **[OK]** をクリックし、もう一度 **[OK]** をクリックしてから、 **[コンピューターの管理]**を閉じます。 SMS 管理者グループのメンバーに対して、リモートの Configuration Manager コンソールからのアクセスを許可するようにコンピューターが構成されました。  

 リモートの Configuration Manager コンソールをサポートする各 SMS プロバイダーのコンピューターで、この手順を繰り返します。  

##  <a name="a-namebkmkdbconfiga-modify-the-site-database-configuration"></a><a name="bkmk_dbconfig"></a> サイト データベースの構成を変更する  
 サイトをインストールした後に、サイト データベースおよびサイト データベース サーバーの構成を変更するには、中央管理サイト サーバーまたはプライマリ サイト サーバーでセットアップを実行します。 サイト データベースは、同じコンピューター上の SQL Server の新しいインスタンス、またはサポートされているバージョンの SQL Server を実行する別のコンピューターに移動できます。 これらの変更および関連する変更は、セカンダリ サイトのデータベースの構成ではサポートされません。  

 サポートの制限について詳しくは、「 [Configuration Manager 環境での手動によるデータベース変更のサポート ポリシー](https://support.microsoft.com/kb/3106512)」をご覧ください。  

> [!NOTE]  
>  サイトのデータベース構成を変更すると、Configuration Manager はサイト サーバー、およびそのデータベースと通信するリモート サイト システム サーバー上の Configuration Manager サービスを再起動または再インストールします。  

**データベース構成を変更するには**、サイト サーバーでセットアップを実行し、 **[サイトのメンテナンスを実施するか、このサイトをリセットする]**オプションを選択します。 次に、[SQL Server の構成を変更する] オプションを選択します。 **** 次のサイト データベースの構成を変更することができます。  

-   データベースをホストする Windows ベースのサーバー。  

-   SQL Server データベースをホストするサーバーで使用されている SQL Server のインスタンス。  

-   データベース名。  

-   Configuration Manager によって使用中の SQL Server のポート  

-   Configuration Manager によって使用中の SQL Server サービス ブローカーのポート  

**サイト データベースを移動するには、次の項目を構成する必要があります。**  

-   **[アクセスの構成]** : サイト データベースを新しいコンピューターに移動する場合は、SQL Server を実行するコンピューターの **ローカルの [Administrators]** グループにサイト サーバーのコンピューター アカウントを追加します。 サイト データベースに SQL Server クラスターを使用する場合は、各 Windows Server クラスター ノード コンピューターのローカルの [Administrators] グループにコンピューター アカウントを追加する必要があります。 ****  

-   **共通言語ランタイム (CLR) 統合:**  データベースを SQL Server 上の新しいインスタンス、または新しい SQL Server コンピューターに移動する場合は、共通言語ランタイム (CLR) 統合を有効にする必要があります。 CLR を有効にするには、**SQL Server Management Studio** を使用して、サイト データベースをホストする SQL Server のインスタンスに接続し、ストアド プロシージャ **sp_configure 'clr enabled',1; reconfigure** をクエリとして実行します。  
-  **新しい SQL Server がバックアップの場所にアクセスできることを確認する:** サイト データベースのバックアップを格納するために UNC を使っている場合は、データベースを新しいサーバーに移動した後で (SQL Server AlwaysOn 可用性グループまたは SQL Server クラスターの移動を含みます)、新しい SQL Server のコンピューター アカウントに UNC の場所への**書き込み**アクセス許可があることを確認します。  


> [!IMPORTANT]  
>  管理ポイントの&1; つまたは複数のデータベースのレプリカを持つデータベースを移動する場合は、最初にデータベースのレプリカを削除する必要があります。 データベースの移動が完了したら、データベースのレプリカを再構成できます。 詳細については、「 [Database replicas for management points for System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)」をご覧ください。  

##  <a name="a-namebkmkspna-manage-the-spn-for-the-site-database-server"></a><a name="bkmk_SPN"></a> サイト データベース サーバーの SPN を管理する  
サイト データベースの SQL サービスを実行するアカウントを選択することができます。  

-   コンピューターのシステム アカウントでサービスが実行されると、SPN は自動的に登録されます。  

-   ドメイン ローカル ユーザー アカウントでサービスが実行される場合、SQL クライアントおよびその他のサイト システムが Kerberos 認証を確実に実行できるよう SPN を手動で登録する必要があります。 Kerberos 認証を使用しない場合、データベースへの通信は失敗する可能性があります。  

SQL Server ドキュメントは [SPN を手動で登録する](https://technet.microsoft.com/library/ms191153\(v=sql.120\).aspx)うえで役立ち、SPN および Kerberos 接続に関する追加の背景情報を提供します。  

> [!IMPORTANT]  
>  -   クラスター化された SQL Server の SPN を作成する場合は、SQL Server クラスターの仮想名を SQL Server のコンピューター名として指定する必要があります。  
> -   SQL Server の名前付きインスタンスの SPN を登録するコマンドは、既定のインスタンスの SPN を登録するときに使用するコマンドと同じですが、ポート番号が名前付きインスタンスで使用するポートと一致している必要があります。  

サイト データベース サーバーの SQL Server サービス アカウントの SPN を登録するには、 **Setspn** ツールを使用します。 Setspn ツールは、SQL Server のドメインに存在するコンピューターで、ドメイン管理者の資格情報を使用して実行する必要があります。  

 Windows Server 2008 R2 で Setspn ツールを使用する SQL Server サービス アカウントの SPN を管理するには、次の手順に従います。 Setspn の詳細については、「 [Setspn Overview (Setspn の概要)](http://go.microsoft.com/fwlink/p/?LinkId=226343)」または使用しているオペレーティング システムの同様のドキュメントを参照してください。  

> [!NOTE]  
>  次の手順では Setspn コマンドライン ツールを使用しています。 Setspn コマンドライン ツールは、Windows Server 2003 Support Tools を製品 CD または [Microsoft ダウンロード センター](http://go.microsoft.com/fwlink/p/?LinkId=100114)からインストールするときに含められます。 Windows Support Tools を製品 CD からインストールする方法の詳細については、「 [Windows サポート ツールをインストールする](http://go.microsoft.com/fwlink/p/?LinkId=62270)」を参照してください。  

#### <a name="to-manually-create-a-domain-user-service-principal-name-spn-for-the-sql-server-service-account"></a>SQL Server サービス アカウントのドメイン ユーザー サービス プリンシパル名 (SPN) を手動で作成するには  

1.  **[スタート]** メニューの **[ファイル名を指定して実行]**をクリックし、[ファイル名を指定して実行] ダイアログ ボックスに「 **cmd** 」と入力します。  

2.  コマンド ラインで、Windows Server サポート ツールのインストール ディレクトリに移動します。 既定では、これらのツールは **C:\Program Files\Support Tools** ディレクトリにあります。  

3.  有効なコマンドを入力して SPN を作成します。 SPN を作成するには、NetBIOS 名、または SQL Server を実行するコンピューターの完全修飾ドメイン名 (FQDN) を使用できます。 ただし、NetBIOS 名と FQDN の両方の SPN を作成する必要があります。  

    > [!IMPORTANT]  
    >  クラスター化された SQL Server の SPN を作成する場合は、SQL Server クラスターの仮想名を SQL Server のコンピューター名として指定する必要があります。  

    -   SQL Server コンピューターの NetBIOS 名の SPN を作成するには、コマンド **setspn -A MSSQLSvc/&lt;SQL Server コンピューター名\>:1433 &lt;ドメイン\アカウント** を入力します。  

    -   SQL Server コンピューターの FQDN の SPN を作成するには、コマンド **setspn -A MSSQLSvc/&lt;SQL Server FQDN\>:1433 &lt;ドメイン\アカウント** を入力します。  

    > [!NOTE]  
    >  SQL Server の名前付きインスタンスの SPN を登録するコマンドは、既定のインスタンスの SPN を登録するときに使用するコマンドと同じですが、ポート番号が名前付きインスタンスで使用するポートと一致している必要があります。  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-by-using-the-setspn-command"></a>Setspn コマンドを使用してドメイン ユーザーの SPN が正しく登録されていることを確認するには  

1.  **[スタート]** メニューの **[ファイル名を指定して実行]**をクリックし、 **[ファイル名を指定して実行]** ダイアログ ボックスに「 **cmd** 」と入力します。  

2.  コマンド プロンプトで、コマンド **setspn -L &lt;ドメインn\SQL サービス アカウント** を入力します。  

3.  登録された [ServicePrincipalName] を確認して、SQL Server に有効な SPN が作成されたことを確認します。 ****  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-when-using-the-adsiedit-mmc-console"></a>ADSIEdit MMC コンソールを使用している場合に、ドメイン ユーザーの SPN が正しく登録されていることを確認するには  

1.  **[スタート]** メニューの **[ファイル名を指定して実行]**をクリックし、「 **adsiedit.msc** 」と入力して ADSIEdit MMC コンソールを起動します。  

2.  必要に応じて、サイト サーバーのドメインに接続します。  

3.  コンソール ウィンドウで、サイト サーバーのドメイン、**DC=&lt;サーバー識別名\>**、**CN=Users** の順に展開し、**CN=&lt;サービス アカウント ユーザー\>** を右クリックして、**[プロパティ]** をクリックします。  

4.  **[CN=&lt;サービス アカウント ユーザー\> のプロパティ]** ダイアログ ボックスで、**servicePrincipalName** の値を検討し、有効な SPN が作成されて適切な SQL Server コンピューターに関連付けられていることを確認します。  

#### <a name="to-change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>SQL Server のサービス アカウントをローカル システムからドメイン ユーザー アカウントに変更するには  

1.  SQL Server サービス アカウントとして使用するドメインまたはローカルのシステム ユーザー アカウントを作成または選択します。  

2.  **[SQL Server 構成マネージャー]**を開きます。  

3.  **[SQL Server のサービス]** をクリックし、**[SQL Server&lt;インスタンス名\>]** をダブルクリックします。  

4.  **[ログオン]** タブで、 **[このアカウント]**を選択してから、手順 1 で作成したドメイン ユーザー アカウントのユーザー名とパスワードを入力するか、 **[参照]** をクリックして Active Directory ドメイン サービスのユーザー アカウントを見つけて、最後に **[適用]**をクリックします。  

5.  **[アカウントの変更の確認]** ダイアログ ボックスで **[はい]** をクリックして、サービス アカウントの変更を確認し SQL Server サービスを再起動します。  

6.  サービス アカウントの変更が完了したら、 **[OK]** をクリックします。  

##  <a name="a-namebkmkreseta-run-a-site-reset"></a><a name="bkmk_reset"></a> サイト リセットを実行する  
 中央管理サイトまたはプライマリ サイトでサイト リセットを実行すると、サイトで次の操作が行われます。  

-   既定の Configuration Manager ファイルおよびレジストリ アクセス許可を再適用する  

-   サイトにすべてのサイト コンポーネントおよびすべてのサイト システムの役割を再インストールする  

セカンダリ サイトでは、サイトのリセットはサポートされません。  

選択する場合にはサイト リセットを手動で実行することができますが、サイト構成を変更した後で自動的に実行することもできます。  

たとえば、Configuration Manager コンポーネントによって使用されるアカウントに対して変更が加えられた場合、サイト コンポーネントの更新が確実に行われて新しいアカウントの詳細が使用されるよう手動サイト リセットを検討する必要があります。 ただし、サイトのクライアントまたはサーバーの言語を変更した場合、サイトでこの変更を使用できるようにするにはリセットを行う必要があるため、Configuration Manager は自動的にサイトのリセットを実行します。  

> [!NOTE]  
>  サイトのリセットでは、Configuration Manager 以外のオブジェクトに対するアクセス許可はリセットされません。  

サイト リセットの実行時には、以下が行われます。  

1.  セットアップでは、 **SMS_SITE_COMPONENT_MANAGER** サービスと、 **SMS_EXECUTIVE** サービスのスレッド コンポーネントを停止してから再起動します。  

2.  セットアップは、ローカル コンピューターおよびリモート サイト システム コンピューター上にある、サイト システムの共有フォルダーと **[SMS Executive]** コンポーネントを削除してから再作成します。  

3.  セットアップにより **SMS_SITE_COMPONENT_MANAGER** サービスが再インストールされ、このサービスによって **SMS_EXECUTIVE** サービスと **SMS_SQL_MONITOR** サービスがインストールされます。  

また、サイトのリセットでは、次のオブジェクトが復元されます。  

-   **SMS** または **NAL** のレジストリ キー、またはこれらのキーの既定のサブキー。  

-   Configuration Manager ファイル ディレクトリ ツリー、およびこのファイル ディレクトリ ツリー内の既定のファイルまたはサブディレクトリ。  

**サイトのリセットを実行するための必要条件**  

サイトのリセットの実行に使用するアカウントには、次のアクセス許可がある必要があります。  

-   サイトのリセットの実行に使用するアカウントには、次のアクセス許可がある必要があります。  

    -   **中央管理サイト**: このサイトでサイトのリセットの実行に使用するアカウントは、中央管理サイト サーバーのローカル管理者であり、 **[完全な権限を持つ管理者]** の役割に基づいた管理セキュリティ ロールと同等の権限を持っている必要があります。  

    -   **プライマリ サイト**: このサイトでサイトのリセットの実行に使用するアカウントは、プライマリ サイト サーバーのローカル管理者であり、 **[完全な権限を持つ管理者]** の役割に基づいた管理セキュリティ ロールと同等の権限を持っている必要があります。 プライマリ サイトが中央管理サイトの階層内にある場合、このアカウントは中央管理サイト サーバーのローカル管理者でもある必要があります。  

**サイトのリセットに関する制限事項**
  - バージョン 1602 以降、[実稼働前コレクションでのクライアント アップグレードのテスト](/sccm/core/clients/manage/upgrade/test-client-upgrades)をサポートするように階層が構成されている場合、サイトにインストールされているサーバーまたはクライアント言語パックをサイトのリセットによって変更することはできません。

#### <a name="to-perform-a-site-reset"></a>サイトのリセットを実行するには  

1.  **&lt;Configuration Manager サイトのインストール フォルダー\>\BIN\X64\setup.exe** から **Configuration Manager のセットアップ**を実行します。  

    > [!TIP]  
    >  サイト サーバー コンピューターの **[スタート]** メニューまたは Configuration Manager のソース メディアから Configuration Manager のセットアップを開始することによって、サイトのリセットを実行することもできます。  

2.  **[作業の開始]** ページで、 **[サイトのメンテナンスを実施するか、このサイトをリセットする]**を選択し、 **[次へ]**をクリックします。  

3.  **[サイトのメンテナンス]** ページで、 **[構成を変更せずにサイトをリセットする]**を選択してから、 **[次へ]**をクリックします。  

4.  [はい] をクリックして、サイトのリセットを開始します。 ****  

サイトのリセットが完了したら、[閉じる] をクリックしてこの手順を完了します。 ****  

##  <a name="a-namebkmksitelanga-manage-language-packs-at-a-site"></a><a name="bkmk_sitelang"></a> サイトの言語パックを管理する  
サイトをインストールした後、使用中のサーバーおよびクライアントの言語パックを変更することができます。  

**サーバー言語パック:**  

-   **適用対象:**  

     Configuration Manager コンソールのインストール  

     適用可能なサイト システムの役割の新規インストール  

-   **詳細:**  

     サイトのサーバー言語パックを更新した後は、言語パックのサポートを Configuration Manager コンソールに追加できます。  

     サーバー言語パックのサポートを Configuration Manager コンソールに追加するには、サイト サーバー上にある、使用する言語パックが格納されている **ConsoleSetup** フォルダーから Configuration Manager コンソールをインストールする必要があります。 Configuration Manager コンソールが既にインストールされている場合、新しいインストールを有効にしてサポートされる言語パックの最新の一覧を特定するには、まず既存のコンソールをアンインストールする必要があります。  

**クライアント言語パック:**  

-   **適用対象:**  

     クライアント言語パックに変更が生じると、新しいクライアントのインストールとアップグレードによってクライアント言語の更新されたリストのサポートが追加されるよう、クライアント インストール ソース ファイルが更新されます。  

-   **詳細:**  

     サイトのクライアント言語パックを更新したら、クライアント言語パックを含むソース ファイルを使用して、言語パックを使用する各クライアントをインストールする必要があります。  

Configuration Manager によってサポートされているクライアントとサーバーの言語については、「[System Center Configuration Manager の言語パック](../../../core/servers/deploy/install/language-packs.md)」を参照してください。  

#### <a name="to-modify-the-language-packs-that-are-supported-at-a-site"></a>サイトでサポートされる言語パックを変更するには  

1.  サイト サーバーで、**&lt;Configuration Manager のサイトのインストール フォルダー\>\BIN\X64\setup.exe** から Configuration Manager のセットアップを実行します。  

2.  [作業の開始 **** ] ページで、[サイトのメンテナンスを実施するか、このサイトをリセットする ****] を選択し、[次へ ****] をクリックします。  

3.  [サイトのメンテナンス **** ] ページで、[言語構成を変更する ****] を選択し、[次へ ****] をクリックします。  

4.  [必須ファイルのダウンロード **** ] ページで [必須ファイルをダウンロードする **** ] を選択して言語パックの更新プログラムを取得するか、[ダウンロード済みのファイルを使用する **** ] を選択して、サイトに使用する言語パックを含むダウンロード済みのファイルを使用します。 [次へ **** ] をクリックしてファイルを確認して続行します。  

5.  [サーバーの言語の選択 **** ] ページで、そのサイトがサポートするサーバー言語のチェック ボックスをオンにし、[次へ ****] をクリックします。  

6.  [クライアント言語の選択 **** ] ページで、そのサイトがサポートするクライアント言語のチェック ボックスをオンにし、[次へ ****] をクリックします。  

7.  [次へ ****] をクリックして、サイトの言語サポートを変更します。  

    > [!NOTE]  
    >  Configuration Manager でサイトのリセットが開始され、サイトのすべてのサイト システムの役割も再インストールされます。  

8.  [閉じる **** ] をクリックしてこの手順を完了します。  

##  <a name="a-namebkmkmoddbalerta-modify-the-database-server-alert-threshold"></a><a name="BKMK_ModDBAlert"></a> データベース サーバーのアラートしきい値を変更する  
 Configuration Manager の既定では、サイト データベース サーバーの空きディスク領域が少なくなると、アラートが発生するようになっています。 既定では、空きディスク領域が 10 GB 以下になると警告アラートが、5 GB 以下になると重大なアラートが発生します。 サイトごとに、このしきい値を変更したり、アラートを無効にしたりすることができます。  

 アラートの設定を変更するには  

1.  [ **管理** ] ワークスペースで [ **サイトの構成**] を展開して、[ **サイト**] をクリックします。  

2.  構成を変更するサイトを選択し、そのサイトの **[プロパティ]** を開きます。  

3.  サイトの **[プロパティ]** ダイアログ ボックスで **[アラート]** タブを選択し、設定を編集します。  

4.  [OK] をクリックし、[プロパティ] ダイアログ ボックスを閉じます。 ****  



<!--HONumber=Jan17_HO1-->

