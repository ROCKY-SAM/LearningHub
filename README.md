# LearningHub

# Next to watch
> - https://www.tatvasoft.com/blog/reactjs-best-practices/amp/
> - https://www.edureka.co/blog/interview-questions/react-interview-questions/amp/
> - https://www.coursedio.com/course/react-software-architecture/next-steps
> - https://www.youtube.com/watch?v=NsKBZuagLcg&t=1290s
> 

# Blogs
> - https://neelbhatt.com/category/net-core/
> - https://www.toptal.com/developers/blog
> - https://engineering.fb.com/
> - https://dev.to/
> - https://cloudemployee.co.uk/blog/
> - https://www.geeksforgeeks.org/
> - https://stackoverflow.blog/
> - https://www.adjust.com/blog/universal-links-vs-deep-links/

# CICD 
Building and Deploying your Code with Azure Pipelines
> - https://www.youtube.com/watch?v=NuYDAs3kNV8
> - https://docs.microsoft.com/en-us/azure/devops-project/azure-devops-project-aspnet-core
> 

# Architecture
> - https://codewithmukesh.com/blog/onion-architecture-in-aspnet-core/

# API
> - https://dzone.com/articles/rest-api-what-is-hateoas

# GIT
> - https://www.gitkraken.com/learn/git/best-practices/git-branch-strategy

# .NET
> - https://www.tutorialsteacher.com/core/aspnet-core-introduction
> - https://www.sam-solutions.com/blog/building-microservice-with-onion-architecture/
> - https://www.lambdatest.com/blog/comprehensive-guide-to-javascript-design-patterns/

# https://www.codecademy.com/learn/introduction-to-javascript/modules/learn-javascript-introduction

# Single-responsibility principle (SRP)
> The single-responsibility principle (SRP) is a computer-programming principle that states that every module, class or function in a computer program should have responsibility over a single part of that program's functionality, and it should encapsulate that part. All of that module, class or function's services should be narrowly aligned with that responsibility.


# TypeScript complain “has no initializer and is not definitely assigned in the constructor” about constructors by returning constructed object

> strictPropertyInitialization forces you to initialize all properties that are not optional in the constructor of the class. This check can be useful as it ensures that you don't get unexpected uninitialized properties. There are several ways to get around the error, the first two are the general way to do it, in your case only the last on applies (I include all for completeness):

Initialize the field

If you define the property as boolean if should be true or false initialize it when you declare the field or initialize it in the constructor:
```
class MyClass {
  someField: boolean = false;
  constructor() {
    return { someField: true };
  }
}
```
Make the field optional

If the field can be undefined, you should mark this in the field declaration either by using ? or typing the field as undefined|boolean
```
class MyClass {
    //someField?: boolean;
    someField: boolean | undefined;
    constructor() {
        return { someField: true };
    }
}
```
Use a not null assertion

> In your case since in the constructor you are actually not initializing the current object (this) but returning a new one, you can tell the compiler it is wrong about the error and use a not null assertion. This assertion is specifically introduced because there are limitations in strictPropertyInitialization checks and sometimes the compiler gets it wrong. For those cases you can override what the compiler thinks, but you have to be explicit about it:
```
class MyClass {
    someField!: boolean;
    constructor() {
        return { someField: true };
    }
}
```

# Creating local repository: 
Initially user may have created the local git repository.\
```sh $ git init```
- This will make the local folder as Git repository,Link the remote branch:- Now challenge is associate the local git repository with remote master branch.\
```sh $ git remote add RepoName RepoURL```
usage: git remote add []
- Test the Remote\
```sh $ git remote show``` --->Display the remote name\
```sh $ git remote -v``` --->Display the remote branches\
- Now Push to remote\
```sh $git add . ```----> Add all the files and folder as git staged\
```sh $git commit -m "Your Commit Message" ```- - - >Commit the message\
```sh $git push ```- - - - >Push the changes to the upstream\


