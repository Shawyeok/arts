##  
32
## [How To Configure a Continuous Integration Testing Environment with Docker and Docker Compose on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-configure-a-continuous-integration-testing-environment-with-docker-and-docker-compose-on-ubuntu-14-04)

### Description
持续测试中我们需要快速创建一个干净、独立的运行环境，之前利用创建虚机的方式速度较慢，集成的成本较高，这种场景与`docker`以及`docker-compose`非常契合，借助`docker-compose`编排出一套运行环境，例如常见的web、db、cache等，通常不会超过1分钟的时间这个环境就准备好了。

有一个小坑需要说明一下，由于db、cache这些服务启动起来并不能立即提供服务，所以依赖这些服务的其他服务启动的时候要有一个等待的过程，这里有一个脚本可以应付这个场景：[wait-for-it.sh](https://github.com/vishnubob/wait-for-it)

### Links
- https://docs.docker.com/compose/