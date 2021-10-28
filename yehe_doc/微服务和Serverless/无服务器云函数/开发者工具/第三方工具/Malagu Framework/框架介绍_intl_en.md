>? Malagu is a third-party development tool with no Tencent Cloud official support unavailable currently. If you have any questions or feedback, please go to the [Malagu community](https://github.com/cellbang/malagu) for discussion and contribution by using issues.


## Malagu Overview

Aka the M framework, Malagu is a serverless-first, componentized, platform-independent progressive application framework based on TypeScript. It uses the same programming language and IoC design to develop frontend, backend, and frontend/backend integrated applications. It combines object-oriented programming (OOP), aspect-oriented programming (AOP), and other elements and draws on many design ideas of Spring Boot.

On the backend, Malagu abstracts a set of APIs to facilitate adaptation to any platforms (SCF, AWS Lambda, Vercel, etc.) and basic frameworks (Express, Koa, Fastify, etc.). It is an upper-layer framework independent of such platforms and basic frameworks.

In serverless scenarios, Malagu is used to develop projects by application. An application generally includes multiple APIs. If the application is large, it should be split into small microapplications or microservices. Just like the principle of granularity breakdown in the microservice architecture, reasonable granularity breakdown enables better application management. The framework will guarantee the execution performance of one application in one function.

For more information, please see [Malagu Framework](https://www.yuque.com/cellbang/malagu).

## Malagu Architecture Diagram

<img src="https://qcloudimg.tencent-cloud.cn/raw/d6e01c817b186c9de2110b8fc5755eac.png" data-nonescope="true">


## Why Malagu?


<dx-accordion>
::: Firm belief that serverless is the future
Serverless is a new-generation cloud computing engine. It is developed to replace the traditional cloud service framework. The core idea of serverless is to enable developers to focus on the business code with no need to care about servers.
:::
::: Serverless status quo
Currently, all cloud vendors and communities are vigorously promoting and advocating the concept of serverless, through which commercial solutions can be implemented with speed and quality at low costs. It is widely acknowledged in the industry that serverless is the combination of FaaS and BaaS, and it may evolve into other forms in the future. However, no matter how its form changes, the core philosophy of serverless will remain the same.
Serverless development experience is subject to the development experience of FaaS, which, however, is not quite satisfactory at present and has many challenges. Some challenges may be hard to overcome at the FaaS underlying layer in the near future, and some may be better to solve at the tool or framework level. Such challenges include cold start, CI/CD, microservice, database access, local development, debugging, and execution, and platform-independency. More and more serverless-first development frameworks will emerge, which not only are resource orchestration and OPS tools, but also provide more advanced serverless or low-code development platforms.
<dx-alert infotype="explain" title="How to solve such challenges?">
You can try solving such problems from the perspective of development framework (which has been proven effective). Then, you should decide whether to use a traditional framework or select a new framework and whether to use a specific or general programming language if you choose a new framework.
</dx-alert>
:::
::: Why a new framework?
With many years of usage of traditional frameworks, most developers can tolerate their development experience. However, when you need to migrate an application developed in a traditional framework to a serverless environment, you will usually encounter various difficult problems, which are generally related to the framework's underlying design. Although you can use the framework's extension capabilities to solve or mitigate some problems, practices show that the threshold for framework transformation is very high, the effect is unsatisfactory, and hacking is required, making the solution less graceful.
If you use a traditional framework in serverless, although your application can run in it, you may still have worries that the application may not be able to run normally in the production environment. Of course, as the underlying technologies of the serverless platform are continuously advanced, the use of traditional frameworks in serverless scenarios are also improved greatly. However, to achieve the optimal status, changes to the application alone may not be enough, and the framework also needs to adapt to serverless scenarios reasonably. Just like when the frontend UI framework tries to be mobile-first, although browsers offer responsive support, the framework also requires adaption. Therefore, a new serverless-first development framework is desired to give full play to the strengths of serverless and make the serverless development experience inherit and even excel the traditional development experience.
:::
::: Why a specific programming language?
Currently, open source communities have many language-neutral serverless tools and frameworks, such as Funcraft, Serverless Framework, and Vercel. Such tools do provide an acceptable experience and can form general standards in terms of OPS, but may be unsatisfactory in terms of the experience of application code development, debugging, and execution. Each programming language has its special benefits in aspects such as development, debugging, and execution, so it is hard for language-neutral serverless tools to achieve an excellent performance while delivering a unified development experience. You can enjoy an ultimate programming experience only by selecting a specific language.
:::
::: Why TypeScript?
Serverless makes it much easier to get started with backend development and greatly reduces the learning costs for frontend developers to develop backend applications based on serverless. In the future, more and more frontend developers will become full-stack developers. TypeScript can be used to develop both frontend and backend applications, so it is very friendly to frontend and full-stack developers.

Its frontend architecture is a serverless-like architecture. For example, a frontend browser needs to load frontend code for execution, and user code also needs to be loaded in a serverless scenario for execution. Therefore, many frontend solutions are natively suitable for serverless scenarios. For example, the frontend can reduce the code size, deployment time, and cold start time through packaging, compression, and tree shaking. Similarly, such optimized solutions are also suitable for serverless scenarios. As a result, if you select TypeScript, you can get direct access to many solutions proven and polished by countless real-world use cases.
In addition, TypeScript is similar to Java, so Java developers can easily switch to its technology stack.
:::
::: Value of Malagu
Malagu is a serverless-first, extensible, componentized progressive application framework based on TypeScript. It shields the underlying details of different serverless platforms and most of the challenges in serverless scenarios. It is developed and improved based on real business scenarios and provides solutions usable at the production level. Moreover, it offers multi-cloud vendor-independent solutions.
:::
</dx-accordion>




## How to Use Malagu

The Malagu framework consists of a series of components, each of which is a node module. You can choose the appropriate components according to your business scenario. You can also develop your own components based on the component mechanism. For the convenience of fast development, Malagu provides a command line tool that has built-in out-of-the-box templates for different use cases. You can quickly create your applications through the command line tool.
1. Run the following commands to install the relevant command line tool.
```sh
$ npm install -g @malagu/cli  # Install Malagu command line tool
$ malagu init project-name    # Use the `malagu init` command to select a template and initialize a template application
$ cd project-name             # Enter the root directory of the application
$ malagu serve                # Start the application. The default port is 3000
```
2. Open a browser and access `http://localhost:3000/`.
