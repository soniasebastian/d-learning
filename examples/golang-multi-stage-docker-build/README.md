# Multi Stage Docker Build

The main purpose of choosing a golang based applciation to demostrate this example is golang is a statically-typed programming language that does not require a runtime in the traditional sense. Unlike dynamically-typed languages like Python, Ruby, and JavaScript, which rely on a runtime environment to execute their code, Go compiles directly to machine code, which can then be executed directly by the operating system.

So the real advantage of multi stage docker build and distro less images can be understand with a drastic decrease in the Image size.


          Multistage docker Builds
DOCKER FILE: example:execute a calculator application
python...use a base image
require ..work dir
install dependecies...RUN APT PYTHON/PIP
advanced ....3 python packages'
binary build....execute...CMD /app......

Python runtime to run application, Docker image created, But Ubuntu base image have lot dependencies/overload
Build/run both are different
Java....Pom.xml, Jar file, ER file...
centOS CAN BE USED /Ubuntu


Now come Multistage Build
2 parts
........> STAGE 1.......>
From Ubuntu [curl, wget by default have]
RUN

CMD [NOT APPLICABLE]


........> STAGE 2.......>
From Python/Java/Distroless image
Copy --from build (base image from stage1)

CMD [/app]

final point have entry point/CMD

fundamental advantage of Multistage docker build

3-tier architecture
forntend-react
backend-java/spring boot
DB-Mysql

Docker file---Ubuntu
Java runtime cannot be choosen directly, if we choose it, docker image become complex...
choose a very rich image...base image with whole dependencies...base image with 2/3 GB

