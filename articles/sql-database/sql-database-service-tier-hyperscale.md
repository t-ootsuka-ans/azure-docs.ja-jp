---
title: Azure SQL Database Hyperscale の概要 | Microsoft Docs
description: この記事では、Azure SQL Database における仮想コアベースの購入モデルでのハイパースケール サービス レベル、およびそれが General Purpose および Business Critical サービス レベルと異なる点について説明します。
services: sql-database
ms.service: sql-database
ms.subservice: service
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
ms.reviewer: ''
ms.date: 10/01/2019
ms.openlocfilehash: a5512aa1a2538d3336bbcc4f65cad671d52b711a
ms.sourcegitcommit: 50ef5c2798da04cf746181fbfa3253fca366feaa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2020
ms.locfileid: "82610668"
---
# <a name="hyperscale-service-tier"></a>ハイパースケール サービス レベル

Azure SQL Database は、インフラストラクチャに障害が発生した場合でも 99.99% の可用性を確保するために、クラウド環境に合わせて調整された SQL Server データベース エンジン アーキテクチャに基づいています。 Azure SQL Database で使用されているアーキテクチャ モデルは 3 つあります。
- General Purpose/Standard 
-  ハイパースケール
-  Business Critical/Premium

Azure SQL Database の Hyperscale サービス レベルは、仮想コアベースの購入モデルにおける最新のサービス レベルです。 このサービス レベルは、拡張性の高いストレージおよびコンピューティング パフォーマンス レベルであり、Azure のアーキテクチャを利用して、General Purpose および Business Critical サービス レベルの制限を大きく超えて、Azure SQL Database 用のストレージおよびコンピューティング リソースをスケールアウトします。

> 
> [!NOTE]
> 仮想コアベースの購入モデルでの General Purpose サービス レベルと Business Critical サービス レベルの詳細については、[General Purpose](sql-database-service-tier-general-purpose.md) サービス レベルと [Business Critical](sql-database-service-tier-business-critical.md) サービス レベルの記事を参照してください。 仮想コアベースの購入モデルと DTU ベースの購入モデルとの比較については、[Azure SQL Database の購入モデルとリソース](sql-database-service-tiers.md)に関する記事をご覧ください。


## <a name="what-are-the-hyperscale-capabilities"></a>ハイパースケールの機能とは

Azure SQL Database の Hyperscale サービス レベルでは、次の追加機能が提供されます。

- 最大 100 TB のデータベース サイズのサポート
- サイズに関係なく、コンピューティング リソースに対する IO の影響もなく、ほぼ瞬間的に行われるデータベース バックアップ (Azure BLOB Storage に格納されたファイル スナップショットに基づく)  
- 数時間あるいは数日かからずに数分間で行われる迅速なデータベース復元 (ファイル スナップショットに基づく) (データ操作の規模ではない)
- データ ボリュームに関係なく、高いログ スループットと速いトランザクション コミット時間による、全体的に高いパフォーマンス
- 迅速なスケールアウト - 読み取りワークロードのオフロード用と、ホット スタンバイ用に、1 つ以上の読み取り専用ノードをプロビジョニングできます。
- 迅速なスケールアップ - 大きいワークロードに対応する必要があるときはコンピューティング リソースを一定の時間でスケールアップでき、必要がなくなったらコンピューティング リソースをスケールダウンして戻すことができます。

Hyperscale サービス レベルでは、クラウド データベースにおいて従来見られた実質的な制限の多くが取り除かれます。 他のほとんどのデータベースは 1 つのノードで使用可能なリソースによって制限されますが、Hyperscale サービス レベルのデータベースにはそのような制限はありません。 ストレージ アーキテクチャの柔軟性が高く、必要に応じてストレージが拡張されます。 実際、Hyperscale データベースの作成時には最大サイズは定義されません。 Hyperscale データベースは必要に応じて拡大し、使用している容量に対してのみ課金されます。 読み取り集中型ワークロードでは、Hyperscale サービス レベルは、読み取りワークロードのオフロード用に必要に応じて追加の読み取りレプリカをプロビジョニングし、迅速なスケールアウトを提供します。

