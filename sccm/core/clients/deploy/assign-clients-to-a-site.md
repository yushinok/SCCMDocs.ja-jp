---
title: "クライアントをサイトに割り当てる | System Center Configuration Manager"
description: "System Center Configuration Manager でクライアントをサイトに割り当てます。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ba9b623f-6e86-4006-93f2-83d563de0cd0
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 3540b178bf8d7c6473b94a7300578ed7cf0dce29

---
# <a name="how-to-assign-clients-to-a-site-in-system-center-configuration-manager"></a>System Center Configuration Manager でクライアントをサイトに割り当てる方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager クライアントをインストールした後、それを管理するには、Configuration Manager プライマリ サイトに参加させる必要があります。 クライアントが参加するサイトのことを、割り当てられたサイトと呼びます。 クライアントを中央管理サイトまたはセカンダリ サイトに割り当てることはできません。  

 割り当て処理は、クライアントが正常にインストールされると実行され、どのサイトがクライアント コンピューターを管理するかが決まります。 Configuration Manager の登録中にモバイル デバイス クライアントをインストールする場合、この処理で常に、モバイル デバイスがサイトに自動的に割り当てられます。 クライアントをコンピューターにインストールするときに、クライアントをサイトに割り当てることができます。または、サイトに割り当てずに、クライアントを単にインストールすることもできます。 ただし、クライアントをインストールしたが割り当てていない場合、サイトの割り当てが正常に行われるまで、クライアントは管理されません。  

 クライアント コンピューターを割り当てるには、クライアントをサイトに直接割り当てるか、またはサイトの自動割り当てを使用できます。サイトの自動割り当てでは、クライアントは自動的に、現在のネットワークの場所に基づいて適切なサイトを検出するか、階層に構成されているフォールバック サイトを検出します。  

> [!NOTE]  
>  常に同じバージョンの Configuration Manager のサイトにクライアントを割り当てます。 新リリースの Configuration Manager クライアントを古いリリースのサイトに割り当てないでください。   必要に応じて、クライアントに使用している同じ Configuration Manager バージョンにプライマリ サイトを更新します。  

 クライアントは、サイトに割り当てられると、IP アドレスを変更したり別のサイトにローミングする場合でも、このサイトに割り当てられたままになります。 管理者のみが、後から手動でクライアントを別のサイトに割り当てたり、クライアントの割り当てを削除したりできます。  

> [!WARNING]  
>  書き込みフィルターを有効にしたときに、サイトに割り当てられたままになるクライアントの例外は、Windows Embedded デバイスのクライアントを割り当てる場合です。 クライアントを割り当てる前に書き込みフィルターを無効にしなかった場合、そのクライアントは、デバイスの次回の再起動時にサイトの割り当ての状態が元の状態に戻ります。  
>   
>  たとえば、クライアントに自動サイト割り当てが構成されている場合、スタートアップ時に再割り当てが実行され、別にサイトに割り当てられることがあります。 クライアントに自動サイト割り当てが構成されておらず、手動でサイトを割り当てる必要がある場合、Configuration Manager でこのクライアントをまた管理できるようにするには、スタートアップ後にクライアントの再割り当てを実行する必要があります。  
>   
>  この動作を防ぐには、書き込みフィルターを無効にしてから、組み込みデバイスのクライアントを割り当てます。そしてサイトの割り当てが成功したことを確認してから、書き込みフィルターを有効にします。  

 クライアントのサイトへの割り当てが失敗した場合、クライアント ソフトウェアはインストールされたままですが、管理されません。 クライアントがインストールされているがサイトに割り当てられていない場合、またはサイトに割り当てられているが管理ポイントと通信できない場合、クライアントは管理されていないと見なされます。  

##  <a name="a-namebkmkmanualassignmenta-using-manual-site-assignment-for-computers"></a><a name="BKMK_ManualAssignment"></a> コンピューターにサイトの手動割り当てを使用する  
 次の 2 つの方法を使用して、クライアント コンピューターを手動でサイトに割り当てることができます。  

-   サイト コードを指定するクライアント インストールのプロパティを使用する  

-   コントロール パネルの [Configuration Manager ****] でサイト コードを指定する  

> [!NOTE]  
>  クライアント コンピューターを存在しない Configuration Manager サイト コードに手動で割り当てると、サイトの割り当ては失敗します。 クライアントはインストールされたままですが、有効な Configuration Manager サイトに割り当てられるまで管理されません。  

