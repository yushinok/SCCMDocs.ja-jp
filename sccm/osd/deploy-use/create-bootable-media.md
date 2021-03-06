---
title: 起動可能なメディアの作成
titleSuffix: Configuration Manager
description: Configuration Manager の起動可能なメディアは、新しいバージョンの Windows のインストールや、コンピューターの置き換えおよび設定の転送を容易にします。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d3b2ce474488ebf02c3a3c4a82def91d706b6bfc
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351025"
---
# <a name="create-bootable-media-with-system-center-configuration-manager"></a>System Center Configuration Manager を使用した起動可能なメディアの作成

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager の起動可能なメディアには、ブート イメージ、オプションとして起動前コマンドとそれに関連付けられているファイル、および Configuration Manager ファイルが含まれています。 事前設定されたメディアは、次のオペレーティング システムの展開シナリオに使用します。  

-   [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](install-new-windows-version-new-computer-bare-metal.md)  

-   [既存のコンピューターの置き換えと設定の転送](replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="BKMK_CreateBootableMedia"></a> 起動可能なメディアの作成  
 起動可能なメディアを使用して起動すると、展開先のコンピューターが起動し、ネットワークに接続され、指定されたタスク シーケンス、オペレーティング システム イメージ、その他の必要なコンテンツをネットワークから取得します。 タスク シーケンスはメディアにはないため、タスク シーケンスやコンテンツを更新しても、メディアを再作成する必要はありません。 起動可能なメディアのパッケージは暗号化されていません。 メディアにパスワードを設定するなど、適切なセキュリティ手段を講じて、承認されていないユーザーからパッケージのコンテンツを守る必要があります。  

 タスク シーケンス メディアの作成ウィザードを使用して起動可能なメディアを作成する前に、次の条件がすべて満たされていることを確認してください。  

|タスク|説明|  
|----------|-----------------|  
|ブート イメージ|オペレーティング システムを展開するためにタスク シーケンスで使用するブート イメージについて、次の事項を考慮してください。<br /><br /> -   ブート イメージのアーキテクチャが、展開先のコンピューターのアーキテクチャに対して適切である必要があります。 たとえば、x64 のコンピューターでは、x86 または x64 のブート イメージを起動して実行できます。 ただし、x86 のコンピューターで起動して実行できるのは、x86 ブート イメージのみです。<br />-  ブート イメージに、対象コンピューターのプロビジョニングに必要なネットワーク ドライバーと大容量記憶装置ドライバーが含まれている必要があります。|  
|オペレーティング システムを展開するタスク シーケンスを作成する|起動可能なメディアの一部として、オペレーティング システムを展開するタスク シーケンスを指定する必要があります。 新しいタスク シーケンスを作成する手順については、「[オペレーティング システムをインストールするタスク シーケンスの作成](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)」を参照してください。|  
|タスク シーケンスに関連付けられているすべてのコンテンツを配布する|1 つ以上の配布ポイントに対し、タスク シーケンスに必要なすべてのコンテンツを配布する必要があります。 これには、ブート イメージと、その他の関連する起動前ファイルが含まれます。 起動可能なメディアの作成時に、ウィザードによって配布ポイントから情報が収集されます。 その配布ポイントのコンテンツ ライブラリへの **読み取り** アクセス権を持っている必要があります。  詳細については、「[コンテンツ ライブラリについて](../../core/plan-design/hierarchy/the-content-library.md)」を参照してください。|  
|リムーバブル USB ドライブを準備する|リムーバブル USB ドライブの場合:<br /><br /> リムーバブル USB ドライブを使用する場合は、ウィザードが実行されるコンピューターに USB ドライブが接続され、USB ドライブが Windows に取り外し可能なメディアとして検知されている必要があります。 メディアの作成時に、ウィザードによって USB ドライブに直接書き込まれます。 スタンドアロン メディアでは FAT32 ファイル システムが使用されています。 スタンドアロン メディアは、サイズが 4 GB を超えるコンテンツが入っている USB フラッシュ ドライブには作成できません。|  
|出力フォルダーを作成する|CD/DVD セットの場合:<br /><br /> タスク シーケンス メディアの作成ウィザードを実行して CD または DVD セット用のメディアを作成する前に、ウィザードで作成される出力ファイル用のフォルダーを作成する必要があります。 CD または DVD セット用に作成されるメディアは、そのフォルダーに .iso ファイルとして直接書き込まれます。|  

 起動可能なメディアを作成するには、次の手順に従います。  

### <a name="to-create-bootable-media"></a>起動可能なメディアを作成するには  

1.  Configuration Manager コンソールで、**[ソフトウェア ライブラリ]** をクリックします。  

2.  **[ソフトウェア ライブラリ]** ワークスペースで **[オペレーティング システム]** を展開して、**[タスク シーケンス]** をクリックします。  

3.  **[ホーム]** タブの **[作成]** グループで **[タスク シーケンス メディアの作成]** をクリックして、タスク シーケンス メディアの作成ウィザードを起動します。  

4.  **[メディアの種類の選択]** ページで次のオプションを指定し、**[次へ]** をクリックします。  

    -   **[起動可能なメディア]** を選択します。  

    -   必要に応じて、ユーザーの入力なしにオペレーティング システムを展開できるようにするには、**[オペレーティング システムの無人展開を許可する]** を選択します。  

        > [!IMPORTANT]  
        >  このオプションを選択すると、ユーザーはネットワーク構成情報やオプションのタスク シーケンスについてプロンプトされません。 ただし、メディアにパスワード保護が構成されている場合は、パスワードの入力を求めるメッセージがユーザーに表示されます。  

5.  **[メディア管理]** ページで次のオプションのいずれかを指定し、**[次へ]** をクリックします。  

    -   サイト境界内のクライアントの場所に基づいて、ある管理ポイントから別の管理ポイントにメディアをリダイレクトできるようにする場合は、**[動的メディア]** を選択します。  

    -   指定の管理ポイントにのみメディアを接続する必要がある場合は、**[サイトベースのメディア]** を選択します。  

6.  **[メディアの種類]** ページで、メディアがフラッシュ ドライブか、または CD/DVD セットであるかを指定してから、次の構成をクリックします。  

    > [!IMPORTANT]  
    >  スタンドアロン メディアでは FAT32 ファイル システムが使用されています。 スタンドアロン メディアは、サイズが 4 GB を超えるコンテンツが入っている USB フラッシュ ドライブには作成できません。  

    -   **[USB フラッシュ ドライブ]** を選択した場合は、コンテンツを保存するドライブを指定します。  

    -   **CD/DVD セット**を選択した場合は、メディアの容量および出力ファイルの名前とパスを指定します。 この場所に出力ファイルが書き込まれます。 例: **\\\servername\folder\outputfile.iso**  

         メディアにコンテンツ全体を保存しきれない場合は、複数のファイルが作成されます。この場合、複数の CD または DVD を使用してコンテンツを保存する必要があります。 複数のメディアが必要な場合は、Configuration Manager が作成する各出力ファイルの名前に連番が付けられます。 さらに、オペレーティング システムと共にアプリケーションを展開し、アプリケーションが 1 つのメディアに収まらない場合、Configuration Manager は複数のメディアでアプリケーションを保存します。 スタンドアロン メディアを実行している場合、Configuration Manager は、アプリケーションを保存する次のメディアの指定をユーザーに求めます。  

        > [!IMPORTANT]  
        >  既存の .iso イメージを選択した場合は、タスク シーケンス メディア ウィザードの次のページに進むと、ドライブまたは共有フォルダーからイメージが削除されます。 既存のイメージは、ウィザードをキャンセルしても削除されます。  

     **[次へ]** をクリックします。  

7.  **[セキュリティ]** ページで次のオプションを指定し、**[次へ]** をクリックします。  

    -   メディアが Configuration Managerで管理されていないコンピューターにオペレーティング システムを展開できるようにするには、**[不明なコンピューターのサポートを有効にする]** チェックボックスをオンにします。 これらのコンピューターのレコードは Configuration Manager データベースには存在しません。  

         不明なコンピューターには次のようなものがあります。  

        -   Configuration Manager クライアントがインストールされていないコンピューター  

        -   Configuration Manager にインポートされていないコンピューター  

        -   Configuration Manager で検出されていないコンピューター  

    -   メディアを不正アクセスから保護するため、**[メディアをパスワードで保護する]** チェック ボックスをオンにし、強力なパスワードを入力します。 パスワードを指定すると、ユーザーは起動可能なメディアを使用するためにパスワードを入力する必要があります。  

        > [!IMPORTANT]  
        >  セキュリティのベスト プラクティスとして、起動可能なメディアの保護に役立つパスワードを常に割り当てることをお勧めします。  

    -   HTTP 接続用には、**[自己署名入りメディア証明書を作成する]** を選択し、証明書の開始日と有効期限を指定します。  

    -   HTTPS 接続用には、**[PKI 証明書のインポート]** を選択し、インポートする証明書とそのパスワードを指定します。  

         ブート イメージで使用される、このクライアント証明書の詳細については、[PKI 証明書の要件](../../core/plan-design/network/pki-certificate-requirements.md)を参照してください。  

    -   **ユーザーとデバイスのアフィニティ**: Configuration Manager でユーザー中心の管理をサポートするため、ユーザーと対象コンピューターをメディアによって関連付ける方法を指定します。 オペレーティング システムの展開でユーザーとデバイスのアフィニティをサポートする方法については、「[展開先のコンピューターにユーザーを関連付ける](../get-started/associate-users-with-a-destination-computer.md)」をご覧ください。  

        -   メディアがユーザーと対象コンピューターを自動的に関連付けるようにするには、**[ユーザーとデバイスのアフィニティを自動的に承認する]** を選択します。 この機能は、オペレーティング システムを展開するタスク シーケンスのアクションに基づきます。 このシナリオでは、タスク シーケンスが、対象コンピューターにオペレーティング システムを展開するときに、指定のユーザーと対象コンピューターの関係を作成します。  

        -   メディアが承認を待ってユーザーと対象コンピューターを関連付けるようにするには、**[ユーザーとデバイスのアフィニティを管理者の承認待ちにする]** を選択します。 この機能は、オペレーティング システムを展開するタスク シーケンスのスコープに基づきます。  このシナリオでは、タスク シーケンスは、指定のユーザーと対象コンピューターの関係を作成しますが、オペレーティング システムを展開する前に管理ユーザーからの承認を待機します。  

        -   メディアがユーザーと対象コンピューターを関連付けないようにするには、**[ユーザーとデバイスのアフィニティを許可しない]** を選択します。 このシナリオでは、タスク シーケンスは、オペレーティング システムを展開するときにユーザーと対象コンピューターを関連付けません。  

8.  **[ブート イメージ]** ページで、次のオプションを指定してから、**[次へ]** をクリックします。  

    > [!IMPORTANT]  
    >  配布されているブート イメージのアーキテクチャが、対象コンピューターのアーキテクチャに適切である必要があります。 たとえば、x64 のコンピューターでは、x86 または x64 のブート イメージを起動して実行できます。 ただし、x86 のコンピューターで起動して実行できるのは、x86 ブート イメージのみです。  

    -   **[ブート イメージ]** ボックスで、対象コンピューターを起動するブート イメージを指定します。  

    -   **[配布ポイント]** ボックスで、ブート イメージが配置されている配布ポイントを指定します。 配布ポイントからブート イメージが取得されてメディアに書き込まれます。  

        > [!NOTE]  
        >  配布ポイントのコンテンツ ライブラリに対し、 **読み取り** アクセス権を持っている必要があります。  

    -   ウィザードの **[メディア管理]** ページでサイトベースの起動可能なメディアを作成する場合は、 **[管理ポイント]** ボックスでプライマリ サイトの管理ポイントを指定します。  

    -   ウィザードの **[メディア管理]** ページで動的起動可能メディアを作成する場合は、 **[関連付けられている管理ポイント]** ボックスで、使用するプライマリ サイトの管理ポイントと、初期通信での優先順位を指定します。  

9. **[カスタマイズ]** ページで、次のオプションを指定してから、**[次へ]** をクリックします。  

    -   オペレーティング システムを展開するためにタスク シーケンスで使用する変数を指定します。  

    -   タスク シーケンスを実行する前に実行する起動前コマンドを指定します。 起動前コマンドは、タスク シーケンスを実行してオペレーティング システムをインストールする前に、Windows PE でユーザーと対話できるスクリプトまたは実行可能ファイルです。 詳細については、「[タスク シーケンス メディアの起動前コマンド](../understand/prestart-commands-for-task-sequence-media.md)」を参照してください。  

        > [!TIP]  
        >  タスク シーケンス メディアの作成中に、パッケージ ID と起動前コマンドライン (タスク シーケンスの変数の値を含む) が、Configuration Manager コンソールを実行しているコンピューターの CreateTSMedia.log というログファイルに書き込まれます。 このログ ファイルで、タスク シーケンスの変数の値を確認できます。  

         必要に応じて、**[起動前コマンドにファイルを含める]** チェック ボックスをオンにして、起動前コマンドに必要なファイルを含めます。  

10. ウィザードを完了します。  

## <a name="create-bootable-media-on-a-usb-drive-from-a-network-share"></a>ネットワーク共有から USB ドライブで起動可能なメディアを作成する
このセクションの情報は、Configuration Manager コンソールを実行しているコンピューターに USB フラッシュ ドライブが接続されているときに、そのフラッシュ ドライブで起動可能なメディアを作成する場合に役立ちます。 USB ドライブに起動可能なメディアを作成する場合、タスク シーケンス起動メディアを作成して、ISO をマウントし、ISO から USB ドライブにファイルを転送することができます。

1. [タスク シーケンス起動メディアを作成します](#to-create-task-boobable-media)。 **[メディアの種類]** ページで、**[CD/DVD セット]** を選択します。 ウィザードで指定した場所に出力ファイルが書き込まれます。 たとえば、**\\\servername\folder\outputfile.iso** のようになります。  
2. リムーバブル USB ドライブを準備します。 ドライブは書式設定され、空であり、かつ、起動可能である必要があります。
3. 共有の場所から ISO をマウントし、ISO イメージから USB ドライブにファイルを転送します。

## <a name="next-steps"></a>次のステップ  
[起動可能なメディアを使用したネットワーク経由での Windows の展開](use-bootable-media-to-deploy-windows-over-the-network.md)  
