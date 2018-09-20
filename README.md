# デプロイ方法

## 設定

### サーバ側設定

```$TOMCAT_HOME/conf/tomcat-users.xml
<?xml version='1.0' encoding='utf-8'?>
<tomcat-users>
  <role rolename="manager-script"/>
  <user username="user" password="password" roles="manager-script"/>
</tomcat-users>
```

### クライアント側設定

```~/.m2/settings.xml
<?xml version='1.0' encoding='utf-8'?>
<settings
  xmlns="http://maven.apache.org/SETTINGS/1.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
  <servers>
    <server>
      <id>target-tomcat</id>
      <username>user</username>
      <password>password</password>
    </server>
  </servers>
</settings>

```

## 実行

クライアント側で実行

```
mvn clean tomcat7:deploy -Dmaven.tomcat.url=http://localhost:8080/manager/text -Dmaven.tomcat.update=true
```
