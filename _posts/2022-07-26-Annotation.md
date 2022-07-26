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

## Parameter 관련 어노테이션

|이름|설명|
|---|---|
|@RequestMapping|요청에 대해 어떤 Controller, 어떤 메소드가 처리할지를 맵핑하기 위한 어노테이션|
|@RequestParam|@RequestParam 어노테이션은 HttpServletRequest 객체와 같은 역할을 한다.|
|@ModelAttribute|@ModelAttribute 어노테이션은 @RequestParam과 달리 객체를 매핑해준다.|


#### RequestParam

```java
@Controller
public class LoginController {    
    //"userID"란 데이터의 이름을 가진 데이터를 String userID에 집어넣는다.
    public ModelAndView login2(@RequestParam("userID") String userID, @RequestParam("userName") String userName) throws Exception {
		request.setCharacterEncoding("utf-8");
		ModelAndView mav = new ModelAndView();
		mav.setViewName("result");
		
   		// getParameter() 메서드를 이용할 필요가 없습니다.
		// String userID = request.getParameter("userID");
		// String userName = request.getParameter("userName");
		
		System.out.println("userID: "+userID);
		System.out.println("userName: "+userName);
		mav.addObject("userID", userID);
		mav.addObject("userName", userName);

		return mav;
	}
}
```
```java
@RequestParam("가져올 데이터의 이름") [데이터타입] [가져온데이터를 담을 변수]
```

#### RequestParam의 required 속성
* @RequestParam 적용 시 required 속성을 생략하면 기본값은 true임
* required 속성을 true로 설정하면 메서드 호출 시 반드시 지정한 이름의 매개변수를 전달해야함(매개변수가 없으면 예외가 발생)
* required 속성을 false로 설정하면 메서드 호출 시 지정한 이름의 매개변수가 전달되면 값을 저장하고 없으면 null을 할당함

```java
@RequestParam(value="userName", required=false) String userName
```

#### RequestParam을 이용해 Map에 매개변수 값 설정하기
* 전송되는 매개변수의 수가 많을 경우 Map에 바로 저장해서 사용하면 편리

```java
public ModelAndView login3(@RequestParam Map<String, String> info) throws Exception {
	request.setCharacterEncoding("utf-8");
	ModelAndView mav = new ModelAndView();
	
	//Map에 저장된 매개 변수의 이름으로 전달된 값을 가져옵니다.
	String userID = info.get("userID");
	String userName = info.get("userName");
	
	System.out.println("userID: "+userID);
	System.out.println("userName: "+userName);
	
	mav.addObject("info", info);	//@RequestParam에서 설정한 Map 이름으로 바인딩합니다.
	mav.setViewName("result");
	return mav;
}
```

```java
RequestParam Map<String, String> info
```

@RequestParam을  Map에 전송된 매개변수의 이름을 key, 값을 value로 지정합니다.


```java
public ModelAndView login4(@ModelAttribute("info") LoginVO loginVO) throws Exception {
	request.setCharacterEncoding("utf-8");
	ModelAndView mav = new ModelAndView();
	System.out.println("userID: "+loginVO.getUserID());
	System.out.println("userName: "+loginVO.getUserName());
	mav.setViewName("result");
	return mav;
```

```java
@ModelAttribute("info") LoginVO loginVO
```

@ModelAttribute("info") LoginVO loginVO는 전달된 매개변수에 대해 loginVO 클래스 객체를 생성합니다. 이어서 매개변수 이름과 같은 속성에 매개변수 값을 설정한 후 info 이름으로 바인딩합니다. 이는 addObject()를 이용할 필요 없이 info를 이용해 바로 JSP에서 LoginVO속성에 접근할 수 있습니다. 예를 들어 로그인창에서 전달된 매개변수 이름이 userID이고, 값이 hong일 경우, @ModelAttribute로 LoginVO를 지정하면 전달 시 LoginVO의 속성 userID에 전달된 값 hong을 자동으로 설정해 줍니다.

```jsp
${info.userID}
```
## @Autowired 이용해 빈 주입하기

XML에서 빈을 설정한 후 애플리케이션이 실행될 때 빈을 주입해서 사용하면 XML 파일이 복잡해지면서 사용 및 관리가 불편합니다. 이를 해결하기 위해 @AutoWired가 등장했습니다.

#### Autowired의 특징
* 기존 XML 파일에서 각각의 빈을 DI로 주입했던 기능을 코드에서 애너테이션으로 자동으로 수행합니다.
* @Autowired를 사용하면 별도의 setter나 생성자 없이 속성에 빈을 주입할 수 있습니다.
