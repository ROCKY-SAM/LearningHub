# LearningHub

# Blogs
> - https://neelbhatt.com/category/net-core/
> - https://www.toptal.com/developers/blog
> - https://engineering.fb.com/
> - https://dev.to/
> - https://cloudemployee.co.uk/blog/
> - https://www.geeksforgeeks.org/
> - https://stackoverflow.blog/
> - https://www.adjust.com/blog/universal-links-vs-deep-links/
> 

# Architecture
> - https://codewithmukesh.com/blog/onion-architecture-in-aspnet-core/

# API
> - https://dzone.com/articles/rest-api-what-is-hateoas

# GIT
> - https://www.gitkraken.com/learn/git/best-practices/git-branch-strategy

# Angular
> - https://coryrylan.com/blog/angular-form-builder-and-validation-management
> - https://www.tutsmake.com/
> - https://github.com/Procaseycash/ng-pure-datatable
> - http://jsfiddle.net/gavinfoley/fR32K/
> - https://nehalist.io/working-with-models-in-angular/ 
> - https://stackblitz.com/angular/jaamvvovxlme?file=angular.json
> - https://angular.io/guide/i18n
> - https://stackblitz.com/angular/aqnrddojgan?file=src%2Fapp%2Fhero-detail%2Fhero-detail.component.ts
> - https://therichpost.com/how-to-implement-fullcalendar-in-angular-8/

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
usage: git remote add []\
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

# Angular 10 - Fix CommonJS or AMD dependencies can cause optimization bailouts
>  When you use a dependency that is packaged with CommonJS, it can result in <a href="https://web.dev/commonjs-larger-bundles/" rel="noreferrer">larger slower applications</a>.Starting with version 10, Angular now warns you when your build pulls in one of these bundles. If you’ve started seeing these warnings for your dependencies, let your dependency know that you’d prefer an ECMAScript module (ESM) bundle.Here is an official documentation - <a href="https://angular.io/guide/build#configuring-commonjs-dependencies" rel="noreferrer">Configuring CommonJS dependencies</a>

In your angular.json file look for the build object and add

```allowedCommonJsDependencies```

as shown below -

```"build": {
  "builder": "@angular-devkit/build-angular:browser",
  "options": {
     "allowedCommonJsDependencies": [
        "rxjs-compat",
         ... few more commonjs dependencies ... 
     ]
     ...
   }
   ...
},```