##  <a name="a-namebkmkautomaticassignmenta-using-automatic-site-assignment-for-computers"></a><a name="BKMK_AutomaticAssignment"></a> コンピューターにサイトの自動割り当てを使用する  
 サイトの自動割り当ては、クライアントの展開時に実行できます。または [Configuration Manager のプロパティ **** ] の [詳細設定 **** ] タブにある [サイトの探索 **** ] をクリックしても、実行できます。 Configuration Manager クライアントは、自身のネットワークの場所を、Configuration Manager 階層内に構成されている境界と比較します。 クライアントのネットワークの場所が、サイトの割り当てが有効な境界グループ内にある場合や、階層がフォールバック サイト用に構成されている場合、サイト コードを指定する必要なく、クライアントは自動的にそのサイトに割り当てられます。  

 次の 1 つまたは複数を使用して境界を構成できます。  

-   IP サブネット  

-   Active Directory サイト  

-   IP v6 プレフィックス  

-   IP アドレスの範囲  

> [!NOTE]  
>  Configuration Manager クライアントに複数のネットワーク アダプター (LAN ネットワーク アダプターやダイヤルアップ モデムなど) があるため、複数の IP アドレスがある場合、クライアントのサイト割り当ての評価に使用される IP アドレスは暫定的なアドレスです。  

 サイトの割り当て用に境界グループを構成する方法、およびサイトの自動割り当て用にフォールバック サイトを構成する方法については、「 [Define site boundaries and boundary groups for System Center Configuration Manager](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)」をご覧ください。  

 Configuration Manager クライアントは、Active Directory Domain Services に発行されているサイトの境界グループを検出するように試みます。 この方法が失敗した場合 (Active Directory スキーマが Configuration Manager 用に拡張されていない場合や、クライアントがワークグループ コンピューターでない場合など)、クライアントは管理ポイントで境界情報を検出することができます。  

 インストール時に、クライアント コンピューターで使用する管理ポイントを指定できます。または、DNS 発行や WINS を使用してクライアントによって管理ポイントを検出することもできます。  

 ネットワークの場所が含まれている境界グループに関連付けられたサイトをクライアントが検出することができず、階層にフォールバック サイトがない場合、クライアントは、サイトに割り当てられるまで 10 分ごとに再試行します。  

 Configuration Manager クライアント コンピューターをサイトに自動的に割り当てることはできないため、手動で割り当てる必要があります。  

-   クライアントが現在、サイトに割り当てられている  

-   クライアントがインターネット上にあるか、イントラネット専用のクライアントとして構成されている  

-   クライアントのネットワークの場所が、Configuration Manager 階層内の構成された境界グループ内に存在せず、階層にフォールバック サイトが存在しない  

##  <a name="a-namebkmksitecompatibilitya-completing-site-assignment-by-checking-site-compatibility"></a><a name="BKMK_SiteCompatibility"></a> サイトの互換性をチェックしてサイトの割り当てを完了する  
 割り当てられたサイトがクライアントによって検出されると、Configuration Manager サイトがクライアントを管理できることを確認するため、クライアントのバージョンとオペレーティング システムがチェックされます。 たとえば、Configuration Manager では、Configuration Manager 2007 クライアント、System Center 2012 Configuration Manager クライアント、または Windows 2000 を実行しているクライアントを管理することができません。  

 Windows 2000 を実行しているクライアントを Configuration Manager サイトに割り当てると、サイトの割り当てが失敗するのに対して、Configuration Manager 2007 クライアントまたは System Center 2012 Configuration Manager クライアントを Configuration Manager (現在のブランチ) サイトに割り当てると、サイトの割り当てが成功して、クライアントの自動アップグレードがサポートされます。 ただし、古い世代のクライアントが Configuration Manager (現在のブランチ) クライアントにアップグレードされるまで、Configuration Manager はクライアント設定、アプリケーション、またはソフトウェア更新プログラムを使用してこのクライアントを管理できません。  

> [!NOTE]  
>  Configuration Manager (現在のブランチ) サイトに対する Configuration Manager 2007 または System Center 2012 Configuration Manager クライアントのサイトの割り当てをサポートするには、階層の自動クライアント アップグレードを構成する必要があります。 詳細については、「[System Center Configuration Manager で Windows コンピューター用クライアントをアップグレードする方法](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)」を参照してください。  

 また、Configuration Manager では、Configuration Manager (現在のブランチ) クライアントをサポートしているサイトにそのクライアントが割り当てられていることも確認します。 Configuration Manager の以前のバージョンから移行する移行期間中に生じる可能性があるシナリオは次のとおりです。  

