# 第三章 EM ExpressおよびSQLベースの管理ツールの使用

## 3.1 EM Expressの起動

**EM Expressとは　★★★**

+ `EM Express` (Enterprise Manager Database Express)は、Oracleインスタンスやデータベースを管理するための軽量な**Webベースの管理ツール**である。

+ `EM Express`は、Oracleソフトウェアをインストール時に、**OUIによって自動的にインストール**されます。

+ `EM Express`を使用すると、データベースの**パフォーマンス監視**や、基本的な**データベース管理**作業を実行できます。

+ `EM Express`はデータベースがオープンしている時**のみ**使用でき、基本的なデータベース管理タスクの実行や、データベースのパフォーマンス監視およびステータス情報の表示を実行できる。

+ 「**EM Expressはデータベースの起動・停止を伴わない、限定された管理作業を行うツール**」といえます。

**EM Expressの構成　★★★**

+ 通常は、`EM Express`の追加の**構成作業は必要ありません**が、何からの理由でHTTPSポートが構成されていない場合や、HTTPSポートを変更したい場合は、**手動で構成必要**です。

+ `EM Express`の手動で構成手順

1. リスナープロセスを起動します。

2. 初期化パラメータDISPATCHERSにPROTOCOL=TCP属性を追加し、TCPディスパッチを有効にします。

```sql
dispatchers="(PROTOCOL=TCP)(SERVICE=<sid>XDB)"
```  

3. DBMS_XDB_CONFIG.sethTTPSPortプロシージャを実行して、ポートを指定する。(このプロシージャを実行するには、SYSDBAとして接続する必要がある。)

```sql
exec DBMS_XDB_CONFIG.setHTTPSPort(5000):
```

## 3.2 EM Expressの使用方法

**EM Expressへのアクセス　★★★**

+ `EM Express`のURLは「`https://ホスト名:ポート番号/em`」です。

+ `EM Express`のポート番号は次のSQLで検索できる。

```sql
SELECT dbms_xdb_config.gethttpsport FROM DUAL;
```

**EM Expressへのアクセス権限の付与　★★★**

+ `EM Express`を使用するには、ユーザーに`EM_EXPRESS_BASICロール` か `EM_EXPRESS_ALLロール`のいずれかが付与されている必要がある。

+ **EM_EXPRESS_BASICロール**：読み取り専用モードでページを表示できる。

+ **EM_EXPRESS_ALLロール**：すべての機能を使用できる。

## 3.3 SQL*PlusおよびSQL Developerを使用したデータベースへのアクセス

**SQL*Plusの起動方法　★★**

+ `SQL*Plus`は、データベースを管理するための、**コマンドベースのツール**である。

+ `SQL*Plus`を起動するには、「**sqlplus/nolog**」 を実行する。

+ `SQL*Plus`で データベースに接続するには「**connect ユーザー名/パスワード**」を実行する。

**SQL*Plusの使用方法　★★★**

+ `SQL*Plus`の使用方法は以下の３つの方法がある。

  + **対話的に**SQLコマンドを入力し、実行する。

  + **SQLスクリプトファイル**を作成し、バッチモードで実行する。

  + `SQL*Plus`を終了せずに**OSコマンド**を実行する。

**SQL Developerの起動方法　★★**

+ `SQL Developer`はデータベースにアクセスするための**グラフィカルツール**である。

+ `SQL Developer`を起動するには`SQL Developer`ディレクトリ($ORACLE_HOME/sqldeveloper)にナビゲートして**sqldeveloper.sh**を実行する。

**SQL Developerの使用方法　★★★**

+ `SQL Developer`の使用パターンには以下の２つがある。

 + **通常モード**でスキーマ・オブジェクトを参照、作成、編集および削除するような、スキーマ・オブジェクトに対する作業を実行する。
 
 + **DBAナビゲータ**を使用してDBA接続をすることで、Oracleデータベースの起動、停止を含むデータベース管理タスクを実行する。

## リンク

- [ディレクトリ](./../directory.md)

- 前章：[第二章 Oracleデータベースのインストールおよびデータベースの作成](Chapter02.md)

- 次章：[第四章 Oracleネットワーク環境の構成](Chapter04.md)
