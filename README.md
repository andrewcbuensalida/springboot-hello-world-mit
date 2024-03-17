https://classroom.emeritus.org/courses/8898/pages/spring-boot?module_item_id=1486484

# create boiler plate spring boot app

go to https://start.spring.io/
add spring-web dependency

# Create container

open docker desktop first, then in cmd
`docker run -it --rm -p 8080:8080 --name javamaven maven:3.8.3-openjdk-17 bash`
javamaven is the container name. 8080 is the ports. maven:3.8.3-openjdk-17 is the image. bash is the program to run in the container.

# add editor

`apt-get update`
`apt-get install nano`

# edit boiler plater to create a get endpoint

Edit DemoApplication.java to be:

package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
@RestController
public class DemoApplication {

    public static void main(String[] args) {
      SpringApplication.run(DemoApplication.class, args);
    }

    @GetMapping("/hello")
    public String hello(@RequestParam(value = "name", defaultValue = "World") String name) {
      return String.format("Hello %s!", name);
    }

}

# copy spring boot boiler plate into container

in local machine cmd, navigate to inside demo (another demo folder is in demo)
`docker cp demo/. javamaven:/home`

# if you need to remove folder that is not empty in linux

`rm -rf demo`

# Start the spring boot server

Go to container home folder then
`mvn spring-boot:run`

# Check if the endpoint is working
In browser, go to localhost:8080/hello?name=joe

# to create image from container
`docker commit javamaven maven_with_hello_world_springboot`
javamaven is the container name. maven_with_hello_world_springboot is the new image name.