-   シナリオ: サイトの自動割り当てを使用していて、境界が、以前のバージョンの Configuration Manager で定義されている境界と重複する。  

     この場合、クライアントは Configuration Manager (現在のブランチ) サイトの検索を自動的に試行します。  

     最初にクライアントは、Active Directory Domain Services を確認します。発行されている Configuration Manager (現在のブランチ) サイトが見つかった場合は、サイトの割り当てが成功します。 これが成功しなかった (たとえば、Configuration Manager (現在のブランチ) サイトが公開されていない場合や、コンピューターがワークグループ クライアントである) 場合には、クライアントは、割り当てられている管理ポイントからのサイト情報を確認します。  

    > [!NOTE]  
    >  クライアントのインストール時に、Client.msi のプロパティ **SMSMP=&lt;server_name>** を使用して、クライアントに管理ポイントを割り当てることができます。  

     どちらの方法も失敗した場合は、サイト割り当てが失敗し、クライアントを手動で割り当てる必要があります。  

-   シナリオ: サイトの自動割り当てを使用せずに、特定のサイト コードを使用して Configuration Manager (現在のブランチ) クライアントを割り当てたときに、System Center 2012 R2 Configuration Manager より前のバージョンの Configuration Manager のサイト コードを誤って指定した。  

     この場合は、サイトの割り当ては失敗します。クライアントを Configuration Manager (現在のブランチ) サイトに手動で再び割り当てる必要があります。  

 サイト互換性チェックには、次のうちいずれかの条件が必要です。  

-   クライアントが、Active Directory ドメイン サービスに発行されているサイト情報にアクセスできる  

-   クライアントが、サイト内の管理ポイントと通信できる  

 サイト互換性チェックが正常に完了しない場合、サイトの割り当ては失敗し、サイト互換性チェックが再度実行されて正常に完了するまで、クライアントは管理されないままになります。  

 サイト互換性チェックは、クライアントがインターネット ベースの管理ポイント用に構成されている場合は、例外的に実行されません。 このシナリオでは、サイト互換性チェックは実行されません。 クライアントをインターネット ベースのサイト システムが含まれているサイトに割り当てて、インターネット ベースの管理ポイントを指定する場合は、クライアントを正しいサイトに割り当てていることを確認する必要があります。 Configuration Manager 2007 サイト、System Center 2012 Configuration Manager サイト、またはインターネット ベースのサイト システムのない Configuration Manager サイトに誤ってクライアントを割り当てた場合、このクライアントは管理されません。  

##  <a name="a-namebkmklocatingmpsa-locating-management-points"></a><a name="BKMK_LocatingMPs"></a> 管理ポイントを検出する  
 クライアントは、サイトに正常に割り当てられると、サイト内の管理ポイントを検出します。  

 クライアント コンピューターは、サイト内の接続可能な管理ポイントの一覧をダウンロードします。 このプロセスは、クライアントの再起動、25 時間ごと、およびクライアントがネットワークの変更 (ネットワークでのコンピューターの切断や再接続、新しい IP アドレスの受信など) を検出したタイミングで実行されます。 一覧には、イントラネットの管理ポイントと、HTTP 経由と HTTPS 経由のいずれのクライアント接続を受け入れるかの情報が含まれます。 クライアント コンピューターがインターネット上にあり、クライアントに管理ポイントの一覧がない場合、クライアントは、指定されたインターネット ベースの管理ポイントに接続して管理ポイントの一覧を取得します。 割り当てられたサイトの管理ポイントの一覧がある場合、クライアントはいずれかの管理ポイントを選択して接続します。  

-   クライアントがイントラネット上にあり、使用できる有効な PKI 証明書がある場合、クライアントは HTTP 管理ポイントの前に HTTPS 管理ポイントを選択します。 その後、フォレストのメンバーシップに基づいて、最も近い管理ポイントを見つけます。  

-   クライアントがインターネット上にある場合、クアイアントはインターネット ベースの管理ポイントのいずれかを無作為に選択します。  

 Configuration Manager に登録されているモバイル デバイス クライアントは、割り当てられたサイトの 1 つの管理ポイントにのみ接続し、セカンダリ サイトの管理ポイントには接続しません。 これらのクライアントは常に HTTPS 経由で接続するため、インターネット経由のクライアント接続を受け入れるように管理ポイントを構成する必要があります。 プライマリ サイトにモバイル デバイス クライアント用の複数の管理ポイントがある場合、Configuration Manager は、割り当て時にこれらの管理ポイントのいずれかを無作為に選択し、モバイル デバイス クライアントは同じ管理ポイントを使用し続けます。  

 クライアントがサイト内の管理ポイントからクライアント ポリシーをダウンロードすると、クライアントは管理されたクライアントになります。  

