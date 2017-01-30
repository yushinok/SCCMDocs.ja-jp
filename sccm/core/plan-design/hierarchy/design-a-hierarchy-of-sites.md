---
title: "System Center Configuration Manager のサイト階層の設計 | Microsoft Docs"
description: "System Center Configuration Manager で使用できるトポロジと管理オプションを理解することで、サイト階層を計画することができます。"
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
caps.latest.revision: 22
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f1e6213c5d28a3219f976b2c92f193b05fed15ce
ms.openlocfilehash: 805184a3e3913d93fa57c0742adf48955175df7f


---
# <a name="design-a-hierarchy-of-sites-for-system-center-configuration-manager"></a>System Center Configuration Manager のサイト階層の設計

*適用対象: System Center Configuration Manager (Current Branch)*

新しい System Center Configuration Manager 階層の最初のサイトをインストールする前に、Configuration Manager で使用可能なトポロジ、利用可能なサイトの種類と相互の関係、各種のサイトで提供される管理のスコープを理解しておくことをお勧めします。
次に、インストールする必要のあるサイトの数を減らすためのコンテンツ管理オプションを検討し、それから現在のビジネス ニーズに対して効率的に機能し、将来の成長の管理のために拡張できるトポロジを計画します。  

> [!NOTE]
> Configuration Manager の新規インストールを計画するときは、[リリース ノート]( /sccm/core/servers/deploy/install/release-notes)でアクティブなバージョンでの現在の問題の詳細を確認してください。 リリース ノートは、Configuration Manager のすべてのブランチに適用されます。  ただし、[Technical Preview ブランチ]( /sccm/core/get-started/technical-preview)を使用する場合は、Technical Preview の各バージョンのドキュメントで、そのブランチにのみ固有の問題を確認してください。  

##  <a name="a-namebkmktopologya-hierarchy-topology"></a><a name="bkmk_topology"></a> 階層トポロジ  
 階層トポロジの範囲は、単一のスタンドアロンのプライマリ サイトから、階層の最上位 (上位層) にある中央管理サイトに接続されているプライマリ サイトおよびセカンダリ サイトのグループに及びます。   通常、階層で使用するサイトの種類と数を決定するうえで重要となるのは、次のような、サポートする必要があるデバイスの数と種類です。   

 **スタンドアロンのプライマリ サイト:**&1; つのプライマリ サイトですべてのデバイスおよびユーザーの管理をサポートできる場合には、スタンドアロン プライマリ サイトを使用します (「[サイジングとスケールの数値](/sccm/core/plan-design/configs/size-and-scale-numbers)」をご覧ください)。 このトポロジは、会社の複数の地理的な場所を&1; つのプライマリ サイトで正常にサービスできる場合にも有効です。  ネットワーク トラフィックを管理する場合、優先管理ポイントと、慎重に計画されたコンテンツ インフラストラクチャを使用できます (「[System Center Configuration Manager でのコンテンツ管理の基本的な概念](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)」を参照してください)。  

 このトポロジの利点は次のとおりです。  

-   管理オーバーヘッドが簡略化される。  

-   クライアント サイトの割り当てと、使用可能なリソースとサービスの検出が簡略化される。  

-   サイト間におけるデータベース レプリケーションによって生じる可能性がある遅延を解消する。

-   スタントアロンのプライマリ階層を、中央管理サイトを使用した、より大きな階層に拡張することもできる。 このようにすると、新しいプライマリ サイトをインストールして、展開の規模を大きくできます。  


**1 つ以上の子プライマリ サイトが含まれる中央管理サイト:** このトポロジは、すべてのデバイスとユーザーの管理をサポートするのに複数のプライマリ サイトが必要な場合に使用します。  これは、複数のプライマリ サイトを使用する必要がある場合には必須です。 このトポロジの利点は次のとおりです。  


-   階層の規模を拡張するために、最大で 25 のプライマリ サイトがサポートされる。  

-   常に中央管理サイトを使用する (サイトを再インストールする場合を除く)。 これは永続的なオプションです。 子プライマリ サイトを切り離して、スタンドアロンのプライマリ サイトにすることはできません。

 次のセクションは、どんな状況で、特定のサイトを使用するか、または追加のサイトの代わりに、コンテンツ管理オプションを使用するかを理解するのに役立ちます。  

