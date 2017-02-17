# 第三章 EM ExpressおよびSQLベースの管理ツールの使用

## 3.1 EM Expressの起動

**EM Expressとは　★★★**

+ **EM Express**(Enterprise Manager Database Express)は、Oracleインスタンスやデータベースを管理するための軽量な**Webベースの管理ツール**である。

+ EM Expressは、Oracleソフトウェアをインストール時に、**OUIによって自動的にインストール**されます。

+ EM Expressを使用すると、データベースの**パフォーマンス監視**や、基本的な**データベース管理**作業を実行できます。

+ EM Expressはデータベースがオープンしている時**のみ**使用でき、基本的なデータベース管理タスクの実行や、データベースのパフォーマンス監視およびステータス情報の表示を実行できる。

+ 「**EM Expressはデータベースの起動・停止を伴わない、限定された管理作業を行うツール**」といえます。

**EM Expressの構成　★★★**

+ 通常は、EM Expressの追加の**構成作業は必要ありません**が、何からの理由でHTTPSポートが構成されていない場合や、HTTPSポートを変更したい場合は、**手動で構成必要**です。

+ EM Expressの手動で構成手順

    1. リスナープロセスを起動します

    2. 初期化パラメータDISPATCHERSにPROTOCOL=TCP属性を追加し、TCPディスパッチを有効にします。

    ```
    dispatchers="(PROTOCOL=TCP)(SERVICE=<sid>XDB)"
    ```  

    3. DBMS_XDB_CONFIG.sethTTPSPortプロシージャを実行して、ポートを指定する。(このプロシージャを実行するには、SYSDBAとして接続する必要がある。)

    ```sql
    exe DBMS_XDB_CONFIG.setHTTPSPort(5000):
    ```

## 3.2 EM Expressの使用方法

**EM Expressへのアクセス　★★★**

+ EM ExpressのURLは「```https://ホスト名:ポート番号/em```」です。

+ EM Expressのポート番号は次のSQLで検索できる。

    ```sql
    SELECT dbms_xdb_config.gethttpsport FROM DUAL;
    ```

**EM Expressへのアクセス権限の付与　★★★**

+ EM Expressを使用するには、ユーザーに**EM_EXPRESS_BASICロール**か**EM_EXPRESS_ALLロール**のいずれかが付与されている必要がある。

+ EM_EXPRESS_BASICロール：読み取り専用モードでページを表示できる。

+ EM_EXPRESS_ALLロール：すべての機能を使用できる。

## 3.3 SQL*PlusおよびSQL Developerを使用したデータベースへのアクセス
