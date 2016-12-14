---
title: "System Center Configuration Manager クライアントを使用せずに管理されている Android デバイスと Samsung KNOX デバイスの構成項目を作成する | System Center Configuration Manager"
description: "System Center Configuration Manager の Android と Samsung KNOX の構成項目を使用してデバイスの設定を管理します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c28d5ef5-3ea7-4ba2-af01-6600aa805d48
caps.latest.revision: 17
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 8d676d31d519b7b6099c878d94b4c81f1c972887


---
# <a name="create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-system-center-configuration-manager-client"></a>System Center Configuration Manager クライアントを使用せずに管理されている Android デバイスと Samsung KNOX デバイスの構成項目を作成する

*適用対象: System Center Configuration Manager (Current Branch)*



 System Center Configuration Manager の **Android および Samsung KNOX** 構成項目を使用して、Microsoft Intune に登録されているか、Configuration Manager によって内部管理されている Android デバイスおよび Samsung KNOX デバイスの設定を管理します。  

## <a name="create-an-android-and-samsung-knox-configuration-item"></a>Android および Samsung KNOX 構成項目を作成する  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[コンプライアンス設定]** > **[構成項目]** の順にクリックします。  

3.  [ホーム **** ] タブの [作成 **** ] グループで、[構成項目の作成 ****] をクリックします。  

4.  **構成項目の作成ウィザード** の **[全般]**ページで、構成項目の名前と、必要に応じて説明を入力します。  

5.  **[作成する構成項目の種類の指定]**で、 **[Android および Samsung KNOX]**を選択します。  

6.  Configuration Manager コンソールで構成項目を検索およびフィルター処理するのに役立つカテゴリを作成して割り当てる場合は、[**カテゴリ**] をクリックします。  

7.  [**サポートされているプラットフォーム**] ページで、構成項目を評価する特定の Android または Samsung KNOX プラットフォームを選択します。  

8.  [**デバイスの設定**] ページで、構成する設定グループを選択します。 このトピックの「 [Android と Samsung KNOX の構成項目設定のリファレンス](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference) 」で詳細情報を確認し、 **[次へ]**をクリックします。  

    > [!TIP]  
    >  必要な設定が一覧にない場合は、 **[既定の設定グループに含まれない追加の設定を構成する]**チェック ボックスをオンにします。  

9. 各設定ページで、必要な設定と、その設定がデバイスに対応していないときにその設定を修正するかどうかを構成します (これがサポートされている場合)。  

10. 設定グループごとに、構成項目が非対応であることが検出されたときに (Configuration Manager レポートで) 報告される重要度を構成することもできます。  

    -   **なし**: このコンプライアンス規則を満たしていないデバイスは、非対応重要度を何も報告しません。  

    -   **情報**: このコンプライアンス規則を満たしていないデバイスは、**情報**というレベルで非対応重要度を報告します。  

    -   **警告**: このコンプライアンス規則を満たしていないデバイスは、**警告**というレベルで非対応重要度を報告します。  

    -   **重大**: このコンプライアンス規則を満たしていないデバイスは、**重大**というレベルで非対応重要度を報告します。  

    -   **重大 (イベント)**: このコンプライアンス規則を満たしていないデバイスは、**重大**というレベルで非対応重要度を報告します。   

11. [**プラットフォームの適用性**] ページで、前に選択したサポート対象プラットフォームと互換性がないすべての設定を確認します。 前に戻ってこれらの設定を削除するか、操作を続行できます。  

    > [!TIP]  
    >  サポートされていない設定のコンプライアンスは評価されません。  

12. ウィザードを完了します。  

 新しい構成項目は、 **[資産とコンプライアンス]** ワークスペースの **[構成項目]** ノードに表示されます。  

##  <a name="android-and-samsung-knox-configuration-item-settings-reference"></a>Android と Samsung KNOX の構成項目設定のリファレンス  

### <a name="password"></a>パスワード  
 これらの設定は Android と Samsung KNOX の両方のデバイスに適用されます。  

|設定|説明|  
|-------------|-------------|  
|**モバイル デバイスのパスワードの設定が必要**|サポート対象デバイスのパスワードが必要です。|  
|**パスワードの最小文字数**|パスワードの最小の長さ。|  
|**パスワードの有効期限 (日数)**|パスワードの変更が必要になるまでの日数。|  
|**記憶するパスワードの数**|以前に使用したパスワードを再利用できないようにします。|  
|**デバイスをワイプするまでのログオン失敗回数**|ログインの試みがこの回数だけ失敗した場合は、デバイスがワイプされます。|  
|**デバイスをロックするまでのアイドル時間**|使用されていない場合に、デバイスがロックされるまでの時間を選びます。|
|**パスワードの品質**|必要なレベルのパスワードの複雑さと、生体認証デバイスを使用できるかどうかを選択します。|  
|**Smart Lock と他の信頼のエージェントを許可する**|互換性のある Android デバイスで Smart Lock 機能が制御できるようになります。 信頼エージェントとも呼ばれるこの電話機能では、デバイスが特定の Bluetooth デバイスに接続したときや、NFC タグの近くにある場合など、信頼できる場所にある場合、デバイスのロック画面のパスワードを無効化またはバイパスすることができます。 この設定を使用して、エンド ユーザーが Smart Lock を構成することを禁止できます。|

###  <a name="device"></a>デバイス  
 これらの設定は、Samsung KNOX デバイスのみに適用されます。  