##  <a name="a-namebkmkchoosecasa-determine-when-to-use-a-central-administration-site"></a><a name="BKMK_ChooseCAS"></a> 中央管理サイトを使用する場合の判別  
 中央管理サイトは、階層全体の設定を構成して、階層内のすべてのサイトとオブジェクトを監視する場所です。 このサイトの種類では、クライアントを直接管理しませんが、階層全体のサイトやクライアントの構成を含め、サイト間のデータ レプリケーションを調整します。  

**以下の情報を参考にして、中央管理サイトをインストールするかどうかを判別できます。**  

-   中央管理サイトは、階層の最上位のサイトです。  

-   複数のプライマリ サイトが含まれる階層を構成する場合は、中央管理サイトをインストールする必要があります。また、中央管理サイトが、インストールする最初のサイトである必要があります。  

-   中央管理サイトは、プライマリ サイトのみ子サイトとしてサポートします。  

-   中央管理サイトにクライアントを割り当てることはできません。  

-   中央管理サイトは、管理ポイントや配布ポイントなどのクライアントを直接サポートするサイト システムの役割はサポートしていません。  

-   中央管理サイトに接続された Configuration Manager コンソールを使用している場合、階層内のすべてのクライアントを管理して、任意の子サイトに対してサイト管理タスクを実行できます。 これには、子プライマリ サイトまたはセカンダリ サイトにおける管理ポイントや他のサイト システムの役割のインストールが含まれる場合があります。  

-   中央管理サイトを使用する場合、中央管理サイトは、ご使用の階層内のすべてのサイトのサイト データを表示できる唯一の場所です。 このデータには、インベントリ データやステータス メッセージなどの情報が含まれます。  

-   個々のサイトで実行する探索方法を割り当てて、中央管理サイトから階層全体の探索処理を構成できます。  

-   別々のセキュリティ ロール、セキュリティ スコープ、およびコレクションを異なる管理ユーザーに割り当てて、階層全体のセキュリティを管理できます。 この構成は、階層内の各サイトに適用されます。  

-   ファイル レプリケーションとデータベース レプリケーションを構成し、階層内のサイト間の通信を制御できます。 これには、サイト データのデータベース レプリケーションのスケジュール設定と、サイト間のファイルベースのデータの転送に使用する帯域幅の管理が含まれます。  

##  <a name="a-namebkmkchoosepriimarya-determine-when-to-use-a-primary-site"></a><a name="BKMK_ChoosePriimary"></a> プライマリ サイトを使用する場合の判別  
 プライマリ サイトは、クライアントを管理するために使用します。 プライマリ サイトは、中央管理サイトの下の子プライマリ サイトとしてインストールするか、新しいサイトの&1; 番目のサイトとしてインストールすることができます。 階層の&1; 番目のサイトとしてインストールされたプライマリ サイトでは、スタンドアロン プライマリ サイトが作成されます。 子プライマリ サイトもスタンドアロン プライマリサイトも、その子としてセカンダリ サイトを持つことができます。  

 次のような場合にプライマリ サイトの使用を検討します。  

-   デバイスとユーザーを管理するため。  

-   1 つの階層で管理できるデバイスの数を増やすため。  

-   展開の管理用に追加の接続ポイントを提供するため。  

-   組織の管理要件を満たすため。 たとえば、リモートの場所にプライマリ サイトをインストールして、低帯域幅のネットワーク経由で展開コンテンツの転送を管理できます。 ただし、System Center Configuration Manager では、データを配布ポイントに転送するときのネットワーク帯域幅を調整するオプションを使用できます。 そのコンテンツ管理機能を使用すれば、追加のサイトをインストールしなくて済みます。  


**以下の情報は、プライマリ サイトをいつインストールするかを決めるのに役立ちます。**  

-   プライマリ サイトをスタンドアロン プライマリ サイトにすることも、大規模な階層内の子プライマリ サイトにすることもできます。 中央管理サイトのある階層にプライマリ サイトを含める場合は、これらのサイト間でデータベースのレプリケーションが行われます。 大量のクライアントとデバイスがあり、1 つのプライマリ サイトでは管理しきれない場合を除き、スタンドアロン プライマリ サイトをインストールすることを検討してください。  スタンドアロンのプライマリ サイトがインストールされたら、展開を拡大するために新しい中央管理サイトに報告するように拡張できます。  

