# 깊이 우선 탐색(Depth first search)

</br>

<a href="https://ibb.co/Jz2D0K4"><img src="https://i.ibb.co/SK0FWP8/IMG-1909.jpg" alt="IMG-1909" border="0"></a>

</br>

깊이 우선 탐색은 그래프를 탐색하는 알고리즘이다.

</br>

<a href="https://ibb.co/0qtHwXn"><img src="https://i.ibb.co/XX8cw4W/IMG-1910.jpg" alt="IMG-1910" border="0"></a>

</br>

A를 시작점, G를 목표로 해서 탐색을 시작한다.

</br>

<a href="https://ibb.co/g4Xk8Md"><img src="https://i.ibb.co/fDKjWY9/IMG-1911.jpg" alt="IMG-1911" border="0"></a>

</br>

A에서 도달할 수 있는 정점은 B, C, D 이므로 다음 후보로 표시한다.

</br>

<<a href="https://ibb.co/LCkS3B2"><img src="https://i.ibb.co/GVx7qGb/IMG-1912.jpg" alt="IMG-1912" border="0"></a>

</br>

후보 중에서 하나의 정점을 선택한다. 선택 기준은 후보 중 가장 최근에(가장 늦게) 추가된 것이다. 동일 시점에 후보가 된 정점은 어느 것을 선택하든 상관 없다. 여기선 왼쪽에 있는 정점을 선택하도록 한다.

</br>

<a href="https://ibb.co/f9vJbHG"><img src="https://i.ibb.co/Qkd0ZMj/IMG-1914.jpg" alt="IMG-1914" border="0"></a>

</br>

모두 동일한 시점에 후보가 됐으므로 B를 선택한다. 선택한 정점으로 이동한다.

</br>

<a href="https://ibb.co/DLVrCn5"><img src="https://i.ibb.co/b7WbBnz/IMG-1915.jpg" alt="IMG-1915" border="0"></a>

</br>

현재 있는 B로부터 도달할 수 있는 E와 F를 새로운 후보로 추가한다. 후보인 정점은 '후입선출(LIFO)' 구조로 관리하므로 '스택' 데이터 구조를 이용할 수 있다.

</br>

<a href="https://ibb.co/gP8fdBq"><img src="https://i.ibb.co/JyTGqM6/IMG-1916.jpg" alt="IMG-1916" border="0"></a>

</br>

후보 중 가장 최근에 추가된 것은 E와 F이다. 이 중에서 왼쪽에 있는 E를 선택한다.

</br>

<a href="https://ibb.co/44fmkFt"><img src="https://i.ibb.co/wpL0tdg/IMG-1917.jpg" alt="IMG-1917" border="0"></a>

</br>

선택한 정점으로 이동한다.

</br>

<a href="https://ibb.co/YP22C6Y"><img src="https://i.ibb.co/S5NNj2W/IMG-1918.jpg" alt="IMG-1918" border="0"></a>

</br>

현재 있는 E에서 도달할 수 있는 K를 새로운 후보로 추가한다.

</br>

<a href="https://ibb.co/d5RqBP6"><img src="https://i.ibb.co/yQr1065/IMG-1919.jpg" alt="IMG-1919" border="0"></a>

</br>

동일한 작업을 목표에 도달하거나 모든 정점의 탐색이 끝날 때까지 반복한다.

</br>

<a href="https://ibb.co/87jpCwB"><img src="https://i.ibb.co/MCR4vHh/IMG-1920.jpg" alt="IMG-1920" border="0"></a>

</br>

<a href="https://ibb.co/xGZ8QgJ"><img src="https://i.ibb.co/4MkgxSP/IMG-1921.jpg" alt="IMG-1921" border="0"></a>

</br>

<a href="https://ibb.co/xm46xt9"><img src="https://i.ibb.co/bHfXcMw/IMG-1922.jpg" alt="IMG-1922" border="0"></a>

</br>

<a href="https://ibb.co/1KskRV5"><img src="https://i.ibb.co/4MsH4yG/IMG-1923.jpg" alt="IMG-1923" border="0"></a>

</br>

<a href="https://ibb.co/99Cskjr"><img src="https://i.ibb.co/Lz2nXfZ/IMG-1924.jpg" alt="IMG-1924" border="0"></a>

</br>

<a href="https://ibb.co/3kZJj5K"><img src="https://i.ibb.co/Ybsr14g/IMG-1925.jpg" alt="IMG-1925" border="0"></a>

</br>

<a href="https://ibb.co/RvDbVZP"><img src="https://i.ibb.co/7Y1C68V/IMG-1926.jpg" alt="IMG-1926" border="0"></a>

</br>

<a href="https://ibb.co/tZjHF8f"><img src="https://i.ibb.co/q0qDVkG/IMG-1928.jpg" alt="IMG-1928" border="0"></a>

</br>

<a href="https://ibb.co/MP1VC25"><img src="https://i.ibb.co/44STVmg/IMG-1929.jpg" alt="IMG-1929" border="0"></a>

</br>

<a href="https://ibb.co/Tk8nWhN"><img src="https://i.ibb.co/hyWnY8T/IMG-1930.jpg" alt="IMG-1930" border="0"></a>

</br>

<a href="https://ibb.co/JjFsx9y"><img src="https://i.ibb.co/KxzrNJL/IMG-1931.jpg" alt="IMG-1931" border="0"></a>

</br>

<a href="https://ibb.co/jJQ7XfW"><img src="https://i.ibb.co/fDymwFn/IMG-1932.jpg" alt="IMG-1932" border="0"></a>

</br>

<a href="https://ibb.co/mBwgMTj"><img src="https://i.ibb.co/8BptSsC/IMG-1933.jpg" alt="IMG-1933" border="0"></a>

</br>

<a href="https://ibb.co/f1T86Dg"><img src="https://i.ibb.co/SsZQYfj/IMG-1934.jpg" alt="IMG-1934" border="0"></a>

</br>

목표로에 도착했음으로 탐색을 종료한다. 이와 같이 깊이 우선 탐색은 하나의 길을 깊이 있게(수직으로) 찾아가는 방식이다.