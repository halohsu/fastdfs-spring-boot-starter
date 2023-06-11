# 💯fastdfs-spring-boot-starter💯

👉最低 Java 版本: ``JDK 11 LTS`` .

> 一个与 SpringBoot 1.x 和 2.x 兼容的高性能 FastDFS 客户端。避免手动引入可能导致项目混乱的 jar 包，并提供常用的 API ，有助于快速开始开发。

# 🥳令人惊叹的功能

- 👍自动添加依赖项
- 👍初始化配置项
- 👍基于 Commons Pool2 的高性能连接池
- 👍更多用于操作 FastDFS 的 API
- 👍支持多个跟踪器、多个存储和多个 NGINX 负载平衡模式
- 👍基于 FastDFS 客户端 Java 构建源代码（1.29-SNAPSHOT）

# 👊 快速开始

## 🍧Maven

```xml
<dependency>
    <groupId>io.github.bluemiaomiao</groupId>
    <artifactId>fastdfs-spring-boot-starter</artifactId>
    <version>2.0.1-RELEASE</version>
</dependency>
```

## 🍧Gradle

```groovy
compile group: 'io.github.bluemiaomiao', name: 'fastdfs-spring-boot-starter', version: '2.0.0-RELEASE'
```

# 🛠️编译

## 🍭克隆

```bash
git clone https://github.com/bluemiaomiao/fastdfs-spring-boot-starter.git
cd fastdfs-spring-boot-starter
```

## 🍭安装到本地

```bash
mvn clean install
mvn source:jar install
mvn javadoc:jar install
```

## 🍭添加到项目

```xml
<dependency>
    <groupId>io.github.bluemiaomiao</groupId>
    <artifactId>fastdfs-spring-boot-starter</artifactId>
    <version>1.0.1-RELEASE</version>
</dependency>
```

## 🍭添加注解 (``@EnableFastdfsClient``)

```java
@EnableFastdfsClient
@SpringBootApplication
public class DemoApplication {

    @Autowired
    private FastdfsClientService fastdfsClientService;

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```
## 🍭添加一些配置(application.properties)

```properties
fastdfs.nginx-servers=192.168.80.2:8000,192.168.80.3:8000,192.168.80.4:8000
fastdfs.tracker-servers=192.168.80.2:22122,192.168.80.3:22122,192.168.80.4:22122
fastdfs.http-secret-key=your key
fastdfs.http-anti-steal-token=true
fastdfs.http-tracker-http-port=8080
fastdfs.network-timeout=30
fastdfs.connect-timeout=5
fastdfs.connection-pool-max-idle=18
fastdfs.connection-pool-min-idle=2
fastdfs.connection-pool-max-total=18
fastdfs.charset=UTF-8
```

## 或者 YAML(application.yml)

```yaml
fastdfs:
  charset: UTF-8
  connect-timeout: 5
  http-secret-key: your key
  network-timeout: 30
  http-anti-steal-token: true
  http-tracker-http-port: 8080
  connection-pool-max-idle: 20
  connection-pool-max-total: 20
  connection-pool-min-idle: 2
  nginx-servers: 192.168.80.2:8000,192.168.80.3:8000,192.168.80.4:8000
  tracker-servers: 192.168.80.2:22122,192.168.80.3:22122,192.168.80.4:22122
```

## 🍭享受吧

```java
@Autowired
private FastdfsClientService remoteService;

// Upload file
String[] remoteInfo;
try {
    remoteInfo = remoteService.autoUpload(image.getBytes(), type);
    log.info("Server Group: " + remoteInfo[0]);
    log.info("Server ID: " + remoteInfo[1]);
} catch (Exception e) {
    log.error("Upload file error: " + e.getMessage());
    return HttpStatus.INTERNAL_SERVER_ERROR;
}

// Download file
String group = file.getGroup();
String storage = file.getStorageId();
String remoteFile = "Get file error.";

try {
    remoteFile = fastdfs.autoDownloadWithToken(group, storage, remoteAddress);
} catch (Exception e) {
    log.error("Get file error: " + e.getMessage());
}
```

一些特定的方法:

```java
// Enable token feature
FastdfsClientService.autoDownloadWithToken(String fileGroup, String remoteFileName, String clientIpAddress)
// Disable token feature
FastdfsClientService.autoDownloadWithoutToken(String fileGroup, String remoteFileName, String clientIpAddress)
// upload file method
FastdfsClientService.autoUpload(byte[] buffer, String ext)
```

# 🌈协议与许可

GNU Lesser General Public License v3.0

- [⚡Home](https://www.gnu.org/licenses/lgpl-3.0.html)
- [⚡Text Version](https://www.gnu.org/licenses/lgpl-3.0.txt)
