---
sort: 1
title: Performance Test Cycle
---

# An Understanding Of A Complete Performance Test Cycle

<style>
    img[alt=pic00000003] { 
        display: block;
        width: 780px; 
    }
</style>
![pic00000003](/assets/images/pic00000003.png)

A complete test cycle consists of four phases: **SetUp**, **WarmUp**, **Test** and **TearDown**.

The **SetUp** phase is executed before the test begins and is used to prepare the test environment.

In the **WarmUp** phase, the virtual users are started linearly, one by one, to gradually stress and warm up the system under test.

During the test phase, all the virtual users are run simultaneously, with each virtual user running the test cases as specified in the test plan.
The execution of each virtual user is split into one or more sessions, and the framework allows specific scripts to be run at the beginning and end of a session to simulate certain periodic behaviors,
such as logging in and out of a website.

At the end of the test, all user sessions are guaranteed to end, and then the test enters the **TearDown** phase, which is used to free up some resources needed for the test.

## Reference

* [Learn more about how to define the SetUp and TearDown actions in the test script](/ScriptGuides/SetUpAndTearDown.html)
