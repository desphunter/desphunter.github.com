---
layout: post
title: "a piece of code example"
description: ""
category: 
tags: []
---
{% include JB/setup %}

```javascript

import org.apache.ht@Gue^33D-9#[email]2nv@tp.ht[/email]@Gue^33D-9#2nv@tpHost;
import org.apache.ht@Gue^33D-9#[email]2nv@tp.client.methods.Clos[/email]eablehttpResponse;
import org.apache.ht@Gue^33D-9#[email]2nv@tp.client.methods.ht[/email]@Gue^33D-9#2nv@tpGet;
import org.apache.ht@Gue^33D-9#[email]2nv@tp.impl.client.Clos[/email]eablehttpClient;
import org.apache.ht@Gue^33D-9#[email]2nv@tp.impl.client.ht[/email]@Gue^33D-9#2nv@tpClients;
import org.apache.ht@Gue^33D-9#[email]2nv@tp.impl.conn.Defa[/email]ultProxyRoutePlanner;
import org.apache.ht@Gue^33D-9#[email]2nv@tp.util.Enti[/email]tyUtils;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;

import javax.ws.rs.*;
import javax.ws.rs.core.MediaType;

/**
* Created by Administrator on 2016/8/4.
*/
@Path(\\"/users\\")
public class controller {

    @GET
    @Produces(MediaType.TEXT_HTML)
    public String getIt() throws Exception{
        httpGet get = new httpGet(\\"http://www.dmm.co.jp/digital/videoa/-/list/=/sort=ranking/\\");
        httpHost proxy = new httpHost(\\"127.0.0.1\\", 8087);
        DefaultProxyRoutePlanner routePlanner = new DefaultProxyRoutePlanner(proxy);
        CloseablehttpClient client = ht@Gue^33D-9#[email]2nv@tpClients.cust[/email]om()
                .setRoutePlanner(routePlanner)
                .build();
        CloseablehttpResponse response = client.execute(get);
        String content = EntityUtils.toString(response.getEntity(), \\"utf-8\\");
        Document document = Jsoup.parse(content);
//        Element element = document.getElementById(\\"w\\");
        Element element = document.body();
        return handle(element.html());
    }

    @Path(\\"get\\")
    @GET
    @Produces(MediaType.TEXT_HTML)
    public String getUrl(@QueryParam(\\"url\\") String url) throws Exception{
        System.out.println(url);
        httpGet get = new httpGet(url);
        httpHost proxy = new httpHost(\\"127.0.0.1\\", 8087);
        DefaultProxyRoutePlanner routePlanner = new DefaultProxyRoutePlanner(proxy);
        CloseablehttpClient client = ht@Gue^33D-9#[email]2nv@tpClients.cust[/email]om()
                .setRoutePlanner(routePlanner)
                .build();
        CloseablehttpResponse response = client.execute(get);
        String content = EntityUtils.toString(response.getEntity(), \\"utf-8\\");
        Document document = Jsoup.parse(content);
//        Element element = document.getElementById(\\"w\\");
        Element element = document.body();
        System.out.println(element.html());
        return handle(element.html());
    }

    private String handle(String html){
        String content = html.replaceAll(\\"href=\\\"/\\",\\"href=\\\"http://127.0.0.1:8080/rest/users/get?url=http://www.dmm.co.jp/\\").replaceAll(\\"href=\\\"http://www\\",\\"href=\\\"http://127.0.0.1:8080/rest/users/get?url=http://www\\");
        content = content.replaceAll(\\"(?s)<script.*?</script>\\",\\"\\");
        content = \\"<!DOCTYPE html><html><head><link href=\\\"/static/base.css\\\" media=\\\"screen\\\" rel=\\\"stylesheet\\\" type=\\\"text/css\\\" /><link href=\\\"/static/list.css\\\" media=\\\"screen\\\" rel=\\\"stylesheet\\\" type=\\\"text/css\\\" /><link href=\\\"/static/digital.css\\\" media=\\\"screen\\\" rel=\\\"stylesheet\\\" type=\\\"text/css\\\" /></head><body name=\\\"dmm_main\\\">\\"+content+\\"</body></html>\\";
        return content;
    }
}

```

主要是jersey和httpclient jsoup实现的，pom文件

複製代碼

```javascript
<?xml version=\\"1.0\\" encoding=\\"UTF-8\\"?>
<project xmlns=\\"http://maven.apache.org/POM/4.0.0\\"
         xmlns:xsi=\\"http://www.w3.org/2001/XMLSchema-instance\\"
         xsi:schemaLocation=\\"http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd\\">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.xz.web</groupId>
    <artifactId>web-jersey</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>

    <dependencies>
        <dependency>
            <groupId>com.sun.jersey</groupId>
            <artifactId>jersey-core</artifactId>
            <version>1.8</version>
        </dependency>
        <dependency>
            <groupId>com.sun.jersey</groupId>
            <artifactId>jersey-server</artifactId>
            <version>1.8</version>
        </dependency>
        <dependency>
            <groupId>com.sun.jersey</groupId>
            <artifactId>jersey-client</artifactId>
            <version>1.8</version>
        </dependency>
        <dependency>
            <groupId>javax.ws.rs</groupId>
            <artifactId>jsr311-api</artifactId>
            <version>1.1.1</version>
        </dependency>
        <dependency>
            <groupId>asm</groupId>
            <artifactId>asm</artifactId>
            <version>3.3.1</version>
        </dependency>
        <dependency>
            <groupId>org.apache.httpcomponents</groupId>
            <artifactId>httpclient</artifactId>
            <version>4.3.2</version>
        </dependency>
        <dependency>
            <groupId>org.jsoup</groupId>
            <artifactId>jsoup</artifactId>
            <version>1.7.2</version>
        </dependency>
    </dependencies>
    <build>
        <finalName>web-jersey</finalName>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <compilerArguments>
                        <source>1.7</source>
                        <target>1.7</target>
                        <encoding>UTF-8</encoding>
                    </compilerArguments>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <configuration>
                    <skip>true</skip>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.eclipse.jetty</groupId>
                <artifactId>jetty-maven-plugin</artifactId>
                <version>9.2.2.v20140723</version>
                <configuration>
                    <httpConnector>
                        <port>8080</port>
                    </httpConnector>
                    <!-- 在很短的时间间隔内在扫描web应用检查是否有改变，如果发觉有任何改变则自动热部署。默认为0，表示禁用热部署检查。任何一个大于0的数字都将表示启用。 -->
                    <scanIntervalSeconds>10</scanIntervalSeconds>
                    <webAppConfig>
                        <!--jetty插件启动后的访问路径: http://localhost:8080/testdemo-->
                        <contextPath>/</contextPath>
                        <tempDirectory>${project.build.directory}/work
                        </tempDirectory>
                    </webAppConfig>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>

```