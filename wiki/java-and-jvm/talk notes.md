---
layout: wiki
title: Project Loom Talk notes
last_updated: 2021-03-21
---


Intro

https://horstmann.com/unblog/2019-12-05/

Structured concurrency on the same blog




good introductionn, but bad ending: https://developers.redhat.com/blog/2019/06/19/project-loom-lightweight-java-threads/


Project looom better future
https://www.youtube.com/watch?v=_fFzyY_7UmA&ab_channel=SoftwareMill


good summary: https://blog.softwaremill.com/will-project-loom-obliterate-java-futures-fb1a28508232

What next for concurrent programming on JVM

Foundation futures


começar do exemplo do parallels.... stream


Talk

https://www.youtube.com/watch?v=7GLVROqgQJY&ab_channel=JUG.ru


https://www.youtube.com/watch?v=zuc9JZz9Xbw&t=588s&ab_channel=NYJavaSIG-NYJavaUserGroup


Concurrency x Paralelism

P: one task, make it run faster, (Care about duration/letancy), try to split in multiple sub tasks, and using multiple computing resources

C: many != taks, largeslyu independent and the problem is sovling, managing the multi tasks without giving computer resources, tasks number vs process, scheduling

Performance, important is thorugh put, number of transacions complete per minute


print 1
contexto of exception, é da thread
debugger, step execution a single thread
profile JFR, thread by thread basis

fundantal design java

p2
one implementation 

coompromise pq é pra todos usos ()


p3 p4
code design harmonious with platform, number thing == nubmer threads, os, low
limiting factor 

p3 reuse with thread pools
ao inves de criar, nos temo sum pool e toda vez que uma transcao precisa, nos usamos o reusmo

a thread nao é mapeada com uma single transacion, leak of thread locals, cancellation (interruption) 
as vezes qdo itnerrumpemos, ele já passou pra proxima task

mas ainda nao resolve escalabilidade, pq é o numero de threads do os

thread pode estar esperando alguma coisa processar, qdo tiver esperando, vamos retornar para o pool para ser reusada

normal blocking apis, nao funcionam como assim sync http client, jbdc etc. (precisa uasr apis diferentes)

thread em java define o contexto da operacao, 

p5 desarmonious com a api

p6

p7

rethink threads

p8 threads in java

virtual threads slide

java concurrency, then and now

chart 2kb
esquerda thread normal

como criar virtual threads

slide we are "just"

solved mane problesm, thread locals leaking,m interrepciopns, calcencalion

structured concurrency

in order to learn loom, you don't need to learn anything, mas unlearn
old habits
never acte to pool, just creat string, vao criar milhoes

structure concurrency, way to organize threads

every time splies, with structure concurrencey you nhave to join before cointinu9ing (slide structure concurrency)

slide structured lok at the code, know ehre the control flow run

every task you submit to it, it will create a new thread

cdeadline,

terminate, se terminou com os 30 segundos, se naodrop the threads running



Q&A

Limitations?
jNI blocking io, native monitor (sincronized), blocking IO, will suspende the virtual thread mas suspende a kernel thread (vc deve usar um dos java.concurrenty blocks reentry lock or stamp lock)


green threads x virtual (green schedule single os thread)


thread dump funcionality (stack of 1mi threads)


blocking file/io


Effective Java executors (olhjar no livro), agora tem que usar o virtualthread executor

qdo usar o heavy weight, virtual thread verygood trans. processing i/o executa um pouco e blocka,
mas qdo eu vou fazer uma task grande, inverter uma matrix,  converter um video a lot of processing vc ianda pode querer usar o normal

Control CPUs, default scheduler fork join pool, number of coorls (set by command line flag)
or you can just apply your own scheduler

I/O bound processing applications -> virtual threads (anything that blocks frequently)
CPU bound virtual threads will not help you


Project Loom reasoning: solve the dileme, wasting hardware or harmonious code, wrihte async code performance loom, but get harmonious

syncronized and IO inside the sync block (temporary limitation), replase with reeintranmt/stramp lock



futures 


bulk heading (olhar o que é) SEDA

Comppl, features will work out of the box (you iwll only need get mostly now, becuase most of them are designed to do async programming, because you do a blocking because free
I'm doing this because blocking is ex43pesnei? maybe yo udon't need to do that, maybe something very simple will do
)

Reactive fraemworks

Reactive Streams, 

loom veio pq é mto impopular, 



















======
https://blog.frankel.ch/project-loom-reactive-coroutines/
https://renato.athaydes.com/posts/taking-loom-for-a-spin.html

exemplo pra talk: https://renato.athaydes.com/posts/taking-loom-for-a-spin.html

https://github.com/rahmanusta/project-loom-samples/blob/master/slides/Project%20Loom%20-%20Scalable%20Concurrency%20with%20Virtual%20Java%20Threads.pdf



