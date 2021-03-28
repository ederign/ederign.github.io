---
layout: wiki
title: Project Loom
last_updated: 2021-02-09
---
## Talk topics & reminders

Benchmark https://github.com/sormuras/junit5-looming/blob/master/STORY.md
https://twitter.com/sormuras/status/1326793610176684032
https://twitter.com/sormuras/status/1326806829456875521/retweets/with_comments




## Blogs and  wikis
[Open JDK Wiki](https://wiki.openjdk.java.net/display/loom)



https://developerlife.com/2019/12/02/project-loom-experiment/
https://github.com/nazmulidris/loomexample
https://inside.java/2020/08/07/loom-performance/
https://www.reddit.com/r/java/comments/evtxe4/project_loom_new_earlyaccess_build_build/
https://www.javaadvent.com/2020/12/project-loom-and-structured-concurrency.html
https://blogs.oracle.com/javamagazine/going-inside-javas-project-loom-and-virtual-threads
http://cr.openjdk.java.net/~rpressler/loom/loom/sol1_part1.html
https://developers.redhat.com/blog/2019/06/19/project-loom-lightweight-java-threads/


https://github.com/sormuras/junit5-looming


https://i-rant.arnaudbos.com/loom-part-0-rationale/

blocking vs no blocking
https://www.youtube.com/watch?v=v5Z8rOTzM8s&ab_channel=Devoxx

slide com summary: https://youtu.be/v5Z8rOTzM8s?t=869
https://speakerdeck.com/arnaudbos/untangled-sneak-peek-at-project-loom slides
https://archive.jlongster.com/Whats-in-a-Continuation
https://web.archive.org/web/20191122044527/https://blog.paralleluniverse.co/2014/02/04/littles-law/


https://horstmann.com/unblog/2019-12-05/


https://blog.softwaremill.com/will-project-loom-obliterate-java-futures-fb1a28508232


## Talk Summaries

### Prepare for What 'Looms' Ahead

Speaker: Heinz Kabutz [link](https://skillsmatter.com/meetups/13271-prepare-for-what-looms-ahead) https://skillsmatter.com/meetups/13271-prepare-for-what-looms-ahead

sc1

sc2

sc3/4 - best deal search

sc5/6 - search in background

sc7 - CompletableFuture

sc8

sc completed futures

debuging is hard

sc9

What pools did you choose for CPU vs IO? Fixed vs Cached Thread Pool? 

what pool uise for io/cpu bound, fixed for CPU bound, cache is tricky

both are unlimted ppols limited by hardware and not java (Fixed thread pool), fixed by thread number, but unlimted pool (2bi level)

reality fixed thread pool get a limite because after too many connections queeus is too long, nothing to do, unlimited queue but can still wait too long

(Task wrapped in completad futues) , cached thread pool has no queue, if new job comes makes a new thread, thread numbers will evententu run out, limited by hardwarres and not java

sc10

sc11

Carrier = OS Thread? Or different identity?

A carrier thread is a normal java thread, backed by a native thread, (limited by hardware threads)

sc12

sc13

The second execeutor service you can't use the same one, otherwhite the join is not work correctly (slide structure concurrency)

sc14

maged blopcker slides, on previous you need to specificy a thread, if you block managed way the fork can construi more thread to keep the paralelmis at your desired level.

as thread gest blocket, fork join poll wil craete more threds up to some limite

(manager blocker uses in jdk, phaser, completable etc.)

slide20

s21

s22

affects  a lto of other parts

s23

syncronized not fully completed with loom

the code blocked all the carrier threads (wait method) that is why there is no output)

current version hardwar thread x 16

If you are working with loom, dont use syncronized wait, 


sc23

they ar echeting a beat, they havent'solve the problem of how to managed syncronized and wait, they just patched over the bitch alying to make more threads if that happens


sc24

sc25

reentrantlock back to syncronized due to performance issues

(syncronized are performed work in both way)

sycnronized if you don't need it, no big penalties

sc26

Virtual threads threadlocal, try to move it away as much as you can

sc27

sc28, 29

What is JPS? histogram? sockeclimitscharter on cli

You don't need to have unblocking IO with virtual threads

sc30,31

half kb per thread

How long does it take to just create these millions of threads? So basically: How long did it take to startup the service?

vthreads are fast, sockets are slow


Tooling he is not sure, java flight recorder, compatibable, 



#### Random notes

Concurrenty in practice book

Research Concurrency Price
