---
title: Intune で Lookout MTD を有効にする
description: Microsoft Intune ポータルで Lookout Mobile Threat Defense (MTD) を有効にします。
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 179aae5fdbd8d6c09a34dca6dd01437d5f61f7b8
ms.sourcegitcommit: 0a4556820fabe004d45a82b0ee1176f6891ac9f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2018
ms.locfileid: "37949596"
---
# <a name="enable-lookout-mtd-connection-in-the-intune-admin-console"></a>Intune 管理コンソールで Lookout MTD 接続を有効にする

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、Microsoft Intune で Lookout Mobile Threat Defense (MTD) を有効にする方法について説明します。 この手順を実行する前に、Lookout コンソールで Intune コネクタを構成しておきます。 まだ構成していない場合は、「[Lookout デバイス脅威保護のサブスクリプションを設定する](set-up-your-subscription-with-lookout.md)」で説明されている手順を実行します。



## <a name="enable-the-lookout-mtd-connector"></a>Lookout MTD コネクタを有効にする

1. [Azure Portal](https://portal.azure.com) に移動し、Intune 資格情報でサインインします。 正常にサインインできたら、**Azure ダッシュボード**が表示されます。  

2. **Azure ダッシュボード**の左のメニューから **[すべてのサービス]** を選択し、テキスト ボックス フィルターに「**Intune**」と入力します。  

3. **[Intune]** を選択します。**Intune ダッシュボード**が開きます。  

4. **Intune ダッシュボード**で、**[デバイスのポリシー準拠]** を選択し、**[設定]** セクションで **[Mobile Threat Defense]** を選択します。  

5. **[Mobile Threat Defense]** ウィンドウで **[追加]** を選択します。  

6. ドロップダウン リストから **[Mobile Threat Defense connector to setup]\(セットアップする Mobile Threat Defense コネクタ\)** として **[Lookout]** を選択します。  

7. 組織の要件に合わせて切り替えオプションを有効にします。  



## <a name="mtd-toggle-options"></a>MTD 切り替えオプション

組織の要件に基づき、有効にする MTD 切り替えオプションを決定できます。 詳細を次に示します。

- **[Connect Android 4.1+ devices to Lookout for Work MTD]\(Android 4.1+ デバイスを Lookout for Work MTD に接続する\)**: このオプションを有効にすると、Android 4.1+ デバイスでセキュリティ リスクを Intune に報告できます。  
    - **[Mark as noncompliant if no data is received]\(データが受け取られない場合、非準拠としてマークする\)**: このプラットフォームに関するデータを Intune が Lookout から受け取らない場合、デバイスは非準拠として見なされます。  

- **[Connect iOS 8.0+ devices to Lookout for Work MTD]\(iOS 8.0+ デバイスを Lookout for Work MTD に接続する\)**: このオプションを有効にすると、iOS 8.0+ デバイスでセキュリティ リスクを Intune に報告できます。
    - **[Mark as noncompliant if no data is received]\(データが受け取られない場合、非準拠としてマークする\)**: このプラットフォームに関するデータを Intune が Lookout から受け取らない場合、デバイスは非準拠として見なされます。  

> [!TIP]  
> [Mobile Threat Defense] ウィンドウでは、Intune と Lookout の**接続状態**と両者が**前回同期された時刻**を確認できます。



## <a name="next-steps"></a>次のステップ
これで、Lookout と Intune の統合の設定は完了です。 このソリューションを実装するための次の手順には、[Lookout for Work アプリ](configure-and-deploy-lookout-for-work-apps.md)の展開や、[コンプライアンス](enable-device-threat-protection-rule-compliance-policy.md) ポリシーの設定などが含まれます。

>[!IMPORTANT]
> コンプライアンス ポリシー ルールを作成し、条件付きアクセスを構成するには、事前に Lookout for Work アプリを構成する*必要があります*。 このアクションにより、エンド ユーザーがアプリをインストールして、電子メールやその他の会社のリソースにアクセスする場合に使用できるようになります。

[Lookout for Work アプリを構成する](configure-and-deploy-lookout-for-work-apps.md)
