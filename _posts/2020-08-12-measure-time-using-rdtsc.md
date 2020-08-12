---
title: rdtsc를 이용하여 코드 실행 시간 측정하기
author: dinggul
date: 2020-08-12 23:30:00 +0900
categories: [Tech, System Programming]
toc: true
---

Intel 환경에서 실험을 하다보면 `rdtsc` 명령어를 사용하여 코드가 실행하는데에
걸리는 시간을 재는 경우가 종종 있다.

## RDTSC
> Loads the current value of the processor's time-stamp counter into the
> EDX:EAX registers. [^c9x-link]

여기서 말하는 타임스탬프 카운터는 CPU tick이 1 증가할 때마다 1 증가하는 값이다.
따라서 원하는 구간의 시작과 끝에 이 명령어를 사용하여 타임스탬프 값을 각각
구한 후, 차이를 내면 해당 구간이 실행되는 동안의 시간을 구할 수 있다. (이 과정에
변수가 존재하는데, 이는 후술하겠다) 보통 다음과 유사한 코드를 이용한다.
[^ex-code]

```C
static __inline__ unsigned long long rdtsc(void)
{
    unsigned hi, lo;
    __asm__ __volatile__ ("rdtsc" : "=a"(lo), "=d"(hi));
    return ( (unsigned long long)lo)|( ((unsigned long long)hi)<<32 );
}
```

단순히 rdtsc 값을 가져오는 방식인데, 측정하고 싶은 범위가 넓든 짧든 동일하게
위와 같이 시간 측정을 해왔었다. 그런데 최근 연구를 진행하던 도중 이렇게 시간을
측정하면 몇 가지 변수가 존재할 수 있음을 알게 되었다.



## Reference
[^c9x-link]: <https://c9x.me/x86/html/file_module_x86_id_278.html>
[^ex-code]: <https://www.mcs.anl.gov/~kazutomo/rdtsc.html>
