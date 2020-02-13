Eclipse [Californium](https://github.com/eclipse/californium) 라이브러리 demo 하는 과정
===============================================

coap/dtls/ipv4 통신
----------------------------
> demo 전 maven 빌드 도구 필요
### root 계정 접속
<pre><code>$ su
password: ****</code></pre>  

### californium 레포지터리 clone(서버, 클라이언트용 2개 필요)
<pre><code>$ git clone https://github.com/eclipse/californium
$ mv californium calS
$ git clone https://github.com/eclipse/californium
$ mv californium calC</code></pre> 
    

### demo-apps/cf-secure/pom.xml 코드 수정(server ↓)
    <dependencies>
        ...

        <!-- <dependency>
            <groupId>${project.groupId}</groupId>
	        <artifactId>californium-core</artifactId>
        </dependency> -->
        <dependency>
            <groupId>org.eclipse.californium</groupId>
            <artifactId>californium-core</artifactId>
            <version>2.0.0</version>
        </dependency>

        ...
    </dependencies>

![image](https://user-images.githubusercontent.com/47745785/74404108-e4c87b80-4e6c-11ea-9e6e-9b26231ef707.png)

    <!-- repositories 추가 -->
    <repositories>
        <repository>
            <id>repo.eclipse.org</id>
            <name>Californium Repository</name>
            <url>https://repo.eclipse.org/content/repositories/californium/</url>
        </repository>
    </repositories>

![image](https://user-images.githubusercontent.com/47745785/74404326-7afca180-4e6d-11ea-9b83-bc6b8ee6bf9f.png)




### demo-apps/cf-secure/pom.xml server와 똑같이 수정 후 추가로 name, description, properties 수정(client ↓)
    <name>Cf-SecureClient</name>
    <description>Californium (Cf) DTLS example client</description>

    <properties>
        <assembly.mainClass>org.eclipse.californium.examples.SecureClient</assembly.mainClass>
        <skipTests>true</skipTests>
    </properties>

![image](https://user-images.githubusercontent.com/47745785/74404421-cd3dc280-4e6d-11ea-8396-184c9ef2a57c.png)


### 데모 실행
### (server)
### demo-apps/cf-secure으로 이동 후 컴파일
    $ mvn clean install
### demo-apps/cf-secure/target으로 이동 후 .jar파일 실행
    $ java –jar cf-secure-2.1.0-SNAPSHOT.jar

### (client)
### demo-apps/cf-secure로 이동 후 컴파일
    $ mvn clean install
### demo-apps/cf-secure/target으로 이동 후 .jar파일 실행
    $ java –jar cf-secure-2.1.0-SNAPSHOT.jar

![image](https://user-images.githubusercontent.com/47745785/74404622-68369c80-4e6e-11ea-95ba-8b5ef65d177b.png)




coap/http proxy
-----------------------
### demo-apps/cf-proxy/pom.xml로 이동 후 server client와 마찬가지로 californium-core, repositories 수정

![image](https://user-images.githubusercontent.com/47745785/74404696-91572d00-4e6e-11ea-96d9-c315ec7d5c5b.png)

### demo-apps/cf-proxy로 이동 후 컴파일
    $ mvn clean install
### demo-apps/cf-proxy/target으로 이동 후 .jar파일 실행
    $ java –jar cf-proxy-2.1.0-SNAPSHOT.jar

![image](https://user-images.githubusercontent.com/47745785/74404736-aa5fde00-4e6e-11ea-8fc1-42b1be90fd5f.png)




