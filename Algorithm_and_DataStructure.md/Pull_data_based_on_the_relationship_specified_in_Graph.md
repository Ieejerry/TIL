# Graph에 명시된 관계에 따라 데이터 뽑아오기

</br>

[![2023-05-02-6-43-38.png](https://i.postimg.cc/CLxhFJyb/2023-05-02-6-43-38.png)](https://postimg.cc/NLZqD6j0)

</br>

[![2023-05-02-6-50-11.png](https://i.postimg.cc/26BDqXkK/2023-05-02-6-50-11.png)](https://postimg.cc/cgZj2h8R)

</br>

프로젝트와 프로젝트간 의존도가 주어지면 의존도는 앞에 있는 것이 먼저 실행이 되어야 뒤에 있는 것이 실행될 수 있다. 각 노드와 노드간의 관계를 명시하는 데이터를 표현하는 데에는 그래프의 개념을 사용하는 것이 좋다.

그래프를 자료구조에 저장하는 방법에는 두 가지가 있다. Matrix에 담는 방법과 LinkedList에 담는 방법이 있다. 공간 효율이 좋은 LinkedList에 담아보겠다.

</br>

[![2023-05-02-6-53-40.png](https://i.postimg.cc/mZJP601t/2023-05-02-6-53-40.png)](https://postimg.cc/Rq1CWpRB)

</br>

우선 배열을 선언해서 프로젝트들을 다 담는다. 그리고 각각의 의존도를 LinkedList로 추가해준다. 앞에 있는 프로젝트가 먼저 실행되어야 한다고 했으니, LinkedList에는 해당 프로젝트가 실행되기 전에 먼저 실행되어야 하는 프로젝트들을 나열한다. 

</br>

[![2023-05-02-7-01-36.png](https://i.postimg.cc/cCBfQW09/2023-05-02-7-01-36.png)](https://postimg.cc/7JbCkpC0)

</br>

모든 프로젝트들을 의존성에 입각해서 순서대로 가져와야 한다. 결과를 저장할 프로젝트 갯수만큼의 배열을 하나 만든다. 그리고 배열에 프로젝트를 추가하는 함수를 하나 만든다. 그리고 배열에 맨 처음부터 끝까지 모든 프로젝트를 한번에 돌면서 이 함수를 호출한다. 그런데 이 함수가 호출되면 바로 결과에 프로젝트를 호출하는 것이 아니라 이 프로젝트가 먼저 실행되어야 하는 다른 프로젝트들이 존재하는지를 확인한다. 있으면 먼저 실행되어야 할 프로젝트들을 for문을 돌면서 다시 추가하는 함수를 호출해서 먼저 처리가 되어야 할 프로젝트들을 계속 찾아서 먼저 결과에 출력해준다.

</br>

## 전체 코드

</br>

``` java
package DataStructure;

import java.util.LinkedList;
import java.util.jar.Attributes.Name;
import java.util.HashMap;

class Project {	// 프로젝트 클래스 생성 
	private String name;	// 이름을 저장할 변수 선언 
	private LinkedList<Project> dependencies;	// 먼저 치리되야하는 프로젝트의 리스트를 저장하는 변수를 선언 
	private boolean marked;	// 순서를 정할 때 결과에 담았는지 여부를 알려줄 플래그 선언 
	
	public Project(String name) {	// 생성자에서 이름을 받아서 
		this.name = name;	// 멤버 변수에 넣어주고
		this.marked = false;	// 마킹 플래그는 false로 초기화 
		this.dependencies = new LinkedList<Project>();	// 의존하는 프로젝트의 리스트를 담을 LinkedList 준비 
	}
	
	public void addDependency(Project project) {	// 의존 관계를 추가해주는 함수 
		if(!dependencies.contains(project)) {	// 먼저 처리해줘야 하는 프로젝트를 받아서 LinkedList에 추가 
			dependencies.add(project);
		}
	}
	
	public LinkedList<Project> getDependencies() {	// 멤버 변수들을 private로 선언하였기에 의존하는 프로젝트를 가져오는 함수 
		return this.dependencies;
	}
	
	public String getName() {	// 멤버 변수들을 private로 선언하였기에 프로젝트 이름을 가져오는 함수 
		return this.name;
	}
	
	public void setMarked(boolean marked) {	// 멤버 변수들을 private로 선언하였기에 마킹 플래그를 설정하는 함수 
		this.marked = marked;
	}
	
	public boolean getMarked() {	// 멤버 변수들을 private로 선언하였기에 마킹 플래그를 가져오는 함수 
		return this.marked;
	}
}

class ProjectManager {	// 프로젝트를 관리할 프로젝트 매니저 클래스 정의 
	private HashMap<String, Project> projects;	// 프로젝트를 담을 해쉬맵을 멤버변수로 선언, 배열 대신 해쉬맵을 사용하였는데, 프로젝트 이름으로 검색할 때, 시간을 절약할 수 있을 거 같아서 배열 대신 해쉬맵을 사용 
	
	public ProjectManager(String[] names, String[][] dependencies) {	// 생성자에서 프로젝트 배열과 의존도 이차원 배열을 받음 
		buildProjects(names);	// 이름으로 프로젝트 생성 
		addDependencies(dependencies);	// 의존도를 프로젝트 노드에 추가 
	}
	
	public void buildProjects(String[] names) {	// 프로젝트 만드는 함수 정의 
		projects = new HashMap<String, Project>();	// 해쉬맵으로 객체 생성 
		for(int i = 0; i < names.length; i++) {	// 이름을 돌면서 이름과 프로젝트 객체를 해쉬맵에 저장 
			projects.put(names[i], new Project(names[i]));
		}
	}
	
	public void addDependencies(String[][] dependencies) {	// 의존도를 추가하는 함수 
		for(String[] dependency : dependencies) {	// 의존도를 돌면서 
			Project before = findProject(dependency[0]);	// 앞에 꺼는 먼저 처리해야 될 것 
			Project after = findProject(dependency[1]);	// 뒤에 꺼는 나중에 처리해야 될 것 
			after.addDependency(before);	// 먼저 처리해야 될 것을 노드안에 의존 프로젝트로 저장하기로 했으니까, 나중에 처리되는 노드에 디펜던시로 먼저 처리되어야 할 프로젝트들을 추가 
		}
	}
	
	private int index;
	
	public Project[] buildOrder() {	// 의존성에 입각해서 프로젝트의 순서를 정하는 함수 
		initMarkingFlages();	// 마킹 플래그를 초기화하고, 
		Project[] ordered = new Project[this.projects.size()];	// 결과값을 저장할 배열 생성 
		index = 0;	// 저장할 배열 방 번호는 0번부터 
		for(Project project : this.projects.values()) {	// 프로젝트를 하나씩 돌면서 재귀함수를 호출 
			buildOrder(project, ordered);
		}
		return ordered;	// 함수가 끝나면 결과값으로 저장된 배열을 반환 
	}
	
	public void buildOrder(Project project, Project[] ordered) {	// 호출을 받으면 먼저 처리해야 될 프로젝트가 있는지 확인하고 있으면 for 루프를 돌면서 재귀 호출한다. 
		if(!project.getDependencies().isEmpty()) {
			for(Project p : project.getDependencies()) {
				buildOrder(p, ordered);
			}
		}
		
		if(project.getMarked() == false) {	// 모든 의존하는 프로젝트가 다 처리된 후에는 결과 배열에 추가가 되었는지 확인하고 아직 처리가 안된 프로젝트면 
			project.setMarked(true);	// marking 플래그를 true로 바꾸면서 
			ordered[index] = project;	// 결과값으로 배열에 추가 
			index++;	// 다음 배열방에 담도록 인덱스 하나 추가 
		}
	}
	
	private void initMarkingFlages() {	// 순서를 정하기 전에 마킹 플래그를 false로 세팅해주는 함수 
		for(Project project : this.projects.values()) {
			project.setMarked(false);
		}
	}
	
	public Project findProject(String name) {	// 이름으로 프로젝트 노드를 찾는 함수 
		return projects.get(name);
	}
}

public class GraphTest2 {
	public static void main(String[] args) {
		String[] proejects = { "a", "b", "c", "d", "e", "f", "g" };	// 프로젝트 나열 
		String[][] dependencies = {{"f", "a"}, {"f", "b"}, {"f", "c"}, {"b", "a"}, {"c", "a"}, {"a", "e"}, {"b", "e"}, {"d", "g"}};	// 의존 관계 나열 
		ProjectManager pm = new ProjectManager(proejects, dependencies);	// 생성자에 넘겨주면서 프로젝트 매니저의 객체를 생성 
		Project[] ps = pm.buildOrder();	// 순서를 받아오면 받아서 출력 
		for(Project p : ps) {
			if(p != null) {
				System.out.print(p.getName() + " ");
			}
		}
	}
}
```

```
f b c a d e g
```