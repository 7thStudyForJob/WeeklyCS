## Binary Search Tree(이진 검색 트리)

- 이진 검색 트리의 조건

  - 왼쪽 자식이 있다면, 왼쪽 자식의 key 값보다 자신의 key 값이 커야 한다.
  - 오른쪽 자식이 있다면, 오른쪽 자식의 key 값보다 자신의 key 값이 작아야 한다.

- 특징

  - 중위 순회를 하면 방문하는 순서에 따라 노드 값이 반드시 증가함.
  - 탐색에 용이함
    - 루트 > n 이면 왼쪽 서브트리, 루트 < n 이면 오른쪽 서브트리에서 탐색하면 됌.
    - 배열로 구성된 Binary Tree는 노드의 개수가 n 개이고 root가 0이 아닌 1에서 시작할 때, i 번째 노드에 대해서 parent(i) = i/2 , left_child(i) = 2i , right_child(i) = 2i + 1 의 index 값을 갖음.
  - 트리가 완전 이진트리에 가깝게, 모든 리프 노드의 깊이 차가 1 정돠지만 나는 균형 잡힌 형태라면 한 번의 이진 탐색에 걸리는 트리 크기가(정점 개수 N일때) 평균 O(logN) 소요됌.

- 종류

  - 포화 이진 트리 : 모든 레벨이 꽉 찬 이진 트리
  - 완전 이진 트리 : 위에서 아래로, 왼쪽에서 오른쪽으로 순서대로 차곡차곡 채워진 이진 트리
  - 모든 노드가 0개 혹은 2개의 자식 노드만을 갖는 이진 트리를 가리켜 정 이진 트리라고 한다.

- 우선순위 큐
  - 현재 우선순위 큐 안에서 제일 우선순위가 높은 원소가 위로 올라감.
  - 따라서 모든 정점은 자신의 자식들 보다 우선순위가 높음.
  - 보통 힙(heap)이라는 자료 구조로 구현됌.
  - 힙에는 최대 힙, 최소 힙 두 종류가 있는데 최대 힙은 각 노드의 값이 해당 자식의 값보다 크거나 같은 완전 이진트리를 의미함.(min heap은 이것과 반대.)
  - 최대 값을 찾는 것은 O(1), 삭제는 O(logN)이 소요 됌.

> [참고블로그](https://blog.naver.com/PostView.naver?blogId=kks227&logNo=220789373847&categoryNo=299&parentCategoryNo=0&viewDate=&currentPage=10&postListTopCurrentPage=1&from=postList&userTopListOpen=true&userTopListCount=5&userTopListManageOpen=false&userTopListCurrentPage=10) > [참고사이트](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure#binary-heap)
