---
layout: post
title:  "C/C++ Coding Guides"
date:   2019-03-01 10:02:50 +0100
tags:   [c,c++,style,guide]
---

C/C++ coding guideline reference for my current project.

## Practices
* Unit Testing/TDD: Any automated tests are better than none. Ideally TDD is used. Remember that automated tests are code that has to be maintained, and that the subjects under test are dependencies. Try to reduce coupling between tests and test subjects. Test externally observable behavior and not the internals of the implementation. Don't get obsessed with metrics.
* Code Reviews: Perform code reviews. Don't do it once right before code freeze, don't do it buraucratically, filling out forms for documenting QA measures. Do it continuously as part of pair programming, fostering a common understanding of the code base.
* Pair programming: Encourage pair programming. This is NOT just two DEVs doing the work of one. It's a constant feedback loop, it creates a deeper common understanding through dialog and discussion, it's energizing and it's fun. Do it.

## Clean Code, Maintainability

* Code style: Dictating particular naming or indentation conventions is not a subject of the guidelines. Choose and refer to any reasonable existing conventions (Stroustroup, Boost, Google). The key is using them consistently. The IDE's auto-formatting capabilities might help here  
* [Prefer C++ to C](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#cpl-c-style-programming)
* Know and obey the SOLID principles, use design patterns where appropriate
* Try to stay DRY. Duplicated code with subtle changes is a missed opportunity for abstraction and creates maintenance horrors
* Let the code express ideas (using meaningful names). Use comments for expressing implicit intents, or workarounds
* Seperate specific behavior from general functionality using command or state patterns

## Documentation

* Document the principles of design (essential classes/entities and their relationships) 
* Document the principles of the architecture, e.g. which components run where and talk to whom using which channels. 
* Document the essential control flows, e.g. startup and command/event processing
* Don't get obsessed with UML
* Don't get obsessed with doc generators. Write meaningful code and use this code to discuss and reason about a program

## Safety & Security

* Perform input validation on component boundaries where IPC or File IO happens
* Don't rely on client-side input validation
* Know about implicit type conversions and avoid them
* More to come

## Static Code Analysis

* Use multiple compilers, e.g. clang in IDE, and g++ for production builds
* Use additional code analysers, such as CppCheck, SonarCube, ...

## Dynamic Code Analysis

* Test with a runtime and memory checker, e.g. valgrind. Run it from your IDE. 

## References

* [C++ Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines.html)
* [SEI CERT C++ Coding Standard](https://wiki.sei.cmu.edu/confluence/pages/viewpage.action?pageId=88046682)
* [OWASP](https://www.owasp.org/index.php/OWASP_Secure_Coding_Practices_-_Quick_Reference_Guide)
* [Seastars Clean Codebase](https://github.com/scylladb/seastar)



[C++ Core Guidelines]: https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines
[C is obsolete]: https://www.youtube.com/watch?v=KlPC3O1DVcg
[Stroustroups FAQ]: http://stroustrup.com/bs_faq.html