##  <a name="a-namebkmkdownloadsitesettingsa-downloading-site-settings"></a><a name="BKMK_DownloadSiteSettings"></a> サイト設定をダウンロードする  
 サイト割り当てが完了し、クライアントが管理ポイントを検出すると、サイト互換性チェックに Active Directory ドメイン サービスを使用するクライアント コンピューターは、割り当てられたサイトのクライアント関連のサイト設定をダウンロードします。 これらの設定には、クライアント証明書の選択条件、証明書失効リストを使用するかどうか、およびクライアント要求のポート番号が含まれています。 クライアントはこれらの設定を定期的に確認します。  

 Active Directory ドメイン サービスからサイト設定を取得できない場合、クライアント コンピューターは管理ポイントからサイト設定をダウンロードします。 クライアント コンピューターは、クライアント プッシュを使用したインストール時にサイト設定を取得することもできます。また、CCMSetup.exe とクライアント インストールのプロパティを使用して手動で指定することもできます。 クライアント インストールのプロパティの詳細については、「[System Center Configuration Manager のクライアント インストール プロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)」を参照してください。  

##  <a name="a-namebkmkdownloadclientsettingsa-downloading-client-settings"></a><a name="BKMK_DownloadClientSettings"></a> クライアント設定をダウンロードする  
 すべてのクライアントが、既定のクライアント設定ポリシーと適切なカスタムのクライアント設定ポリシーをダウンロードします。 ソフトウェア センターは、Windows コンピューターのこれらのクライアント構成ポリシーを使用するため、この構成情報がダウンロードされるまでソフトウェア センターが正常に実行されないことをユーザーに通知します。 構成されているクライアント設定によっては、クライアント設定の初回ダウンロードに時間がかかることがあります。また、このプロセスが完了するまで、一部の管理タスクが実行されない可能性があります。  

##  <a name="a-namebkmkverifyassignmenta-verifying-site-assignment"></a><a name="BKMK_VerifyAssignment"></a> サイト割り当てを確認する  
 次のいずれかの方法を使用して、サイト割り当てが正常に行われていることを確認できます。  

-   Windows コンピューターのクライアントには、コントロール パネルの Configuration Manager を使用し、[**サイト**] タブにサイト コードが正しく表示されることを確認します。  

-   クライアント コンピューターの場合、[資産とコンプライアンス **** ] ワークスペースの [デバイス **** ] ノードを使用して、コンピューターの [クライアント **** ] 列に [はい **** ] が表示され、[サイト コード **** ] 列に正しいプライマリ サイト コードが表示されることを確認する  

-   モバイル デバイス クライアントの場合、[資産とコンプライアンス **** ] ワークスペースの [すべてのモバイル デバイス **** ] コレクションを使用して、モバイル デバイスの [クライアント **** ] 列に [はい **** ] が表示され、[サイト コード **** ] 列に正しいプライマリ サイト コードが表示されることを確認する  

-   クライアント割り当てとモバイル デバイス登録のレポートを使用する  

-   クライアント コンピューターの場合、クライアント上の LocationServices.log ファイルを使用する  

##  <a name="a-namebkmkroaminga-roaming-to-other-sites"></a><a name="BKMK_Roaming"></a> 他のサイトにローミングする  
 イントラネット上のクライアント コンピューターがプライマリ サイトに割り当てられており、別のサイトに構成されている境界グループに入るようにネットワークの場所が変更された場合、これらのクライアント コンピューターは別のサイトにローミングされます。 このサイトが、割り当てられたサイトのセカンダリ サイトである場合、クライアントはセカンダリ内の管理ポイントを使用してクライアント ポリシーのダウンロードとクライアント データのアップロードを行うため、このデータは低速ネットワーク経由では送信されません。 ただし、これらのクライアントが、別のプライマリ サイトの境界または割り当てられたサイトの子サイトでないセカンダリの境界にローミングする場合、これらのクライアントは常に、割り当てられたサイト内の管理ポイントを使用して、クライアント ポリシーのダウンロードとサイトへのデータのアップロードを行います。  

 ほかのサイト (すべてのプライマリ サイトとすべてのセカンダリ サイト) にローミングするこれらのクライアント コンピューターは、コンテンツの場所を要求するため、いつでもほかのサイトの管理ポイントを使用できます。 現在のサイトの管理ポイントは、クライアントが要求するコンテンツを持つ配布ポイントの一覧を、クライアントに渡すことができます。  

 インターネットのみで管理されるように構成されたクライアント コンピューターや、Configuration Manager に登録された Mac コンピューターおよびモバイル デバイス用に構成されたクライアント コンピューターの場合は、クライアントは割り当てられたサイトの管理ポイントとのみ通信します。 これらのクライアントは、セカンダリ サイトの管理ポイントや、ほかのプライマリ サイトの管理ポイントと通信することは一切ありません。  



<!--HONumber=Nov16_HO1-->

