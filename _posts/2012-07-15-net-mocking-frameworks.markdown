---
layout: post
status: publish
published: true
title: ".Net Mocking Frameworks"
author: Antony Koch
author_login: amkoch
author_email: ant@iamkoch.com
wordpress_id: 57
wordpress_url: http://localhost/~Ant/wordpress/?p=57
date: '2012-07-15 13:59:10 +0100'
date_gmt: '2012-07-15 13:59:10 +0100'
categories:
- ".Net"
- Mocking
- Unit Testing
tags: []
comments: []
---
1.0 Frameworks
There are a number of options, both open source and paid:
1.1 Open Source

EasyMock.NET


Rhino Mocks


Moq


FakeItEasy


NUnit.Mocks (as part of NUnit)


NMock2

1.2 Closed Source&lt;

Microsoft Moles

1.3 Paid

TypeMock Isolator

2.0 Which to Review
Based on our previous experience with Rhino Mocks and Karl's experience / recommendation of Moq (which also has some very positive internet feedback) I will include them. I will also take a look at Microsoft Moles as it has integration with VS2010, something which provides inherent added value. The other options all appear to provide similar or identical core functionality, however our lack of experience with them realistically rules them out simply on learning curve
2.1 Prior Considerations
Something worth noting is the extent to which we will utilise a mocking framework. If our use is limited to providing mocked stubs in unit tests along with the standard dependency injection then using an overly verbose, overly complex solution seems overkill. Furthermore, we've already signalled our intention to provide stubs for systems such as Third Party Finance and quoting, removing a lot of the burden from any mocking solution we choose.
3.0 Pros and Cons
3.1 Rhino Mocks
3.1.1 Pros
+ Team has previous experience with it
+ Good community, open source
+ Explicit, verbose language.
+ Extensive documentation
+ Been around for a while - Mature
3.1.2 Cons
- Requires recording/replaying - can cause semantic issues in a test class
- Can be complex to pick up
- Quote verbose, not always logical/
3.2 Moq
3.2.1 Pros
+ Team member has previous experience with it
+ No recording/replaying
---&gt; ? easier to move common expectations into setup fixtures as a result
+ Fully supports Linq expression trees
+ Fully supports Lambdas
+ Supports full intellisense integration
+ Easy to pick up
+ Explicitly verify number of times method is called at end of each test - greater readiablity.
+ Granularity with respect to testing stubs, services and methods - good control
3.2.2 Cons
- Some would argue that the lack of explicit record and replay states is a con
- Immature compared to alternatives
- Only provides support for .Net 3.5 and above
3.3 Microsoft Moles
3.3.1 Pros
+ Generates moles classes according to specification (defined in xml)
+ Allows mocking of Static, non-static, system and user-generated classes and methods, e.g. DateTime.Now
+ Integration with VS2010
+ Aimed at MSTest
3.3.2 Cons
- Very immature
- Small community (seemingly)
- Dependency on specification defined in XML
- Lack of documentation
4.0 Conclusions
From what I have seen and what I have briefly spiked out in Moq, it seems to fit perfectly. I'll admit bias beforehand having been frustrated by Rhino Mocks prompting a brief investigation into Moq, however the lack of a need to record/reply and its ability to verify in-place the number of times a test has been run, coupled with attractive Linq-style syntax and .Net 3.0 Lambdas push it ahead of Rhino for me. Moles seems too immature at this stage to include it in the project, its community too small and its documentation good, although not as expansive as the other two choices. Also it has a dependency on writing XML documents in order for the Moles code generation to generate the M-prefixed classes used in the code. The fact that we intend to stub out services will reduce the load on t he mocking framework, so the syntactic sugar and simplicity of Moq seems best suited to our needs.
