---
title: コレクションのベスト プラクティス
titleSuffix: Configuration Manager
description: System Center Configuration Manager のコレクションのベスト プラクティスを示します。
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ab92f27e37113db88d1cadf5ff49870162206563
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32343434"
---
# <a name="best-practices-for-collections-in-system-center-configuration-manager"></a>System Center Configuration Manager のコレクションのベスト プラクティス

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のコレクションに関する以下のベスト プラクティスを使用してください。  

## <a name="do-not-use-incremental-updates-for-a-large-number-of-collections"></a>多数のコレクションに対して、増分更新を使用しないでください。  
 **[このコレクションで増分更新を使用する]** オプションを多数のコレクションに対して有効にすると、この構成が評価の遅延を引き起こす可能性があります。 しきい値は、階層内では約 200 コレクションです。 正確な数は、次の要因によります。  

-   コレクションの総数  

-   階層内で、リソースが新しく追加または変更される頻度  

-   階層内のクライアント数  

-   階層内のコレクション メンバーシップ規則の複雑さ  

## <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>重要なソフトウェア更新プログラムを展開するのに十分なメンテナンス期間を確保する  
 デバイス コレクションのメンテナンス期間を構成して、Configuration Manager がソフトウェアをそれらのデバイスにインストールできる時間を制限することができます。 メンテナンス期間の構成で十分な時間が確保されていない場合、クライアントは重要なソフトウェア更新プログラムをインストールできない可能性があり、その結果、ソフトウェア更新プログラムによって緩和される攻撃に対して脆弱なままになります。  
