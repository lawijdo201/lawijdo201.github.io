---
title: 'Annotation'
date: 2022-07-26 00:00:00
featured_image: 
excerpt: Annotation에 대해
---

## 스프링 어노테이션
* 기존에 XML에서 빈 설정을 애너테이션을 이용해서 자바 코드에서 설정하는 방법
* 기능이 복잡해짐에 따라 XML에서 설정하는 것보다 유지 보수에 유리함
* 현재 애플리케이션 개발 시 XML 설정 방법과 어노테이션 방법을 혼합해서 사용함


### <context:component-scan base-package="패키지명"/>
* <context:component-scan> 태그를 사용해 패키지 이름을 지정하면 애플리케이션 실행 시 해당 패키지에서 애너테이션으로 지정된 클래스를 빈으로 만들어 줍니다.

아래는 <context:component-scan> 태그로 지정한 패키지에 위치하는 클래스에 지정하는 여러 가지 어노테이션입니다.

|어노테이션|기능|
|----------|----------------|
|@Controller|스프링 컨테이너가 component-scan에 의해 지정한 클래스를 컨트롤러 빈으로 자동 변환합니다.|
|@Service|스프링 컨테이너가 component-scan에 의해 지정한 클래스를 서비스 빈으로 자동 변환합니다.|
|@Repository|스프링 컨테이너가 component-scan에 의해 지정한 클래스를 DAO 빈으로 자동 변환합니다.|
|@Component|스프링 컨테이너가 component-scan에 의해 지정한 클래스를 빈으로 자동 변환합니다.|


스프링에서 애너테이션을 사용하려면 먼저 스프링에서 제공하는  어노테이션 관련 클래스를 XML 설정 파일에서 빈으로 설정해야 합니다.
```xml
<!-- 클래스 레벨에 @RequestMapping을 처리합니다. -->
<bean class="org.springframework.web.servlet.mvc.annotation.DefaultAnnotationHandlerMapping"/>
<!-- 메서드 레벨에 @RequestMapping을 처리합니다. -->
<bean class="org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter"/>
<!-- 적용한 패키지에 존재하는 클래스에 애너테이션이 적용되도록 설정합니다. -->
<context:component-scan base-package="패키지명"/>              
```

주요 어노테이션
|이름|설명|
|---|---|
|@RequestMapping|요청에 대해 어떤 Controller, 어떤 메소드가 처리할지를 맵핑하기 위한 어노테이션|


