# 페이지 랭크(PageRank)

</br>

[![IMG-2512.jpg](https://i.postimg.cc/x8m280QF/IMG-2512.jpg)](https://postimg.cc/ctdj5GrQ)

</br>

검색 사이트에서 검색 결과의 순위를 결정하기 위해 사용되는 알고리즘이다. 구글이 이 알고리즘을 검색 엔진에 적용해서 세계적인 기업이 될 수 있었다. 이전 검색 사이트에선 검색 키워드와 페이지 내 문장의 관령성을 중심으로 검색 결과의 순위를 결정했었다. 이 방법에선 페이지 내에 유익한 정보가 포함돼 있는지는 고려되고 있지 않는다. 이 때문에 검색 결과의 정확도가 높다고 볼 수 없었다. 페이지랭크는 페이지 간의 링크 구조로부터 페이지의 가치를 산출하는 알고리즘이다. 산출까지의 구체적인 과정을 보도록 하겠다.

</br>

[![IMG-2513.jpg](https://i.postimg.cc/Z5tqrMDd/IMG-2513.jpg)](https://postimg.cc/Wh8jVXVN)

</br>

사각형이 웹페이지고 화살표가 페이지 간 링크를 나타낸다. 다음 그림에선 아래 세 개의 페이지가 하나의 페이지를 링크하고 있는 것을 보여주고 있다. 페이지랭크에선 링크된 수가 많을수록 중요한 페이지라고 판단한다.

</br>

[![IMG-2514.jpg](https://i.postimg.cc/Qx57G52c/IMG-2514.jpg)](https://postimg.cc/F7rz0fsK)

</br>

이 그림에선 상위에 있는 페이지가 가장 중요한 페이지라고 판단한다.

</br>

[![IMG-2513.jpg](https://i.postimg.cc/Z5tqrMDd/IMG-2513.jpg)](https://postimg.cc/Wh8jVXVN)

</br>

실제로는 각 페이지의 중요도가 계산에 의해 수치화된다. 기본적인 계산 방법을 보도록 하겠다.

</br>

[![IMG-2516.jpg](https://i.postimg.cc/0NL6ByVV/IMG-2516.jpg)](https://postimg.cc/wtQTtg8N)

</br>

링크되지 않은 페이지의 점수를 1이라고 한다.

</br>

[![IMG-2517.jpg](https://i.postimg.cc/RZYqW0xv/IMG-2517.jpg)](https://postimg.cc/RWcv840Y)

</br>

링크돼 있는 페이지의 점수는 링크를 하고 있는 페이지의 점수를 합한 것이 된다.

</br>

[![IMG-2518.jpg](https://i.postimg.cc/MKKGtBWW/IMG-2518.jpg)](https://postimg.cc/G9VrmH8N)

</br>

단, 링크가 여러 페이지로 나누어 지는 경우는

</br>

[![IMG-2519.jpg](https://i.postimg.cc/nVdxFPJJ/IMG-2519.jpg)](https://postimg.cc/8sr9wwcK)

</br>

링크 점수를 균등하게 배분한다.

</br>

[![IMG-2520.jpg](https://i.postimg.cc/6pr138vv/IMG-2520.jpg)](https://postimg.cc/zyfk2Xpz)

</br>

페이지랭크에선 링크를 모으고 있는 페이지로부터 링크되는 경우 큰 가치를 지닌다.

</br>

[![IMG-2521.jpg](https://i.postimg.cc/vBcJcQMw/IMG-2521.jpg)](https://postimg.cc/ZBz7QzCw)

</br>

그림의 가운데 페에지는 세 개의 독립된 페이지로부터 링크되므로 점수가 3이 된다.

</br>

[![IMG-2522.jpg](https://i.postimg.cc/zX1Q1wLr/IMG-2522.jpg)](https://postimg.cc/V5DgqCBG)

</br>

최상단에 있는 페이지는 점수가 3인 페이지가 링크하고 있어서 큰 점수를 부여받는다. 이 그림에 있는 6개의 페이지에선 가장 상단에 있는 페이지가 가장 중요한 페이지로 인식된다.

이상이 페이지랭크의 기본적인 개념이다.

</br>

[![IMG-2523.jpg](https://i.postimg.cc/t4JN07zb/IMG-2523.jpg)](https://postimg.cc/ZWkdpbgs)

</br>

이 방법에선 링크가 원형을 이루는 경우 문제가 발생한다.

</br>

[![IMG-2524.jpg](https://i.postimg.cc/2jxQVncm/IMG-2524.jpg)](https://postimg.cc/7bfGRJrQ)

</br>

[![IMG-2525.jpg](https://i.postimg.cc/Twfy64Xb/IMG-2525.jpg)](https://postimg.cc/qtDBcQqB)

</br>

[![IMG-2526.jpg](https://i.postimg.cc/SN2xwhz5/IMG-2526.jpg)](https://postimg.cc/vcyyVChL)

</br>

[![IMG-2527.jpg](https://i.postimg.cc/qRvkQVT1/IMG-2527.jpg)](https://postimg.cc/67FJ5PTZ)

</br>

각 페이지의 점수를 순서대로 계산하다 보면

</br>

[![IMG-2528.jpg](https://i.postimg.cc/Mp0qSKZs/IMG-2528.jpg)](https://postimg.cc/3kwPjhvp)

</br>

이처럼 무한 루프가 돼서 루프 내의 페이지 점수가 계산 증가되게 된다. 루프 문제는 '랜덤 서퍼모델(Random Surfer Model)'이라는 계산 방법으로 해결할 수 있다.

</br>

[![IMG-2529.jpg](https://i.postimg.cc/gkHG922g/IMG-2529.jpg)](https://postimg.cc/rKsBxcW4)

</br>

인터넷 서핑을 하는 사용자가 어떤 식으로 페이지를 열람하는지 생각해보자. 우연히 본 잡지에 재미있는 사이트가 소개돼서 접속하려고 한다.

</br>

[![IMG-2530.jpg](https://i.postimg.cc/tg0khphH/IMG-2530.jpg)](https://postimg.cc/QFbcDL46)

</br>

링크를 따라 다른 페이지로 이동한다.

</br>

[![IMG-2531.jpg](https://i.postimg.cc/cJN7vTSx/IMG-2531.jpg)](https://postimg.cc/gxNL5VjQ)

</br>

몇 개의 페이지를 방문하다 재미가 없어지면

</br>

[![IMG-2532.jpg](https://i.postimg.cc/8kqb8T0f/IMG-2532.jpg)](https://postimg.cc/c6B3wGZd)

</br>

일단 서핑을 중단한다.

</br>

[![IMG-2533.jpg](https://i.postimg.cc/HLBJTtWP/IMG-2533.jpg)](https://postimg.cc/jWnqXP7z)

</br>

그리고 며칠 후, 이번에는 친구가 추천해준 다른 페이지를 통해 인터넷 서핑을 시작한다.

</br>

[![IMG-2534.jpg](https://i.postimg.cc/wMd3V4wM/IMG-2534.jpg)](https://postimg.cc/5Ynx9gdW)

</br>

여기서도 링크를 따라서 다른 페이지로 이동하며

</br>

[![IMG-2535.jpg](https://i.postimg.cc/Y9xB5Xph/IMG-2535.jpg)](https://postimg.cc/62TPRf4X)

</br>

재미가 없어지면 서핑을 중단한다. 이와 같이 어떤 페이지에서 열람을 시작해서 몇페이지 이동한 후 종료하는 동작이 반복된다. 인터넷 공간으로 시점을 옮겨서 이 동작을 보도록 하겠다. 페이지들을 정해진 횟수 없이 이동한 후에 전혀 다른 페이지로 순간이동하는 것을 반복하는 것처럼 보인다.

</br>

[![IMG-2536.jpg](https://i.postimg.cc/c4y5R7Zz/IMG-2536.jpg)](https://postimg.cc/G9KQry4P)

</br>

인터넷 서핑을 하는 사람의 동작을 정의하면 다음과 같이 된다.

</br>

[![IMG-2537.jpg](https://i.postimg.cc/ZnhFdc3F/IMG-2537.jpg)](https://postimg.cc/34nvM2td)

</br>

확률 1-a로 지금 있는 페이지의 링크 중 하나를 선택한다.

</br>

[![IMG-2538.jpg](https://i.postimg.cc/dt5rsvW9/IMG-2538.jpg)](https://postimg.cc/nCQCT8fs)

</br>

확률 a로 다른 페이지로 순간이동한다.

</br>

[![IMG-2539.jpg](https://i.postimg.cc/Gtq8mJjp/IMG-2539.jpg)](https://postimg.cc/T55YkbF8)

</br>

순간이동하는 확률인 a를 여기선 15%라고 하겠다. 이 정의에 따라서 페이지 간 전이를 시뮬레이션 해보겠다.

</br>

[![IMG-2540.jpg](https://i.postimg.cc/HxWTkGvQ/IMG-2540.jpg)](https://postimg.cc/LqWcxWpX)

</br>

앞에서 본 것처럼 링크가 루프(원형) 상태인 경우를 생각해보겠다. 각 페이지상의 숫자는 인터넷 서핑을 한 사람이 페이지를 방문한 수를 나타낸다. 현재는 시뮬ㄹ이션 전이므로 모든 숫자가 0이다.

</br>

[![IMG-2541.jpg](https://i.postimg.cc/HLRFFqDY/IMG-2541.jpg)](https://postimg.cc/xkGszF1h)

</br>

[![IMG-2542.jpg](https://i.postimg.cc/3Jf1LgH7/IMG-2542.jpg)](https://postimg.cc/SJ8cRYst)

</br>

[![IMG-2543.jpg](https://i.postimg.cc/QdrCZzDq/IMG-2543.jpg)](https://postimg.cc/RNX4cXN3)

</br>

[![IMG-2544.jpg](https://i.postimg.cc/ncXSfd2M/IMG-2544.jpg)](https://postimg.cc/3dHFgFPH)

</br>

[![IMG-2545.jpg](https://i.postimg.cc/rF4G97gG/IMG-2545.jpg)](https://postimg.cc/w76sqfC3)

</br>

[![IMG-2546.jpg](https://i.postimg.cc/vHntBNNK/IMG-2546.jpg)](https://postimg.cc/zVJg205w)

</br>

정의에 따라서 시뮬레이션을 하면 페이지당 방문 횟수의 차가 나온다.

시간의 흐름을 빠르게 해보곘다.

</br>

[![IMG-2547.jpg](https://i.postimg.cc/3xCjjD7C/IMG-2547.jpg)](https://postimg.cc/NKFrBFK5)

</br>

페이지의 방문 횟수가 합계 1000회에 도달할 때까지 시뮬레이션을 계속한 결과 위와 같은 결과가 됐다.

</br>

[![IMG-2548.jpg](https://i.postimg.cc/KcknqWxY/IMG-2548.jpg)](https://postimg.cc/t7bZ7210)

</br>

이것을 비율로 바꾸면 이와 같이 된다. 해시 테이블에는 몇 가지 종류가 있으며 리스트를 이용하는 방법을 '연쇄법'이라고 한다. 이 값은 '특정 시점에 해당 페이지를 열람할 확률'을 나타낸다고 볼 수 있다. 이 기법이라면 링크가 루프 상태여도 점수를 계산할 수 있다. 실제로는 시뮬레이션을 하는 것이 아니라 더 효율적인 계산 방식을 사용한다. 이 방식을 보도록 하겠다.

</br>

[![IMG-2549.jpg](https://i.postimg.cc/MKnrY5r0/IMG-2549.jpg)](https://postimg.cc/kBdcJQCD)

</br>

그림처럼 복잡한 링크 구조에서 각 페이지의 점수를 계산해보겠다. 먼저 각 페이지의 초기 점수를 설정한다.

</br>

[![IMG-2550.jpg](https://i.postimg.cc/d0jW0xLF/IMG-2550.jpg)](https://postimg.cc/WDtmWSGY)

</br>

점수는 전체의 합이 1이 되도록 균등하게 분배한다. 다음은 인터넷 서핑을 하는 사람이 1회 이동했을 때에 각 페이지에 있을 확률을 구한다. 참고로 n회 이동했을 때에 A에 있을 확률을 PAn이라고 표시한다.

</br>

[![IMG-2551.jpg](https://i.postimg.cc/8cJBLKPj/IMG-2551.jpg)](https://postimg.cc/YL7WHxFH)

</br>

예로 1회 이동한 후에 A에 있을 확률(PA1)을 구해보겠다.

</br>

[![IMG-2552.jpg](https://i.postimg.cc/h4z5LMYL/IMG-2552.jpg)](https://postimg.cc/MXw5x0qH)

</br>

이동해서 A에 있을 경우는 C에 있는 사람이 순간이동을 하지 않고

</br>

[![IMG-2523.jpg](https://i.postimg.cc/t4JN07zb/IMG-2523.jpg)](https://postimg.cc/ZWkdpbgs)

</br>

목적지를 B가 아닌 A를 선택한 경우이다. 초기 상태(0회째 이동 시점)에 C에 사람이 있을 확률은 PC0(=0.25)이다. 또한, C에 있는 사람이 이동을 선택할 확률은 1-a로, A/B에서 A를 선택할 확률은 0.5이다. 따라서 C에서 A로 이동할 확률은 PC0x(1-a)x0.5가 된다.

</br>

[![IMG-2554.jpg](https://i.postimg.cc/9MFjXTXx/IMG-2554.jpg)](https://postimg.cc/Lq7WNJ1f)

</br>

이동해서 A에 있을 경우가 한가지 더 있다. A~D페이지 중 한 페이지에 있는 사람이 순간이동을 하기로 하고

</br>

[![IMG-2555.jpg](https://i.postimg.cc/XYz2BCgH/IMG-2555.jpg)](https://postimg.cc/w1D5S3ZL)

</br>

순간이동 목적지로 A를 선택하는 경우이다. A~D 페이지 중 한 페이지에 있는 사람이 순간이동을 선택할 확률은 a이다. 또한, 순간이동 목적지로 A를 선택할 확률은 0.25이다. 따라서 A로 순간이동으로 이동할 확률은 a x 0.25가 된다.

</br>

[![IMG-2556.jpg](https://i.postimg.cc/Hx2vxPv5/IMG-2556.jpg)](https://postimg.cc/N9KkCbcf)

</br>

이상으로부터 1회 이동한 후에 A에 있을 확률은 PA1 = PC0 x (1-a) x 0.5 + a x 0.25가 된다.

</br>

[![IMG-2557.jpg](https://i.postimg.cc/1tbxPd8H/IMG-2557.jpg)](https://postimg.cc/S2L1fD72)

</br>

PC0 = 0.25, a = 0.15를 대입해서 계산하면 PA1 = 0.14375가 된다.

</br>

[![IMG-2558.jpg](https://i.postimg.cc/1RTR5Wkb/IMG-2558.jpg)](https://postimg.cc/5jBWsmNm)

</br>

마찬가지로 B, C, D 페이지에 있을 확률도 계산해서 값을 변경한다.

</br>

[![IMG-2559.jpg](https://i.postimg.cc/x18WJYLR/IMG-2559.jpg)](https://postimg.cc/YvcXZ5nG)

</br>

결과는 그림과 같다. 다음은 인터넷 서핑을 하는 사람이 2회 이동했을 때에 각 페이지에 있을 확률을 동일한 방법으로 구한다.

</br>

[![IMG-2560.jpg](https://i.postimg.cc/Fs3xT6N4/IMG-2560.jpg)](https://postimg.cc/XpNFJQrH)

</br>

결과는 다음과 같다. 동일한 계산을 반복한다. 그러면 각 페이지에 있을 확률이 수렴하게 된다.

</br>

[![IMG-2561.jpg](https://i.postimg.cc/7L60rt8b/IMG-2561.jpg)](https://postimg.cc/zysVnjf1)

</br>

수렴한 단계에서 계산을 종료한다. 이렇게 구한 값을 각 페이지의 점수로 설정한다.

</br>

[![IMG-2562.jpg](https://i.postimg.cc/yYHR884M/IMG-2562.jpg)](https://postimg.cc/Lhx5yRsD)

</br>

마지막으로 페이지랭크 값이 처음 설명한 링크의 가중치 계산과 일치하는지 확인한다. 그림의 링크 구조에서 앞의 계산 방법을 사용해서 점수를 계산해보겠다.

</br>

[![IMG-2563.jpg](https://i.postimg.cc/pVD94Mhq/IMG-2563.jpg)](https://postimg.cc/pyLX57BF)

</br>

각 값을 반올림하고 있으므로 전체를 더해도 1이 되지 않지만, 비슷한 비율이 되는 것을 알 수 있따.

</br>

[![IMG-2564.jpg](https://i.postimg.cc/pdzxrRtS/IMG-2564.jpg)](https://postimg.cc/06khHgjG)

</br>

이 링크 구조에서도 점수를 계산해보겠다.

</br>

[![IMG-2565.jpg](https://i.postimg.cc/h4yFSfdj/IMG-2565.jpg)](https://postimg.cc/hhdZs4MW)

</br>

여기서도 앞의 결과와 비슷한 비율이 되는 것을 알 수 있다. 이처럼 링크의 가중치를 방문할 확률로 대체해서 계산하는 것이 페이지랭크이다.

</br>

[![IMG-2566.jpg](https://i.postimg.cc/T2L83TqJ/IMG-2566.jpg)](https://postimg.cc/XXb12SPr)

</br>

실제로 구글의 검색 순위는 페이지랭크만 사용하는 것은 아니다. 하지만, 링크 구조로부터 페이지의 가치를 산출한다는 발상과 링크가 루프 상태인 경우에도 계산할 수 있다는 점에서 페이지랭크라는 알고리즘이 획기적이었다는 사실에는 변함이 없다.