-   プライマリ サイトの親になれるのは、中央管理サイトだけです。  

-   プライマリ サイトの子になれるのは、セカンダリ サイトだけで、複数のセカンダリ子サイトをサポートすることもできます。  

-   プライマリ サイトは、割り当てられたクライアントのすべてのクライアント データを処理します。  

-   プライマリ サイトは、データベース レプリケーションを使用して中央管理サイトと直接通信します (新しいサイトをインストールすると、自動的に構成されます)。  

##  <a name="a-namebkmkchoosesecondarya-determine-when-to-use-a-secondary-site"></a><a name="BKMK_ChooseSecondary"></a> セカンダリ サイトを使用する場合の判別  
 セカンダリ サイトは、低帯域幅のネットワーク経由で展開コンテンツとクライアント データの転送を管理するために使用します。  

 セカンダリ サイトは、中央管理サイトまたはセカンダリ サイトの直接の親プライマリ サイトから管理します。 セカンダリ サイトは、プライマリ サイトに接続されている必要があります。また、セカンダリ サイトを別の親サイトに移動するには、セカンダリ サイトをアンインストールして新しいプライマリ サイトの下に子サイトとして再インストールする必要があります。

ただし、2 つのピアのセカンダリ サイト間でコンテンツをルーティングでき、展開コンテンツのファイルベースのレプリケーションを管理するのに役立ちます。 セカンダリ サイトは、クライアント データをプライマリ サイトに転送するために、ファイルベースのレプリケーションを使用します。 親プライマリ サイトと通信するために、データベース レプリケーションも使用します。  

 次の条件のいずれかが当てはまる場合は、セカンダリ サイトのインストールを検討します。  

-   管理ユーザーのローカル接続ポイントは必要ありません。  

-   階層内の下位サイトへの展開コンテンツの転送を管理する必要があります。  

