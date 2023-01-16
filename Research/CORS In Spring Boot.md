<h1>Research: How to Use CORS in Spring Boot</h1>

<h2>Table of Contents</h2>

- [Introduction](#introduction)
  - [Research Purpose](#research-purpose)
  - [Research Questions](#research-questions)
- [What is CORS?](#what-is-cors)
- [How does CORS work?](#how-does-cors-work)
- [How can you use CORS to increase the security of your application?](#how-can-you-use-cors-to-increase-the-security-of-your-application)
- [How can you use CORS in a Spring Boot application?](#how-can-you-use-cors-in-a-spring-boot-application)
- [Summary](#summary)


# Introduction

## Research Purpose

This research serves the purpose of giving more insights about what CORS is, what purpose it serves and how to use in an application. I have decided to start this research, because I was getting CORS problems while developing the Chess Tournament Manager and wanted to know more about it.

## Research Questions

In this research, there is a main question which answer should be very clear at the end of this research:

***How can you use CORS in a Spring Boot application?***

Besides this main question, there are several sub-questions that should also be answered in this research:

1. What is CORS?
2. How does CORS work?
3. How can you use CORS to increase the security of your application? 

# What is CORS?

CORS stands for Cross-Origin Resource Sharing. It is a security feature implemented by web browsers that blocks web pages from making requests to a different domain than the one that served the web page.

For example, if a web page served from "https://example1.com" makes an HTTP request to "https://example2.com", the browser will block the request by default. CORS is a mechanism that allows web pages served from one domain to make requests to a different domain, but with the approval of the server.

# How does CORS work?

CORS works by adding HTTP headers to server responses that indicate which origin domains are allowed to make requests to the server. When a browser receives a response with the appropriate headers, it will allow the request to proceed. If the headers are not present or the origin domain is not on the list of allowed domains, the browser will block the request.
The headers that the browser looks for are:

- Access-Control-Allow-Origin: This header indicates which domains are allowed to make requests to the server. The value of this header can be a specific domain (e.g. "https://example1.com"), or a wildcard ("*") which allows any domain to make requests.
- Access-Control-Allow-Methods: This header indicates which HTTP methods are allowed to be used when making a request.
- Access-Control-Allow-Headers: This header indicates which headers are allowed to be sent with a request.
- Access-Control-Allow-Credentials: This header indicates whether credentials (such as cookies) can be sent with a request.

# How can you use CORS to increase the security of your application? 

By configuring the allowed origin domains, you can use CORS to increase the security of your application by only allowing requests from trusted domains. Additionally, CORS can also be used to limit the types of requests that are allowed (such as GET, POST, etc.).

For example, you could configure your server to only allow requests from a specific domain, or only allow requests that use the GET method. This can help to prevent unauthorized access to your server, as well as prevent malicious actors from making unwanted requests.

# How can you use CORS in a Spring Boot application?

To use CORS in a Spring Boot application, you can add the spring-boot-starter-web dependency to your project. 

```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
```

Then you can do two things. The first option is to configure a WebMvcConfigurer bean in your application, which is what I did:

```java
    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/*").allowedOrigins("http://localhost:3000");
            }
        };
    }
```

In this case, I allowed all types of request methods for all routes coming from the origin `http://localhost:3000`, which is the address for my Vue.js 3 frontend application. For an application meant for production, you would specify certain request methods that are allowed, use an environment variable for the address and specify certain routes. If you have certain users with different types of roles, you could also specify which users with which roles are allowed to make certain requests.

You could also configure CORS by adding this line of code on top of your Spring Boot controller:

```java
@CrossOrigin(origins = "http://localhost:3000")
```

# Summary

In this research, we have taken a look at CORS. We have discussed what it is, how it works and how it should be used to increase application security. We have also taken a look at how to implement it in a Spring Boot applciation.

