---
title: rdtsc를 이용하여 코드 실행 시간 측정하기
author: dinggul
date: 2020-08-12 23:30:00 +0900
categories: [Tech, System Programming]
toc: true
---

Intel 환경에서 실험을 하다보면 `rdtsc` 명령어를 사용하여 코드가 실행하는데에
걸리는 시간을 재는 경우가 종종 있다.

## `rdtsc`
> Loads the current value of the processor's time-stamp counter into the
> EDX:EAX registers. [^c9x-link]



## Reference
- [^c9x-link]: <https://c9x.me/x86/html/file_module_x86_id_278.html>
