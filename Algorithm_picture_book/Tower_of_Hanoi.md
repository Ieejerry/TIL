# 하노이의 탑(Tower of Hanoi)

</br>

[![IMG-2568.jpg](https://i.postimg.cc/ydBVbh7C/IMG-2568.jpg)](https://postimg.cc/f32n3938)

</br>

하노이의 탑은 원반을 이동해서 탑을 쌓는 게임이다. 그림에선 A, B, C 세 개의 막대가 있으며 A 막대에 2개의 원반이 꽃혀있다.

</br>

[![IMG-2569.jpg](https://i.postimg.cc/PrNd95nJ/IMG-2569.jpg)](https://postimg.cc/6yJsGw3x)

</br>

A의 원반을 순서를 유지한 채 C로 이동하는 것이 게임의 목적이다.

</br>

[![IMG-2570.jpg](https://i.postimg.cc/43RZYv7H/IMG-2570.jpg)](https://postimg.cc/DS6RDXc7)

</br>

원반의 이동에는 다음 두 가지 조건이 있다. 첫 번째 조건은, 한 번에 한 개의 원반만 이동할 수 있다는 것이다.

</br>

[![IMG-2571.jpg](https://i.postimg.cc/B6q0gqCq/IMG-2571.jpg)](https://postimg.cc/f3gpWQFF)

</br>

이처럼 한 개를 움직이는 것은 문제가 없지만

</br>

[![IMG-2572.jpg](https://i.postimg.cc/657NzbCG/IMG-2572.jpg)](https://postimg.cc/1fZT3HC9)

</br>

그림처럼 2개를 동시에 움직여서는 안 된다.

</br>

[![IMG-2573.jpg](https://i.postimg.cc/dVrcc7Hs/IMG-2573.jpg)](https://postimg.cc/21kK45NM)

</br>

[![IMG-2574.jpg](https://i.postimg.cc/Fz7wW1kQ/IMG-2574.jpg)](https://postimg.cc/0K1trkCt)

</br>

두 번째 조건은, 작은 원반의 위에 그것보다 큰 원반을 둘 수 없다.

</br>

[![IMG-2575.jpg](https://i.postimg.cc/gkLf3XPV/IMG-2575.jpg)](https://postimg.cc/hfgyBGvv)

</br>

이상의 조건을 바탕으로 실제로 원반을 움직이는 예를 보겠다.

</br>

[![IMG-2576.jpg](https://i.postimg.cc/PJpFbc0X/IMG-2576.jpg)](https://postimg.cc/hQnrcCS6)

</br>

작은 원반이 가장 위에 있으므로 B로 이동할 수 있다.

</br>

[![IMG-2577.jpg](https://i.postimg.cc/PfY7xGby/IMG-2577.jpg)](https://postimg.cc/QVNm4yyK)

</br>

큰 원반을 C로 이동한다.

</br>

[![IMG-2578.jpg](https://i.postimg.cc/vB3c72fN/IMG-2578.jpg)](https://postimg.cc/r0RVMJh1)

</br>

작은 원반을 C로 이동하면 게임이 종료된다. 원반이 두 개인 경우 목표에 도달할 수 있는 것을 확인했다.

</br>

[![IMG-2579.jpg](https://i.postimg.cc/6Qx0FqgN/IMG-2579.jpg)](https://postimg.cc/VJ4nCfz7)

</br>

원반이 세 개인 경우는 어떨까?

</br>

[![IMG-2580.jpg](https://i.postimg.cc/mrhHXs2G/IMG-2580.jpg)](https://postimg.cc/zLZvv4gd)

</br>

가장 큰 원반을 무시하고 나머지 원반을 B로 이동하는 방법을 생각해보겠다.

</br>

[![IMG-2581.jpg](https://i.postimg.cc/QdQ48cpM/IMG-2581.jpg)](https://postimg.cc/hXGbMzZF)

</br>

나머지 원반(가장 큰 원반을 제외한)은 앞서 본 두 개의 원반 이동 방식과 동일한 방식을 사용하면 B로 이동할 수 있다.

</br>

[![IMG-2582.jpg](https://i.postimg.cc/6pfkHkbz/IMG-2582.jpg)](https://postimg.cc/w134MGps)

</br>

여기서 가장 큰 원반을 C로 이동한다.

</br>

[![IMG-2583.jpg](https://i.postimg.cc/W3BYp8fh/IMG-2583.jpg)](https://postimg.cc/PpMQ2WHj)

</br>

앞서 본 것과 동일한 방법으로 B의 두 개를 C로 이동한다. 이동을 완료했다. 원반이 세 개인 경우라도 목표를 달성할 수 있다. 사실은 이 게임은 원반이 몇 장이라도 목표를 달성할 수 있다. 이것을 수학적 귀납법을 사용해서 증명해보겠다.

</br>

[![IMG-2584.jpg](https://i.postimg.cc/66VfGB8H/IMG-2584.jpg)](https://postimg.cc/9zM765tT)

</br>

[![IMG-2585.jpg](https://i.postimg.cc/50BLvm2H/IMG-2585.jpg)](https://postimg.cc/ygNDCc9B)

</br>

원반이 한 개일 때 목표를 달성한다.

</br>

[![IMG-2586.jpg](https://i.postimg.cc/yYQ9FxsT/IMG-2586.jpg)](https://postimg.cc/xcmcQ0kk)

</br>

[![IMG-2587.jpg](https://i.postimg.cc/cC1g3yzj/IMG-2587.jpg)](https://postimg.cc/vgjZRjbL)

</br>

원반이 n개일 때 목표를 달성할 수 있다고 가정한다.

</br>

[![IMG-2588.jpg](https://i.postimg.cc/Vs4b8vrc/IMG-2588.jpg)](https://postimg.cc/fktb7wfH)

</br>

n+1 개를 이동하는 경우를 생각해보겠다.

</br>

[![IMG-2589.jpg](https://i.postimg.cc/fWHkPPpz/IMG-2589.jpg)](https://postimg.cc/6Tv92MBg)

</br>

가장 큰 원반을 무시한다.

</br>

[![IMG-2590.jpg](https://i.postimg.cc/02Fjkw9h/IMG-2590.jpg)](https://postimg.cc/9rPC1zRB)

</br>

가장에 의해 n 개라면 이동할 수 있으므로 n 개를 B로 이동한다.

</br>

[![IMG-2591.jpg](https://i.postimg.cc/KjKbw03j/IMG-2591.jpg)](https://postimg.cc/wRdnscVY)

</br>

가장 큰 원반을 C로 이동한다.

</br>

[![IMG-2592.jpg](https://i.postimg.cc/9XqFxfdp/IMG-2592.jpg)](https://postimg.cc/Bt40b4wL)

</br>

B에 있는 n 개를 C로 이동한다. 이것으로 이동이 완료된다. 수학적 귀납법을 통해 원반이 몇 개이든 목표를 달성할 수 있다는 것이 증명됐다.

하노이의 탑의 해법에 대해 생각해보자. n 개 원반의 하노이 탑 문제는 n-1 개의 하노이 탑을 해결하는 방식을 이용하면 되는 것이다. 이 n-1 개의 하노이 탑을 풀려면 n-2 개의 하노이 탑을 해결하는 방식을 이용하면 된다. 이것을 계속하다 보면 최종적으로 한 개의 원반을 푸는 방법에까지 이른다. 이 재귀적 접근법은 다양한 알고리즘에 사용되고 있으며 재귀적 알고리즘이라고 한다.