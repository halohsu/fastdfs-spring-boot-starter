# 💯fastdfs-spring-boot-starter💯

👉Minimum Java version: ``JDK 11 LTS`` .

A high-performance FastDFS client that is compatible with both SpringBoot1.x and 2.x. Avoiding manual introduction of jar packages that can lead to project confusion and providing commonly used APIs helps to quickly get started with development.

-----

Some links:

- [访问简体中文页面](README_zh_CN.md)
- [Visit English Pages](README.md)

- Gitee: [https://gitee.com/bluemiaomiao/fastdfs-spring-boot-starter](https://gitee.com/bluemiaomiao/fastdfs-spring-boot-starter)
- GitHub: [https://github.com/bluemiaomiao/fastdfs-spring-boot-starter](https://github.com/bluemiaomiao/fastdfs-spring-boot-starter)

![GitHub Release Version](https://img.shields.io/github/v/release/bluemiaomiao/fastdfs-spring-boot-starter?display_name=tag)
![GitHub Star](https://img.shields.io/github/stars/bluemiaomiao/fastdfs-spring-boot-starter?label=star)
![GitHub Fork](https://img.shields.io/github/forks/bluemiaomiao/fastdfs-spring-boot-starter?label=fork)

![GitHub License](https://img.shields.io/github/license/bluemiaomiao/fastdfs-spring-boot-starter)
![GitHub Issues](https://img.shields.io/github/issues/bluemiaomiao/fastdfs-spring-boot-starter)
![GitHub Download](https://img.shields.io/github/downloads/bluemiaomiao/fastdfs-spring-boot-starter/total)
![GitHub Repo Size](https://img.shields.io/github/repo-size/bluemiaomiao/fastdfs-spring-boot-starter)
![Documentation](https://img.shields.io/badge/documentation-yes-brightgreen)

# 🥳Awesome Features

- 👍Automatically add dependencies.
- 👍Initialize configuration items.
- 👍High performance Connection pool based on Commons Pool2.
- 👍More APIs for manipulating FastDFS.
- 👍Supports multiple Trackers, multiple Storage, and multiple NGINX load balancing modes.
- 👍Building source code based on fastdfs client Java (1.29-SNAPSHOT).

# 👊Get Stared

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

# 🛠️Build

## 🍭Clone

```bash
git clone https://github.com/bluemiaomiao/fastdfs-spring-boot-starter.git
cd fastdfs-spring-boot-starter
```

## 🍭Install to local

```bash
mvn clean install
mvn source:jar install
mvn javadoc:jar install
```

## 🍭Add to project

```xml
<dependency>
    <groupId>io.github.bluemiaomiao</groupId>
    <artifactId>fastdfs-spring-boot-starter</artifactId>
    <version>1.0.1-RELEASE</version>
</dependency>
```

## 🍭 Add annotation (``@EnableFastdfsClient``)

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
## 🍭Add some configuration items(application.properties)

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

## Or YAML(application.yml)

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

## 🍭Enjoy it

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

Some specifical methods:

```java
// Enable token feature
FastdfsClientService.autoDownloadWithToken(String fileGroup, String remoteFileName, String clientIpAddress)
// Disable token feature
FastdfsClientService.autoDownloadWithoutToken(String fileGroup, String remoteFileName, String clientIpAddress)
// upload file method
FastdfsClientService.autoUpload(byte[] buffer, String ext)
```

# 🌈License

GNU Lesser General Public License v3.0

- [⚡Home](https://www.gnu.org/licenses/lgpl-3.0.html)
- [⚡Text Version](https://www.gnu.org/licenses/lgpl-3.0.txt)