# primeNG
Question : PrimeNG Table filterGlobal TS2339: Property 'value' does not exist on type 'EventTarget'\
Answer : Your HTML input should be like this\
```<input pInputText type="text" (input)="applyFilterGlobal($event, 'contains')" placeholder="Filter" />```
and in your TS do this
```
applyFilterGlobal($event: any, stringVal: any) {
    this.dt!.filterGlobal(($event.target as HTMLInputElement).value, 'contains');
  }
```
if you get error for dt add below line
```
import { ViewChild } from '@angular/core';
import  {Table} from 'primeng/table';
@ViewChild('dt') dt: Table | undefined;
```
![image](https://user-images.githubusercontent.com/12700182/120366535-6461ae80-c32d-11eb-8f47-3f601f06e91c.png)

![image](https://user-images.githubusercontent.com/12700182/120595693-709a5880-c460-11eb-84bb-7e794b5a3a31.png)

<a href="https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens" rel="noreferrer">GitLens</a> &amp; 
<a href="https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph" rel="noreferrer">GitGraph</a>
Below snapshot highlights how gitlens is showing commit over time
![image](https://user-images.githubusercontent.com/12700182/120990249-fa6a5e80-c79d-11eb-813b-105ad12c5903.png)
And the below picture is for the the amazing vivid GitGraph
![image](https://user-images.githubusercontent.com/12700182/120990264-ffc7a900-c79d-11eb-87c2-e22022203c24.png)


![image](https://user-images.githubusercontent.com/12700182/121293564-759c5380-c909-11eb-8160-1038f1926e48.png)


# Update a user
```
var url = "http://localhost:8080/api/v1/users";

var data = {};
data.firstname = "John2";
data.lastname  = "Snow2";
var json = JSON.stringify(data);

var xhr = new XMLHttpRequest();
xhr.open("PUT", url+'/12', true);
xhr.setRequestHeader('Content-type','application/json; charset=utf-8');
xhr.onload = function () {
    var users = JSON.parse(xhr.responseText);
    if (xhr.readyState == 4 && xhr.status == "200") {
        console.table(users);
    } else {
        console.error(users);
    }
}
xhr.send(json);
 ```
# Delete a user
```
var url = "http://localhost:8080/api/v1/users";
var xhr = new XMLHttpRequest();

xhr.open("DELETE", url+'/12', true);
xhr.onload = function () {
    var users = JSON.parse(xhr.responseText);
    if (xhr.readyState == 4 && xhr.status == "200") {
        console.table(users);
    } else {
        console.error(users);
    }
}
xhr.send(null);
  ```

# Azure DevOps: Resolving 'Conflict Prevents Automatic Merging'
> https://www.shawnmcgough.com/conflict-prevents-automatic-merging/
  
# What Is ADA Compliance? (And What Does ADA Compliance Mean for Your Website?)
> https://www.webfx.com/blog/marketing/what-is-ada-compliance/
 
# dynamic var in i18n message
![image](https://user-images.githubusercontent.com/12700182/126354354-77000187-a7a9-4eef-9baf-98517817113b.png)

# Full calendar buttonText on 'today' view not updating
> https://stackoverflow.com/questions/56941545/buttontext-on-today-view-not-updating

  ![image](https://user-images.githubusercontent.com/12700182/127805137-3ee13816-b236-4e06-a795-7f45848635b5.png)
  
```
  //Inhertiance example
class person{
    constructor(name,job){
        this.name = name;
        this.job =job;
    }
    //method to return the string
    toString(){
        return (`Name of person: ${this.name}  --job ${this.job}`   );
    }
}
class student extends person{
    constructor(name,job,id){
        //super keyword to for calling above class constructor
        super(name,job);
        this.id = id;
    }
    toString(){
        return (`${super.toString()},Student ID: ${this.id}`);
    }
}
let student1 = new student('Sameera','developer',22);
console.log(student1.toString());
```  

  ```
  unamePattern = "^[a-z0-9_-]{8,15}$";
  pwdPattern = "^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?!.*\s).{6,12}$";
  mobnumPattern = "^((\\+91-?)|0)?[0-9]{10}$"; 
  emailPattern = "^[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,4}$";
  ```