|設定の名前|説明|  
|------------------|-------------|  
|**出荷時の設定に戻す**|ユーザーがデバイスを出荷時の設定に戻せるようにします。|  
|**アプリケーション間でのクリップボードの共有**|クリップボードを使用してアプリ間でコピーと貼り付けを実行します。|  

### <a name="cloud"></a>クラウド  
 これらの設定は、Samsung KNOX デバイスのみに適用されます。  

|設定|説明|  
|-------------|-------------|  
|**Google へのバックアップ**|Google へのバックアップを使用できるようにします。|  
|**Google アカウントの自動同期**|Google アカウントの設定を自動的に同期できるようにします。|  

### <a name="security"></a>セキュリティ  

|設定|説明|  
|-------------|-------------|  
|**カメラ**|デバイスのカメラを使用できるようにします。<br /><br /> Android と Samsung KNOX のデバイスに適用されます。|  
|**YouTube**|デバイスで YouTube アプリを使用できるようにします。<br /><br /> Samsung KNOX デバイスのみに適用されます。|  
|**電源オフ**|デバイスの電源をオフにできるようにします。<br /><br /> Samsung KNOX デバイスのみに適用されます。|  

### <a name="encryption"></a>暗号化  
 これらの設定は Android と Samsung KNOX の両方のデバイスに適用されます。  

|設定|説明|  
|-------------|-------------|  
|**デバイスのファイルの暗号化**|モバイル デバイス上のファイルを必ず暗号化するようにします。|  

### <a name="kiosk-mode-samsung-knox-only"></a>キオスク モード (Samsung KNOX のみ)  
 キオスク モードでは、特定の機能のみ実行できるようにデバイスをロックできます。 たとえば、指定した 1 つの管理対象アプリの実行のみをデバイスに許可することや、デバイスのボリューム ボタンを無効にすることができます。 これらの設定は、デバイスのデモ モデルや、POS デバイスなどの 1 つの機能の実行専用のデバイス向けに使用できます。  

#### <a name="to-configure-kiosk-mode-for-a-samsung-knox-device"></a>Samsung KNOX デバイスのキオスク モードを構成する方法  

**[構成項目の作成ウィザード]** の **[Samsung KNOX デバイス用にキオスク モードの設定を構成します]** ページで、次の情報を指定します。  

- **アプリの選択**: [**参照**] をクリックして、デバイスがキオスク モードのときに実行が許可される Configuration Manager Android アプリケーション (拡張子 **.apk**) を選びます。 他のアプリはデバイスでの実行が許可されません。
- **ボリューム ボタン** - デバイスのボリューム ボタンの使用を有効または無効にします。
- **画面のスリープと復帰のボタン**: デバイスの画面のスリープと復帰のボタンを有効または無効にします。  

###  <a name="compliant-and-noncompliant-apps-android"></a>準拠アプリと非準拠アプリ (Android)  
 社内の準拠している (または準拠していない) Android アプリの一覧を指定できます。 これにより、レポートを使用して、非準拠アプリがインストールされているデバイス、および関連付けられているユーザーを表示できるようになります。  

 同一の構成アイテム内で準拠アプリと非準拠アプリの両方を指定することはできません。  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>準拠アプリまたは非準拠アプリの一覧を指定するには  

1.  **[準拠アプリと非準拠アプリ (Android)]** ページで、次の情報を指定します。  

    |設定|説明|  
    |-------------|----------------------|  
    |**非準拠アプリの一覧**|非準拠として報告されるアプリがユーザーによってインストールされている場合、その一覧を指定するには、このオプションを選択します。|  
    |**準拠アプリの一覧**|ユーザーがインストールできるアプリの一覧を指定するには、このオプションを選択します。 インストールされているその他のすべてのアプリは、非準拠として報告されます。|  
    |**[追加]**|選択した一覧にアプリを追加します。 選択した名前と、必要に応じて、アプリの発行者、App Store のアプリへの URL を指定します。<br /><br /> URL を指定するには、 [Google Play のアプリ セクション](https://play.google.com/store/apps)で、使用するアプリを検索します。<br /><br /> アプリのページを開き、URL をクリップボードにコピーします。 準拠アプリおよび非準拠アプリの一覧で URL として使用できるようになります。<br /><br /> **例:** Google Play で **Microsoft Office Mobile**を検索します。 **https://play.google.com/store/apps/details?id=com.microsoft.office.officehub**という URL を使用します。|  
    |**編集**|選択したアプリの名前、発行者、および URL を編集できます。|  
    |**削除**|選択したアプリを一覧から削除します。|  
    |**[インポート]**|コンマ区切り値ファイルで指定したアプリの一覧をインポートします。 ファイルの形式、アプリケーション名、発行者、アプリの URL を使用します。|  

2.  終了したら、 **[次へ]**をクリックします。  

 次のレポートのいずれかを使用して、準拠アプリと非準拠アプリを監視できます。  

-   **指定されたユーザーの準拠しないアプリケーションとデバイスの一覧** : 指定したポリシーに準拠していないアプリをインストールしたユーザーとデバイスについての情報が表示されます。  

-   **非準拠アプリを持つユーザーの概要** - アプリがインストールされ、指定されたポリシーに準拠していないユーザーに関する情報を表示します。  

 レポートの使用方法の詳細については、「[System Center Configuration Manager のレポート](../../core/servers/manage/reporting.md)」を参照してください。  



<!--HONumber=Nov16_HO1-->

