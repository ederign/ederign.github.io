---
layout: wiki
title: Federated Modules 
last_updated: 2021-03-09
---

### Talk  Webpack 5 Module Federation 

Abstract

For years, we have never been able to consume or share modules from another standalone application. The nearest we had was externals or DLL Plugin. Both of which are not scalable or sustainable in large scale systems. For those who have built a micro frontend stack, likely understand the challenges. Introducing Module Federation, a feature that I bought for Webpack 5. It allows us to import code just like you would within a monolith. No overhead, no learning curves, and no real deviation from standard engineering practices. We have built a universal system for developers to consume modules of other applications at runtime. Be it server or client. This architecture has been considered a game-changer to Javascript and will change how we build applications in the future. 


Zack Jackson
[link] https://www.youtube.com/watch?v=-ei6RqZilYI

Sharing code is hard (and gets harder at scale)
- Incovinient;
- NPM is slow;
- Grows in complexity;
- Sharing is usually primitive;
- Inneficient and unproductive to share feature code;

Motivation
- Mid to large scale platforms;
- Deploy multiple apps, or parts of an app independetly;
- Multiple teams, autonomous workflows;
- Avoid learning curves
- Avoid multiple copies of the same library;
- Sahre vendor code, stay flexible;
- NO UX drawbacks, like page reloads in user flow;
- Avoid complicated CI.

Context slide (print)


gif  https://p192.p3.n0.cdn.getcloudapp.com/items/xQunmG16/1d7c9c20-bebd-4a05-bb1e-e5475060b64a.gif?v=51287dc326286787e6ea28db91c11846

Import modules from a separted compiled app

Share cmopiled apps from other sources

Current solutions are brittle, hard to rollout on shared deps updateds; UX if often impacted (download more javascript, page refresh etc.)
lots of code duplication, in house solutions are complexes, requires manual labor, SSR is a nightmare

slide existing options

single build

externals

Native ESM is bad on for web performance
Single build is bad on build performance
DLL plugin/externals is too much manual work

what we4 look is:
good performance slide


work in browser and in node.js

host slide
remote
bi directional hosts
omnidirectional hosts
hability: I can use semantic versioning and I can have a patch version os react, the runtimes negociate bweten each other before run (to find best version of react)

what is module federation slide

not a framework

what is slide

an example
team b's perspective

Container ref. plugin

dote lines are async , but can be 'used' as a sync

container ref. slide

container orange balls

container is what other teams exposes to you

container plugin

share scope is how they share modules/deps, you can have multiple 
shared scope (if you want to keep the scope separed, like != versions of react)


creating a container slide

react lazy how to use

example at scale


supporting multiple react versions

basic modern react repo


applied architecture

what could you federate?

? react.lazy? react.suspense


decentralized routing, 


non webpack compability

federation dashboard for Saas

