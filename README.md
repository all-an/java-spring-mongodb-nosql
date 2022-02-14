![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=java&logoColor=white)
![SpringBoot](https://img.shields.io/badge/Spring_Boot-F2F4F9?style=for-the-badge&logo=spring-boot)
![MongoDB](https://img.shields.io/badge/MongoDB-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white)
![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=Postman&logoColor=white)
![Spring](https://img.shields.io/badge/Spring-6DB33F?style=for-the-badge&logo=spring&logoColor=white)

## Java Spring Boot / MongoDB / NoSQL 
### Posts and Comments API

Requirements : 
- Java 11
- Spring Boot
- MongoDB 5


### MongoDB dependency:

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>

```

<p align="center">
        <a href="https://www.linkedin.com/in/all-an/">
        <img align="center" width="691" height="198"  src="/img/img1.png" />
</a>
</p>

#### Simple sample Enconding String in JS: ( for later consult )

```js
encodeURIComponent("Allan Pereira Abrahão")
'Allan%20Pereira%20Abrah%C3%A3o'
```

#### URL decoder class in Java (this project):

```java
package com.project.resources.util.URL;

import java.io.UnsupportedEncodingException;
import java.net.URLDecoder;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.TimeZone;

public class URL {

	public static String decodeParam(String text) {
		try {
			return URLDecoder.decode(text, "UTF-8");
		} catch (UnsupportedEncodingException e) {
			return "";
		}
	}
	
	public static Date convertDate(String textDate, Date defaultValue) {
		SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
		sdf.setTimeZone(TimeZone.getTimeZone("GMT"));
		try {
			return sdf.parse(textDate);
		} catch (ParseException e) {
			return defaultValue;
		}		
	}
}

```


### Title Search and Full Search sample endpoints:

```bash

localhost:8080/posts/titlesearch?text=bom%20dia

localhost:8080/posts/fullsearch?text=bom&maxDate=2022-05-02

```
### Post Repository Methods:
#### Search and Find :

```java
        @Query("{ 'title': { $regex: ?0, $options: 'i' } }")
	List<Post> searchTitle(String text);
	
	List<Post> findByTitleContainingIgnoreCase(String text);
	
	@Query("{ $and: [ { date: {$gte: ?1} }, { date: { $lte: ?2} } , { $or: [ { 'title': { $regex: ?0, $options: 'i' } }, { 'body': { $regex: ?0, $options: 'i' } }, { 'comments.text': { $regex: ?0, $options: 'i' } } ] } ] }")
	List<Post> fullSearch(String text, Date minDate, Date maxDate);
```

### MongoDB Regex Reference:

https://docs.mongodb.com/manual/reference/operator/query/regex/
https://docs.mongodb.com/manual/reference/operator/query-logical/
https://docs.mongodb.com/manual/reference/operator/query-comparison/