さらに、データベース バックアップの作成に必要な時間や、スケールアップまたはスケールダウンに必要な時間は、データベース内のデータの量に関連しなくなっています。 Hyperscale データベースはほぼ瞬時にバックアップできます。 また、数十テラバイトのデータベースを、数分でスケールアップまたはスケールダウンできます。 この機能により、初期構成の選択によって縛り付けられることを心配する必要はなくなります。

ハイパースケール サービス レベルのコンピューティング サイズについて詳しくは、「[サービス レベルの特性](sql-database-service-tiers-vcore.md#service-tiers)」をご覧ください。

## <a name="who-should-consider-the-hyperscale-service-tier"></a>Hyperscale サービス レベルを検討する必要があるユーザー

Hyperscale サービス レベルは、個別にスケーラブルなコンピューティング リソースとストレージ リソースを使用して優れた柔軟性と高パフォーマンスを提供するため、ほとんどのビジネス ワークロードを対象としています。 ストレージを最大 100 TB まで自動スケールする機能により、次のようなお客様にとって最適な選択肢となります。

- オンプレミスに大規模なデータベースがあり、クラウドに移行してアプリケーションを最新化する必要がある場合
- 既にクラウドを利用しているが、他のサービス レベルのデータベースの最大サイズ制限によって制限されている (1 ～ 4 TB)
- 使用するデータベースは小さいが、垂直方向と水平方向の高速なコンピューティング スケーリング、高パフォーマンス、インスタント バックアップ、データベースの高速復元を必要としている。

Hyperscale サービスレベルは、純粋な OLTP から純粋な分析まで、さまざまな SQL Server ワークロードをサポートしていますが、主に OLTP とハイブリッド トランザクションおよび分析処理 (HTAP) のワークロード向けに最適化されています。

> [!IMPORTANT]
> エラスティック プールでは、Hyperscale サービス レベルはサポートされていません。

## <a name="hyperscale-pricing-model"></a>ハイパースケールの価格モデル

ハイパースケール サービス レベルは[仮想コア モデル](sql-database-service-tiers-vcore.md)のみで提供されています。 新しいアーキテクチャに合わせて、価格モデルは General Purpose または Business Critical サービス モデルとは少し異なります。

- **コンピューティング**:

  ハイパースケール コンピューティング ユニットの料金はレプリカ単位です。 [Azure ハイブリッド特典](https://azure.microsoft.com/pricing/hybrid-benefit/)の価格が読み取りスケール レプリカに自動的に適用されます。 既定では、Hyperscale データベースごとにプライマリ レプリカと 1 つの読み取り専用レプリカを作成します。  ユーザーは、プライマリを含むレプリカの総数を、1 から 5 までの間で調整できます。

- **ストレージ**:

  ハイパースケールのデータベースを構成するときに、最大データ サイズを指定する必要はありません。 ハイパースケール レベルでは、実際の割り当てに基づいてデータベースのストレージに対して課金されます。 ストレージは、40 GB から 100 TB までの間 (10 GB 単位の増分) で自動的に割り当てられます。 必要に応じて、複数のデータ ファイルを同時に拡大することができます。 ハイパースケール データベースは、10 GB の開始サイズで作成され、10分ごとに 10 GB ずつ拡大し、最終的には 40 GB のサイズに達します。

ハイパースケールの価格について詳しくは、「[Azure SQL Database の価格](https://azure.microsoft.com/pricing/details/sql-database/single/)」をご覧ください。

## <a name="distributed-functions-architecture"></a>分散機能アーキテクチャ

1 つの場所/プロセスにすべてのデータ管理機能を集中させる従来のデータベース エンジンとは異なり (今日の運用環境で分散データベースと呼ばれているものでも、モノリシックなデータ エンジンの複数のコピーを使用しています)、Hyperscale データベースでは、さまざまなデータ エンジンのセマンティクスが分岐しているクエリ処理エンジンと、データの長期的なストレージと持続性を提供するコンポーネントが分かれています。 これにより、ストレージ容量をスムーズに必要な限りスケールアウトできます (初期ターゲットは 100 TB)。 読み取り専用レプリカは同じストレージ コンポーネントを共有しているので、新しい読み取り可能レプリカを起動するためにデータのコピーは必要ありません。 

次の図では、Hyperscale データベースでのノードのさまざまな種類を示します。

![アーキテクチャ](./media/sql-database-hyperscale/hyperscale-architecture.png)

Hyperscale データベースには、次の種類のコンポーネントが含まれます。

### <a name="compute"></a>Compute

コンピューティング ノードにはリレーショナル エンジンが存在するので、すべての言語要素、クエリ処理などがここで発生します。 Hyperscale データベースとユーザーのすべてのやり取りは、これらのコンピューティング ノードを通して行われます。 データのページをフェッチするために必要なネットワーク ラウンドトリップの数を最小限に抑えるため、コンピューティング ノードは SSD ベースのキャッシュ (前の図の RBPEX - 弾性バッファー プール拡張機能) を備えています。 プライマリ コンピューティング ノードが 1 つあり、すべての読み書きワークロードとトランザクションがそこで処理されます。 1 つ以上のセカンダリ コンピューティング ノードがあり、フェールオーバーのためのホット スタンバイ ノードとして、また (この機能が必要な場合は) 読み取りワークロードをオフロードするための読み取り専用コンピューティング ノードとして機能します。

### <a name="page-server"></a>ページ サーバー

ページ サーバーは、スケールアウトされたストレージ エンジンを表すシステムです。  各ページ サーバーは、データベース内のページのサブセットを受け持ちます。  通常、各ページ サーバーでは 128 GB から 1 TB のデータが制御されます。 複数のページ サーバーでデータが共有されることはありません (冗長性と可用性のために保持されているレプリカの外部)。 ページ サーバーの役割は、必要に応じてコンピューティング ノードにデータベース ページを提供し、トランザクションでデータが更新されたらページを更新することです。 ページ サーバーは、ログ サービスからのログ レコードを再生することによって最新の状態に維持されます。 また、ページ サーバーはパフォーマンスを強化するために SSD ベースのキャッシュも備えています。 信頼性向上のため、データ ページの長期的なストレージが Azure Storage に保持されます。

### <a name="log-service"></a>ログ サービス

ログ サービスは、プライマリ コンピューティング レプリカからログ レコードを受け取り、持続性キャッシュにそれを保持し、他のコンピューティング レプリカ (キャッシュを更新できるように) および関連するページ サーバーにログ レコードを転送して、それらの場所でデータを更新できるようにします。 このようにして、プライマリ コンピューティング レプリカからのすべてのデータ変更が、ログ サービスを介して、すべてのセカンダリ コンピューティング レプリカとページ サーバーに伝達されます。 最後に、ログ レコードは、実質的に無制限のストレージ リポジトリである Azure Storage の長期ストレージにプッシュされます。 このメカニズムにより、頻繁にログを切り捨てる必要がなくなります。 ログ サービスは、ログ レコードへのアクセスを高速化するためのローカル キャッシュも備えています。

### <a name="azure-storage"></a>Azure Storage

Azure Storage には、データベース内のすべてのデータ ファイルが格納されています。 ページ サーバーは Azure Storage 内のデータ ファイルを最新の状態に保ちます。 このストレージは、バックアップ目的だけでなく、Azure リージョン間のレプリケーションにも使用されます。 バックアップはデータ ファイルのストレージ スナップショットを使用して実行されます。 スナップショットを使用した復元操作は、データ サイズに関係なく高速です。 データはデータベースのバックアップ保有期間内の任意の時点に復元できます。

## <a name="backup-and-restore"></a>バックアップと復元

バックアップはファイル スナップショット ベースなので、ほぼ瞬時に実行されます。 ストレージとコンピューティングの分離により、バックアップ/復元操作をストレージ層に移すことができるので、プライマリ コンピューティング レプリカの処理の負荷が軽減されます。 その結果、データベースのバックアップはプライマリ コンピューティング ノードのパフォーマンスに影響を与えません。同様に、復元はファイル スナップショットに戻すことによって行われるため、データ サイズに左右される操作ではありません。 復元は一定時間の操作であり、数テラバイトのデータベースであっても数時間や数日ではなく数分で復元できます。 既存のバックアップを復元することによって新しいデータベースを作成する場合もこの機能を利用します。開発またはテスト目的でのデータベース コピーの作成は、テラバイト サイズのデータベースであっても数分で実行できます。

## <a name="scale-and-performance-advantages"></a>スケールとパフォーマンスの利点

追加の読み取り専用コンピューティング ノードを迅速に起動/停止できるので、Hyperscale アーキテクチャでは、読み取りのスケーリング機能が優れ、より多くの書き込み要求に対応できるようにプライマリ コンピューティング ノードを解放することもできます。 また、Hyperscale アーキテクチャの共有ストレージ アーキテクチャのため、コンピューティング ノードをすばやくスケールアップ/スケールダウンできます。

## <a name="create-a-hyperscale-database"></a>ハイパースケール データベースの作成

ハイパースケール データベースは、[Azure portal](https://portal.azure.com)、[T-SQL](https://docs.microsoft.com/sql/t-sql/statements/create-database-transact-sql?view=azuresqldb-current)、[PowerShell](https://docs.microsoft.com/powershell/module/azurerm.sql/new-azurermsqldatabase)、または [CLI](https://docs.microsoft.com/cli/azure/sql/db#az-sql-db-create) を使用して作成できます。 ハイパースケール データベースは、[仮想コアベースの購入モデル](sql-database-service-tiers-vcore.md)を使用してのみ入手できます。

次の T-SQL コマンドによって、ハイパースケール データベースが作成されます。 `CREATE DATABASE` ステートメントにエディションとサービス目標の両方を指定する必要があります。 有効なサービス目標の一覧については[リソースの制限](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases#hyperscale---provisioned-compute---gen4)に関するページを参照してください。

```sql
-- Create a Hyperscale Database
CREATE DATABASE [HyperscaleDB1] (EDITION = 'Hyperscale', SERVICE_OBJECTIVE = 'HS_Gen5_4');
GO
```
これにより、4 コア搭載の Gen5 ハードウェアに Hyperscale データベースが作成されます。

## <a name="migrate-an-existing-azure-sql-database-to-the-hyperscale-service-tier"></a>既存の Azure SQL Database のハイパースケール サービス レベルへの移行

既存の Azure SQL データベースをハイパースケールに移行するには、[Azure portal](https://portal.azure.com)、[T-SQL](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql?view=azuresqldb-current)、[PowerShell](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqldatabase)、または [CLI](https://docs.microsoft.com/cli/azure/sql/db#az-sql-db-update) を使用します。 現時点で、これは一方向にしか移行できません。 データのエクスポートとインポート以外の方法で、Hyperscale から別のサービス レベルにデータベースを移動することはできません。 概念実証 (POC) のために、運用データベースのコピーを作成して、コピーを Hyperscale に移行することをお勧めします。 既存の Azure SQL データベースの Hyperscale レベルへの移行は、データ サイズに左右される操作です。

次の T-SQL コマンドによってデータベースがハイパースケール サービス レベルに移行されます。 `ALTER DATABASE` ステートメントにエディションとサービス目標の両方を指定する必要があります。

```sql
-- Alter a database to make it a Hyperscale Database
ALTER DATABASE [DB2] MODIFY (EDITION = 'Hyperscale', SERVICE_OBJECTIVE = 'HS_Gen5_4');
GO
```

## <a name="connect-to-a-read-scale-replica-of-a-hyperscale-database"></a>ハイパースケール データベースの読み取りスケールへの接続

ハイパースケール データベースでは、クライアントによって提供された接続文字列の `ApplicationIntent` 引数により、接続が書き込みレプリカと読み取り専用セカンダリ レプリカのどちらにルーティングされるかが指定されます。 `ApplicationIntent` が `READONLY` に設定され、データベースにセカンダリ レプリカがない場合、接続はプライマリ レプリカにルーティングされ、既定で `ReadWrite` の動作になります。

```cmd
-- Connection string with application intent
Server=tcp:<myserver>.database.windows.net;Database=<mydatabase>;ApplicationIntent=ReadOnly;User ID=<myLogin>;Password=<myPassword>;Trusted_Connection=False; Encrypt=True;
```

ハイパースケールのセカンダリ レプリカはすべて同じであり、プライマリ レプリカと同じサービス レベル目標が使用されます。 複数のセカンダリ レプリカが存在する場合、ワークロードは使用可能なすべてのセカンダリ レプリカに分散されます。 各セカンダリ レプリカは個別に更新されるため、レプリカごとに、プライマリ レプリカに対して異なるデータ遅延が生じる可能性があります。

## <a name="database-high-availability-in-hyperscale"></a>ハイパースケールでのデータベースの高可用性

他のすべてのサービス レベルと同様に、Hyperscale は、コンピューティング レプリカの可用性に関係なく、コミットされたトランザクションのデータの持続性を保証します。 プライマリ レプリカが使用できなくなったことによるダウンタイムの程度は、フェールオーバーの種類 (計画されたものと計画外のもの)、および少なくとも 1 つのセカンダリ レプリカの存在に左右されます。 計画フェールオーバー (つまりメンテナンス イベント) では、システムはフェールオーバーを開始する前に新しいプライマリ レプリカを作成するか、既存のセカンダリ レプリカをフェールオーバーのターゲットとして使用します。 計画外のフェールオーバー (つまりプライマリ レプリカでのハードウェア障害) では、システムはセカンダリ レプリカが存在する場合はこれをフェールオーバーのターゲットとして使用し、あるいは使用可能なコンピューティング能力のプールから新しいプライマリ レプリカを作成します。 後者の場合、新しいプライマリ レプリカの作成に必要な追加の手順により、ダウンタイムの期間が長くなります。

Hyperscale の SLA については、「[SLA for Azure SQL Database の SLA](https://azure.microsoft.com/support/legal/sla/sql-database/)」を参照してください。

## <a name="disaster-recovery-for-hyperscale-databases"></a>Hyperscale データベースのディザスター リカバリー

### <a name="restoring-a-hyperscale-database-to-a-different-geography"></a>Hyperscale データベースを別の地理的な場所に復元する
ディザスター リカバリー操作の一環として、またはドリル、再配置などの他の理由で、Azure SQL Database Hyperscale DB を、現在ホストされているリージョン以外のリージョンに復元する必要がある場合、主な方法として、データベースの geo リストアを実行します。  これには、他の AZURE SQL DB を別のリージョンに復元するときとまったく同じ手順が含まれます。
1. ターゲット リージョンにまだ適切なサーバーが存在しない場合は、そこに Azure SQL Database サーバーを作成します。  このサーバーは、元の (ソース) サーバーと同じサブスクリプションが所有する必要があります。
2. 自動バックアップからの Azure SQL データベースの復元に関するページの「[geo リストア](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups#geo-restore)」トピックにある手順に従ってください。

> [!NOTE]
> ソースとターゲットが別々のリージョンにあるため、データベースは、geo リストア以外と同様に、スナップショット ストレージをソース データベースと共有することができません。これは、非常に短時間で完了します。 Hyperscale データベースの geo リストアの場合、ターゲットが geo レプリケーション ストレージのペア リージョンにある場合でも、データのサイズに関連した操作になります。  つまり、geo リストアを実行すると、復元されるデータベースのサイズに比例した時間がかかります。  ペア リージョン内にターゲットがある場合、コピーは 1 つのリージョン内で行われます。これは、複数のリージョンにまたがって行われるコピーよりもはるかに高速になりますが、それでもデータのサイズに左右される操作になります。

## <a name="available-regions"></a><a name=regions></a>対応リージョン

現在、Azure SQL Database Hyperscale レベルは次のリージョンで使用できます。

- オーストラリア東部
- オーストラリア南東部
- ブラジル南部
- カナダ中部
- 米国中部
- 中国東部 2
- 中国北部 2
- 東アジア
- 米国東部
- 米国東部 2
- フランス中部
- 東日本
- 西日本
- 韓国中部
- 韓国南部
- 米国中北部
- 北ヨーロッパ
- 南アフリカ北部
- 米国中南部
- 東南アジア
- 英国南部
- 英国西部
- 西ヨーロッパ
- 米国西部
- 米国西部 2

サポート対象として掲載されていないリージョンに Hyperscale データベースを作成したい場合は、Azure portal 経由でオンボード要求を送信できます。 手順については、「[Azure SQL Database のクォータの増加を要求する](quota-increase-request.md)」を参照してください。 要求を送信するときは、次のガイドラインに従ってください。

- [その他のクォータ要求](quota-increase-request.md#other) SQL データベースのクォータの種類を使用します。
- テキストの詳細に、読み取り可能なレプリカを含むコンピューティング SKU/コア総数を追加します。
- また、推定 TB を指定します。

## <a name="known-limitations"></a>既知の制限事項

以下は、一般提供時点の Hyperscale サービス レベルに対する現在の制限事項です。  これらの制限事項ができるだけなくなるように、積極的に取り組んでいます。

| 問題 | 説明 |
| :---- | :--------- |
| 論理サーバーの [バックアップの管理] ウィンドウには、Hyperscale データベースが表示されません。これらはビューからフィルターで除外されます  | ハイパースケールは別の方法でバックアップを管理しています。そのため、長期的な保有期間と特定の時点のバックアップなどの保有設定が適用されず、無効になります。 したがって、ハイパースケールのデータベースは、[バックアップの管理] ウィンドウに表示されません。 |
| ポイントインタイム リストア | Hyperscale データベースを、Hyperscale 以外のデータベースの保有期間の範囲内に、Hyperscale 以外のデータベースに復元することができます。 Hyperscale 以外のデータベースを Hyperscale データベースに復元することはできません。|
| 1 TB を超えるデータ ファイルがデータベースに 1 つ以上ある場合、移行に失敗します。 | 場合によっては、サイズの大きいファイルを 1 TB 未満に圧縮することで、この問題を回避できることがあります。 移行プロセス中に使用されているデータベースを移行する場合は、1 TB を超えるファイルがないことを確認してください。 データベース ファイルのサイズを確認するには、以下のクエリを使用してください。 `SELECT *, name AS file_name, size * 8. / 1024 / 1024 AS file_size_GB FROM sys.database_files WHERE type_desc = 'ROWS'`;|
| マネージド インスタンス | Azure SQL Database Managed Instance は、現在、Hyperscale データベースではサポートされていません。 |
| エラスティック プール |  エラスティック プールは、現在、SQL Database Hyperscale ではサポートされていません。|
| ハイパースケールへの移行は現在一方向 | データベースがハイパースケールにいったん移行されると、ハイパースケール以外のサービス レベルに直接移行することはできません。 現時点では、ハイパースケールからハイパースケール以外にデータベースを移行する唯一の方法は、BACPAC ファイルまたはその他のデータ移動テクノロジ (一括コピー、Azure Data Factory、Azure Databricks、SSIS など) を使用してエクスポートおよびインポートすることです。Azure portal、PowerShell ([New-AzSqlDatabaseExport](https://docs.microsoft.com/powershell/module/az.sql/new-azsqldatabaseexport) と [New-AzSqlDatabaseImport](https://docs.microsoft.com/powershell/module/az.sql/new-azsqldatabaseimport))、Azure CLI ([az sql db export](https://docs.microsoft.com/cli/azure/sql/db?view=azure-cli-latest#az-sql-db-export) と [az sql db import](https://docs.microsoft.com/cli/azure/sql/db?view=azure-cli-latest#az-sql-db-import))、[REST API](https://docs.microsoft.com/rest/api/sql/databases%20-%20import%20export) から BACPAC のエクスポートとインポートを行うことはサポートされていません。 比較的小さい Hyperscale データベース (最大 200 GB) の BACPAC インポートと BACPAC エクスポートは、SSMS と [SqlPackage](https://docs.microsoft.com/sql/tools/sqlpackage) バージョン 18.4 以降を使用することでサポートされます。 大きなデータベースでは、BACPAC エクスポートと BACPAC インポートに時間がかかり、さまざまな理由で失敗する可能性があります。|
| 永続メモリ内オブジェクトを含むデータベースの移行 | ハイパースケールでは、非永続メモリ内オブジェクト (テーブル型、ネイティブ SP、関数) のみがサポートされます。  データベースがハイパースケール サービス レベルに移行される前に、永続メモリ内テーブルとその他のオブジェクトは削除され、メモリ内ではないオブジェクトとして再作成されます。|
| geo レプリケーション  | Azure SQL Database Hyperscale の geo レプリケーションは、まだ構成できません。 |
| データベース コピー | 現時点では、データベース コピーを使用して、Azure SQL Hyperscale に新しいデータベースを作成することはできません。 |
| TDE/AKV の統合 | Azure Key Vault を使用した透過的データベース暗号化 (通常、Bring Your Own Key (BYOK) と呼ばれます) は、Azure SQL Database Hyperscale ではまだサポートされていませんが、サービス マネージド キーを使用した TDE は完全にサポートされています。 |
|インテリジェント データベース機能 | [Force Plan] オプションを除き、他のすべての自動チューニング オプションは Hyperscale ではまだサポートされていません。オプションは有効になっているように見えますが、推奨事項やアクションは実行されません。 |
|Query Performance Insights | Query Performance Insight は現在、Hyperscale データベースではサポートされていません。 |
| データベースの圧縮 | DBCC SHRINKDATABASE または DBCC SHRINKFILE は、現在、Hyperscale データベースではサポートされていません。 |
| データベースの整合性チェック | DBCC CHECKDB は現在、Hyperscale データベースではサポートされていません。 Azure SQL Database におけるデータ整合性管理の詳細については、「[Azure SQL Database でのデータ整合性](https://azure.microsoft.com/blog/data-integrity-in-azure-sql-database/)」を参照してください。 |

## <a name="next-steps"></a>次のステップ

- ハイパースケールの FAQ については、[ハイパースケールに関するよくあるご質問](sql-database-service-tier-hyperscale-faq.md)をご覧ください。
- サービス レベルについては、[サービス レベル](sql-database-service-tiers.md)に関するページをご覧ください
- サーバーおよびサブスクリプション レベルの制限については、[論理サーバー上のリソース制限の概要](sql-database-resource-limits-logical-server.md)に関するページをご覧ください。
- 単一データベースの購入モデルの制限について詳しくは、「[Azure SQL Database の単一データベースに対する仮想コアベースの購入モデルの制限](sql-database-vcore-resource-limits-single-databases.md)」をご覧ください。
- 機能比較一覧については、[SQL 共通機能](sql-database-features.md)に関する記事をご覧ください。
