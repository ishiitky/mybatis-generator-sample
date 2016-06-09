# MyBatis Generator の使い方

## 事前準備

- DB・テーブルを用意する.本プログラムはPostgreSQLを前提としている.  
  MySQLに変更する場合は JDBC ドライバの設定を修正すること.
- 本プログラムからアクセスできる状態にしておく(アクセス許可設定).

## generatorConfig.xml の編集

JDBCの設定を行う.
PostgreSQL のJDBCドライバは pom で設定済み.
接続先情報はそれぞれのシステムごとに変更すること.
```
<jdbcConnection driverClass="org.postgresql.Driver" 
	connectionURL="jdbc:postgresql://192.168.56.101:5432/sample" userId="postgres" password="postgres" />
```

Entityクラスの出力先を設定する.
targetPackage はそれぞれのシステムごとに変更すること.
```
<javaModelGenerator targetPackage="sample.app.domain.model" targetProject="src/main/java" />
```

SQL Mapperファイル(xmlファイル)の出力先を設定する.
targetPackage はそれぞれのシステムごとに変更すること.
```
<sqlMapGenerator targetPackage="sample.app.domain.repository" targetProject="src/main/resources" />
```

DAOファイルの出力先を設定する.
targetPackage はそれぞれのシステムごとに変更すること.
```
<javaClientGenerator targetPackage="sample.app.domain.repository" targetProject="src/main/java" type="XMLMAPPER" />
```

ターゲットとするテーブルを選択する.
本例ではテーブル名は複数形.ただしEntityクラス,SQL Mapperファイル,DAOクラスは単数形にしたいため、domainObjectName を指定している.
domainObjectName を指定しない場合はテーブル名と同じクラス、XMLファイルが生成される.
```
<table tableName="users" domainObjectName="User" />
<table tableName="password_changelogs" domainObjectName="PasswordChangelog" />
```

## 実行方法

1. Lombok がインストールされていること
2. https://github.com/ishiitky/mybatis-generator-plugins をcloneし、ローカルリポジトリに登録.
3. 本プロジェクトを右クリック > Run As > Run Configurations...
4. Maven Build　を編集
  - Name : mybatis generator
  - Base directory:${workspace_loc:/mybatis-generator-sample}
  - Goals : mybatis-generator:generate
5. Run で実行する.
6. Entityクラス,DAOクラス,SQL Mapperファイル(XMLファイル)が生成されていることを確認する. 

## 参考情報

* http://hit-techblog.blogspot.jp/2014/03/mybatis-2.html