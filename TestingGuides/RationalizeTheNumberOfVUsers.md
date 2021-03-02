---
sort: 2
title: Rationalize The Number Of VUsers
---

# Rationalize The Number Of Virtual Users On Each Worker

First the virtual users of each type will be evenly distributed across the worker nodes.

The difference in the number of virtual users of each type on each worker node will not be greater than one.

<style>
    img[alt=pic00000004] { 
        display: block;
        width: 680px; 
    }
</style>
![pic00000004](/assets/images/pic00000004.png)

This has the advantage that the test cases executed and the system resources used by each worker will be relatively similar, with low variance between workers.

Each worker is a Pod of Kubernetes, and all virtual users on a worker will share that worker's CPU and Memory resources in a threaded fashion.

The total number of virtual users must be an integer multiple of the number of workers, and for the number of virtual users, the more workers will consume more system resources, 
but also the more stress will be placed on the system under test.
