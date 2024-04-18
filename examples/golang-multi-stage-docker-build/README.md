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

1ST STAGE.......form ubuntu as build, Java, React,mysql, Java application..frontend.....ENTRYPOINT /app.ear

400MB
50MB'100MB......1GB WITH ALL THESE

2ND STAGE....final stage
FROM OPENJDK: 11  [100mb]
COPY -- from build [50mb] (ubuntu create as alias) from 1st stage 
Entrypoint [app.ear]........

150mb...reduced size..multistage.........



3 stages......

1st stage..fromtend
2nd stage....Backend
3rd stage.....final end....CMD

N NUMBER OF STAGES, THERE WILL BE ONLY ONE FINAL STAGE WHICH IS A MINIMALIST IMAGE..ADVANTAGE OF DOCKER MULTISTAGE BUILD


              DISTROLESS IMAGE
very minimalistic image/LIGHTWEIGHT DOCKER IMAGE hardly have packages

python distroless image...will only have python run time ...
openjdk....100mb,,only that example

GOLANG APPLICATION..STATISTCIALLY TYPED APPLICATION..DONT NEED GO RUNTIME
10MB,15MB SIZE FOR IMAGE

      PYTHON..SHELL COMMANDS....FIND, LS, WGET..NOT ABLE TO EXECUTE

/APP CAN BE EXECUTED...

    ANOTHER ADVANTAGE
REDUCED IMAGE SIZE
SECURITY


        DOCKER IMAGES

UBUNTU IMAGE, PYTHON RUN TIME ENV IMAGES..HACKERS
DISTROLESS IMAGES MOVED TO PYTHON 
PYTHON RUNTIME IMAGE..NO BASIC IMAGES
SO PRIVIDE HIGH LEVEL OF SECURITY
NO OS RELATED VULNERABILITILES

      GO LANGUAGE...NO NEED OF RUNTIME
SO DISTROLESS IMAGES NO VULNERABILITIES....NO EXPOSURE TO SECURITY THREATS


https://github.com/GoogleContainerTools/distroless/blob/main/java/README.md 
   for getting java distroless image
   







