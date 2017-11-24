# 마이크로서비스 아키텍처 with SpringCloud



## 마이크로 서비스 소개



### 마이크로서비스 아키텍처(Microservice Architecture) 란?

서비스는 독립적으로 정보를 제공할 수 있는 단위이고, 여러 개의 서비스를 연결하여 시스템을 구성하는 방식으로 기능, 장소 등 여러 요소에 따라 서비스를 분리할 수 있다. 

> 2주안에 완전히 새로 작성할 수 있는 서비스



#### 기존 개발 방식 설명

기존 단일 서비스 개발방식은 Microservice Architecture와 구분을 위해 Monolithic Architecture라고 부른다. 지금까지 서비스를 개발할 때, 2-tier 또는 3-tier로 개발했다.

![2-tire and 3-tire](http://3.bp.blogspot.com/-VkwNc4nK8-A/VgT3uf4BWSI/AAAAAAAAApo/N65EsLc3Hl0/s1600/Architecture.jpg)

> 이미지 출처 : http://battipati-java-performance-engineer.blogspot.kr/2015/09/difference-between-two-tier-and-three.html



#### 서버 운영을 클라우드로 도입하면 생기는 변화

서버를 클라우드로 이전하면 서버운영이 편해지고, 운영비용도 저렴해진다. 그러나 서비스를 개발하고, 배포하고, 유지보수하는 것은 큰 변화가 없다. 개발자 입장에서는 그냥 하던대로 개발하면 된다.

동시접속자가 증가하고 서버의 능력이 제한되면 어떻게 해야할까?

서버를 증설하고 사용자가 몰리면 서버의



##### 기존방식을 클라우드로 단순 이동

###### 단일서버

단일 서버를 클라우드 기반 가상서버로 이동시 서버의 위치만 변동되었고 물리적으로 서버를 별도로 운영하는 환경과 큰 차이가 없다.

![Single on-premises physical or virtual machine](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/ic728008.png)

###### 로드밸런서 도입

![2-tier and 3-tier with presentation tier scale-out](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/ic728010.png)



> 이미지 출처 : https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-app-patterns-dev-strategies





#### 마이크로서비스 아키텍처는 단순히 서버운영을 이동하는 것이 아니다.

![Monolithic Architecture vs Microservice Architecture](https://inform.tmforum.org/wp-content/uploads/2017/02/flo.ci-microservices-architecture.png)

> 이미지 출처 : https://inform.tmforum.org/features-and-analysis/2017/02/what-are-microservices-and-why-should-you-care/

위 그림처럼 마이크로서비스 아키텍처에서는 각 서비스별 Data Layer가 독립되어 있다.



#### 마이크로서비스 아키텍처의 장단점 

- 장점
  1. 서비스가 여러개로 나뉘어 있기 때문에 문제가 발생했을 때 전체 서비스에 영향을 주지 않고 격리된 환경을 구성할 수 있다.
  2. 크기가 작아서 기능을 파악해 재작성하거나 새로운 기능을 만들거나 기능을 수정하기가 쉽다는 장점이 있다.
  3. 서비스 단위로 개발언어, 서버, 도구 등 여러 기술을 혼합할 수 있다.


- 단점
  1. 반면에 서비스가 분리되어 있으므로 하나의 트랜잭션에 모두 담을 수 없다.
  2. 이를 극복하기 위해서 트랜잭션을 고려해 서비스를 구현하거나 데이터 정합성 유지를 위해 비동기 메세지 큐를 구현하는 등 대책이 필요하다
  3. 분산된 기술을 통합해서 관리할 수 있는 방법이 필요하다.
  4. 초기 구축이 어렵다..





### Spring Cloud로 Microservice Architecture 구현하기

스프링은 Microservice Architecure를 구현하기 위한 다양한 도구를 [Spring Cloud Netflix](http://cloud.spring.io/spring-cloud-netflix/single/spring-cloud-netflix.html)로 지원하고 있다. 



#### 1. Config Server / Client

![ConfigServer](http://docs.pivotal.io/spring-cloud-services/1-4/common/config-server/images/config-server-fig1.png)

> 출처 : http://docs.pivotal.io/spring-cloud-services/1-4/common/config-server/

#####         가. Config Server

​    	Springboot 환경설정(properties, yml)을 특정위치에 올려놓고 다른 서비스들이 공유할 수 있다.    

#####         나. Config Client

​    	ConfigServer를 지정하면 Server에서 Springboot 환경설정을 불러온다.



#### 2. Service Registry : Eureka

![Eureka](https://docs.pivotal.io/spring-cloud-services/1-2/images/service-registry/Netflix-Eureka-d1.png)

> 출처 : https://docs.pivotal.io/spring-cloud-services/1-2/service-registry/background.html

#####     가. Eureka



3. #### Circuit Breaker: Hystrix Clients

![Circuit Breaker: Hystrix Clients](http://cloud.spring.io/spring-cloud-static/Finchley.M2/images/HystrixFallback.png)

> 출처 : http://cloud.spring.io/spring-cloud-static/Finchley.M2/



#### 4. Circuit Breaker: Hystrix Dashboard

![Circuit Breaker: Hystrix Dashboard](http://cloud.spring.io/spring-cloud-static/Finchley.M2/images/Hystrix.png)

> 출처 : http://cloud.spring.io/spring-cloud-static/Finchley.M2/



#### 5. Client side Load balancing : Ribbon

![Client-side load-balancing](http://callistaenterprise.se/assets/blogg/goblog/part7-clientsidelb.png)

![Server-side load-balancing](http://callistaenterprise.se/assets/blogg/goblog/part7-serversidelb.png)

> 출처 : http://callistaenterprise.se/blogg/teknik/2017/04/24/go-blog-series-part7/



#### 5. API Gate-way : ZUUL

![Zuul](https://exampledriven.files.wordpress.com/2016/07/zuul-api-gateway.jpg)

> 출처 : https://exampledriven.wordpress.com/2016/07/06/spring-cloud-zuul-example/





### 참고자료

* spring cloud netflix 
    http://cloud.spring.io/spring-cloud-netflix/single/spring-cloud-netflix.html

* [배민 API GATEWAY - spring cloud zuul 적용기]
    http://woowabros.github.io/r&d/2017/06/13/apigateway.html

* zuul 튜토리얼
    https://exampledriven.wordpress.com/2016/07/06/spring-cloud-zuul-example/

* Spring Security and Angular(Zuul 인증내용이 들어있다.)
    https://spring.io/guides/tutorials/spring-security-and-angular-js/

* 조대협 - 소프트웨어 개발 트랜드 및 MSA (마이크로 서비스 아키텍쳐)의 이해
    https://www.slideshare.net/Byungwook/msa-52918441

* 마이크로서비스 아키텍처와 DevOps 기술 - Amazon 사례를 중심으로 (윤석찬)
    https://www.slideshare.net/awskorea/micro-services-devops-with-aws-partner-techshift

* 마이크로서비스 아키텍처로 개발하기
    https://www.slideshare.net/saltynut/building-micro-service-architecture