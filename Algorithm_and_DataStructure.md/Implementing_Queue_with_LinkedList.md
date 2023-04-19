# LinkedList로 Queue구현하기

</br>

[![2023-04-18-8-55-16.png](https://i.postimg.cc/PJncRb8k/2023-04-18-8-55-16.png)](https://postimg.cc/xJgtkzRs)

</br>

[![2023-04-18-8-55-57.png](https://i.postimg.cc/Lsf30ckn/2023-04-18-8-55-57.png)](https://postimg.cc/HJYMrPhg)

</br>

[![2023-04-18-8-56-52.png](https://i.postimg.cc/9ftq9Ctt/2023-04-18-8-56-52.png)](https://postimg.cc/DW0ZkVN8)

</br>

가장 먼저 들어온 동물이 가장 먼저 분양이 되어야 한다. 분양받는 사람이 동물의 종류를 고를 수 있는데, 개와 고양이가 같은 Queue에 있다면, 그 Queue 전체를 검색해야 한다. 그래서 개 Queue와 고양이 Queue 따로 분리한다. 분양 받는 사람이 아무 동물의 종류나 상관없다고 할 때는 두 Queue중 먼저 들어온 동물을 분양해주면 되고, 고양이를 분양 받고 싶다고 하면 고양이 Queue에서 먼저 들어온 고양이를, 개를 분양하고 싶다면 개 Queue에서 먼저 들어온 개를 분양해주면 된다.

</br>

## 전체 코드

``` java
package DataStructure;

import java.util.LinkedList;

enum AnimalType {
	DOG, CAT
}

abstract class Animal {
	AnimalType type;
	String name;
	int order;
	
	Animal(AnimalType type, String name) {
		this.type = type;
		this.name = name;
	}
	
	void setOrder(int order) {
		this.order = order;
	}
	
	int getOrder() {
		return order;
	}
	
	String info() {
		return order + ") type: " + type + ", name: " + name;
	}
}

class Dog extends Animal {
	Dog(String name) {
		super(AnimalType.DOG, name);
	}
}

class Cat extends Animal {
	Cat(String name) {
		super(AnimalType.CAT, name);
	}
}

class AnimalShelter {
	LinkedList<Dog> dogs = new LinkedList<>();
	LinkedList<Cat> cats = new LinkedList<>();
	int order;
	
	AnimalShelter() {
		order = 1;
	}
	
	void enqueue(Animal animal) {
		animal.setOrder(order);
		order++;
		if(animal.type == AnimalType.DOG) {
			dogs.addLast((Dog)animal);
		} else if(animal.type == AnimalType.CAT) {
			cats.addLast((Cat)animal);
		}
	}
	
	Animal dequeueDog() {
		return dogs.poll();
	}
	
	Animal dequeueCat() {
		return cats.poll();
	}
	
	Animal dequeue() {
		if(dogs.size() == 0 && cats.size() == 0) {
			return null;
		} else if(dogs.size() == 0) {
			return cats.poll();
		} else if(cats.size() == 0) {
			return dogs.poll();
		}
		
		Animal dog = dogs.peek();
		Animal cat = cats.peek();
		
		if(cat.order < dog.order) {
			return cats.poll();
		} else {
			return dogs.poll();
		}
	}
}

public class Implementing_Queue_with_LinkedList {
	public static void main(String[] args) {
		Dog d1 = new Dog("puppy");
		Dog d2 = new Dog("chichi");
		Dog d3 = new Dog("choco");
		Cat c1 = new Cat("shasha");
		Cat c2 = new Cat("miumiu");
		Cat c3 = new Cat("gaga");
		
		AnimalShelter as = new AnimalShelter();
		as.enqueue(d1);
		as.enqueue(c1);
		as.enqueue(d2);
		as.enqueue(c2);
		as.enqueue(d3);
		as.enqueue(c3);
		
		System.out.println(as.dequeueCat().info());
		System.out.println(as.dequeueDog().info());
		System.out.println(as.dequeue().info());
		System.out.println(as.dequeue().info());
		System.out.println(as.dequeue().info());
		System.out.println(as.dequeue().info());
	}
}
```