# fastdfs-spring-boot-starter

FastDFS Java Client(for SpringBoot1.x & SpringBoot 2.x).

* Import dependence

* Initial configuration

* Connection pool

* More method

# Quick start

* Download.

    ```bash
    git clone https://github.com/bluemiaomiao/fastdfs-spring-boot-starter.git
    cd fastdfs-spring-boot-starter
    ```

* Install to local repository.

    ```bash
    mvn clean install
    ```
    
* Add to project.

    ```xml
    <dependency>
        <groupId>com.bluemiaomiao</groupId>
        <artifactId>fastdfs-spring-boot-starter</artifactId>
        <version>1.0-SNAPSHOT</version>
    </dependency>
    ```

* Add annotations and service (``@EnableFastdfsClient``).

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
* Add configuration entries(application.properties).

    ```properties
    fastdfs.nginx-servers=192.168.80.2:8000,192.168.80.3:8000,192.168.80.4:8000
    fastdfs.tracker-servers=192.168.80.2:22122,192.168.80.3:22122,192.168.80.4:22122
    fastdfs.http-secret-key=2scPwMPctXhbLVOYB0jyuyQzytOofmFCBIYe65n56PPYVWrntxzLIDbPdvDDLJM8QHhKxSGWTcr+9VdG3yptkw
    fastdfs.http-anti-steal-token=true
    fastdfs.http-tracker-http-port=8080
    fastdfs.network-timeout=30
    fastdfs.connect-timeout=5
    fastdfs.connection-pool-max-idle=18
    fastdfs.connection-pool-min-idle=2
    fastdfs.connection-pool-max-total=18
    fastdfs.charset=UTF-8
    ```

* Add configuration entries(application.yml).

    ```yaml
    fastdfs:
      charset: UTF-8
      connect-timeout: 5
      http-secret-key: 2scPwMPctXhbLVOYB0jyuyQzytOofmFCBIYe65n56PPYVWrntxzLIDbPdvDDLJM8QHhKxSGWTcr+9VdG3yptkw
      network-timeout: 30
      http-anti-steal-token: true
      http-tracker-http-port: 8080
      connection-pool-max-idle: 20
      connection-pool-max-total: 20
      connection-pool-min-idle: 2
      nginx-servers: 192.168.80.2:8000,192.168.80.3:8000,192.168.80.4:8000
      tracker-servers: 192.168.80.2:22122,192.168.80.3:22122,192.168.80.4:22122
    ```
    
* Enjoy it.