-   階層内の上位サイトに送信されるクライアント情報を管理する必要があります。  

 セカンダリ サイトをインストールしないことを希望しており、リモートの場所にクライアントがある場合は、Windows BranchCache を使用すること、または帯域幅の制御とスケジューリングに対応した配布ポイントをインストールすることを検討します。 これらのコンテンツ管理オプションはセカンダリ サイトに関係なく使用でき、インストールが必要なサイトとサーバーの数を削減するのに役立ちます。 Configuration Manager でのコンテンツ管理オプションの詳細については、「[コンテンツ管理オプションを使用する場合の判別](#BKMK_ChooseSecondaryorDP)」をご覧ください。  


**以下の情報を参考にして、セカンダリ サイトをインストールするかどうかを判別できます。**  

-   セカンダリ サイトでは、SQL Server のローカル インスタンスが使用できない場合、サイトのインストール時に SQL Server Express が自動的にインストールされます。  

-   セカンダリ サイトのインストールは、コンピューター上でセットアップを直接実行するのではなく、Configuration Manager コンソールから開始されます。  

-   セカンダリ サイトは、サイト データベース内の情報の一部を使用します。それにより、親プライマリ サイトとセカンダリ サイト間のデータベースのレプリケーションによって複製されるデータ量が削減されます。  

-   セカンダリ サイトは、共通の親プライマリ サイトを持つ他のセカンダリ サイトへの、ファイルベースのコンテンツのルーティングをサポートします。  

-   セカンダリ サイトのインストール時に、管理ポイントと配布ポイントが自動的に展開されて、セカンダリ サイト サーバーに配置されます。  

##  <a name="a-namebkmkchoosesecondaryordpa-determine-when-to-use-content-management-options"></a><a name="BKMK_ChooseSecondaryorDP"></a> コンテンツ管理オプションを使用する場合の判別  
 リモートのネットワークの場所にクライアントがある場合、プライマリ サイトまたはセカンダリ サイトの代わりにコンテンツ管理オプションを使用することを検討します。 Windows BranchCache を使用するか、帯域幅制御に配布ポイントを構成するか、または配布ポイントにコンテンツを手動でコピー (コンテンツを事前準備) すると、多くの場合、サイトをインストールする必要がなくなります。  


**次のいずれかの条件が当てはまる場合は、別のサイトをインストールするのではなく、配布ポイントを展開することを検討します。**  

-   ネットワーク帯域幅が、リモートの場所のクライアント コンピューターが管理ポイントと通信してクライアント ポリシーをダウンロードしたり、インベントリ、レポート ステータス、および探索情報を送信するのに十分である。  

-   バックグラウンド インテリジェント転送サービス (BITS) では、ネットワーク要件に対応する十分な帯域幅制御は提供されません。  

 Configuration Manager でのコンテンツ管理オプションの詳細については、「[System Center Configuration Manager でのコンテンツ管理の基本的な概念](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)」をご覧ください。  

##  <a name="a-namebkmkbeyonda-beyond-hierarchy-topology"></a><a name="bkmk_beyond"></a> 階層トポロジ以外  
 最初の階層トポロジに加え、階層内の別のサイトでどのようなサービスまたは機能が使用できるか (サイト システムの役割)、インフラストラクチャ内で階層規模の構成や機能をどのように管理するかも検討してください。 次の一般的な考慮事項は別のトピックで説明します。 これらは、階層の設計によって影響を与えたり、受けたりする可能性があるため、重要です。  

-   [System Center Configuration Manager を使用したコンピューターおよびデバイスの管理を行う](/sccm/core/clients/manage/manage-clients)準備をする場合、管理するデバイスがオンプレミスまたはクラウドに配置されているか、あるいはユーザーが所有するデバイス (BYOD) が含まれるかどうかを検討します。  さらに、Configuration Manager によって直接、または Microsoft Intune との統合によって管理できる Windows 10 コンピューターなどの、複数の管理オプションによってサポートされるデバイスを管理する方法を検討します。  

-   利用可能なネットワーク インフラストラクチャが、リモートの場所の間のデータ フローにどのような影響を及ぼすかを理解します (「[System Center Configuration Manager のネットワーク環境の準備](/sccm/core/plan-design/network/configure-firewalls-ports-domains)」をご覧ください)。 また、管理対象のユーザーとデバイスが配置されている地理的な場所、およびユーザーやデバイスが対象のインフラストラクチャにアクセスするときに会社のドメインとインターネットのどちらを使用するかを検討します。  

-   管理対象デバイスに展開する情報 (ファイルとアプリ) を効率的に配布するためのコンテンツ インフラストラクチャを計画します (「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」をご覧ください)。  

-   使用する予定の [System Center Configuration Manager の特徴と機能](../../../core/plan-design/changes/features-and-capabilities.md)、必要とされるサイト システムの役割または Windows インフラストラクチャ、ネットワークやサーバー リソースを最も効率的に使用するために複数のサイト階層内のどのサイトにそれらの特徴や機能を展開するかを決定します。  

-   PKI の使用を含む、データとデバイスのセキュリティを検討します。 「[System Center Configuration Manager での PKI 証明書の要件](../../../core/plan-design/network/pki-certificate-requirements.md)」を参照してください。  


**サイト固有の構成については、次のリソースを確認ください。**  

-   [System Center Configuration Manager の SMS プロバイダーの計画](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)  

-   [System Center Configuration Manager のサイト データベースの計画](../../../core/plan-design/hierarchy/plan-for-the-site-database.md)  

-   [System Center Configuration Manager のサイト システム サーバーとサイト システムの役割の計画](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)  

-   [System Center Configuration Manager でのセキュリティの計画](../../../core/plan-design/security/plan-for-security.md)  

-   [Managing network bandwidth](../../../core/plan-design/hierarchy/manage-network-bandwidth.md) (サイト内のコンテンツを展開するとき)  


**複数のサイトと階層にまたがる構成について考慮します。**  

-   サイトおよび階層のための [System Center Configuration Manager の高可用性オプション](/sccm/protect/understand/high-availability-options)

-   [System Center Configuration Manager 向けの Active Directory スキーマの拡張](../../../core/plan-design/network/extend-the-active-directory-schema.md)および、[System Center Configuration Manager のサイト データを発行](../../../core/servers/deploy/configure/publish-site-data.md)するためのサイトの構成  

-   [System Center Configuration Manager のサイト間でのデータの転送](../../../core/servers/manage/data-transfers-between-sites.md)  

-   [System Center Configuration Manager のロール ベース管理の基礎](../../../core/understand/fundamentals-of-role-based-administration.md)



<!--HONumber=Jan17_HO1-->

