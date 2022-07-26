---
title: 'Annotation'
date: 2022-07-26 00:00:00
featured_image: 
excerpt: Annotation에 대해
---

## 스프링 애너테이션
* 기존에 XML에서 빈 설정을 애너테이션을 이용해서 자바 코드에서 설정하는 방법
* 기능이 복잡해짐에 따라 XML에서 설정하는 것보다 유지 보수에 유리함
* 현재 애플리케이션 개발 시 XML 설정 방법과 애너테이션 방법을 혼합해서 사용함

스프링에서 애너테이션을 사용하려면 먼저 스프링에서 제공하는 애너테이션 관련 클래스를 XML 설정 파일에서 빈으로 설정해야 합니다.
```xml
<bean class="org.springframework.web.servlet.mvc.annotation.DefaultAnnotationHandlerMapping"/>  <!-- 클래스 레벨에 @RequestMapping을 처리합니다. -->
<bean class="org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter"/>   <!-- 메서드 레벨에 @RequestMapping을 처리합니다. -->
<context:component-scan base-package="com.spring"/>                   <!-- com.sping 패키지에 존재하는 클래스에 애너테이션이 적용되도록 설정합니다. -->
```
