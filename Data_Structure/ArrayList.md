# ArrayList

</br>

## 소개

`ArrayList`는 배열을 이용해서 리스트를 구현한 것을 의미한다. 장점은 내부적으로 배열을 이용하기 때문에 인덱스를 이용해서 접근하는 것이 빠르지만 데이터의 추가와 삭제가 느리다.

</br>

## 데이터의 추가

`ArrayList`는 내부적으로 데이터를 배열에 저장한다. 배열의 특성상 데이터를 리스트의 처음이나 중간에 저장하면 이후의 데이터들이 한칸씩 뒤로 물러나야 한다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2886.png)

</br>

## 데이터의 삭제

삭제도 추가와 비슷하다. 빈자리가 생기면 빈자리를 채우기 위해서 순차적으로 한칸씩 땡겨야 한다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2887.png)

</br>

## 데이터를 가져오기

인덱스를 이용해서 데이터를 가져오고 싶을 때 `Array`로 구현한 리스트는 매우 빠르다. 메모리 상의 주소를 정확하게 참조해서 가져오기 때문이다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2842.png)

</br>

배열을 건물에 비유해보겠다. 각각의 엘리먼트는 그 엘리먼트에 대한 인덱스를 가지고 있다. 인덱스를 안다는 것은 주소를 알고 있는 것과 같다. 반면에 인덱스를 모르는 것은 주소를 모르고 집을 찾아가는 것과 같기 때문에 시간이 오래 걸린다. 인덱스만 알고 있다면 `Arraylist`에서 데이터를 가져오는 것은 매우 빠르다.