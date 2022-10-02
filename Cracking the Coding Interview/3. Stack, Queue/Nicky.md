### Stack
- LIFO
- recursive를 iterative로 구현할 수 있게 한다

### Queue
- FIFO
- BFS, Cache

### 문제1
내생각) 스택 1,2,3을 array[index % 3 === 0], array[index % 3 === 1], array[index % 3 === 2]로 할당  
js로 해서 가능한거일수도? (arr의 크기에 구애받지 않음..)
1. stack1.push
- arr[i % 3 === 0]을 처음부터 순회하면서 빈칸을 발견하면 넣는다
2. stack1.peek
- 스택들의 마지막 위치를 저장 안한다고 할때, arr[i % 3 === 0]을 처음부터 순회하다가 빈칸을 발견하면 그 전의 값을 돌려준다
3. stack1.pop
- peek한 뒤 해당 위치를 빈칸(null같은것)으로 변경한다
해설) 스택 크기 고정 / 고정안됨(매우 어렵 복잡) 나눠서 생각해볼 수 있음

### 문제4
내생각) Push하면 스택1에 계속 넣고, Pop하면 하나 빼고 전체를 스택2로 push했다가 스택1에서 하나 pop 후 스택2에서 다시 전체를 스택1로 push
해설) lazy 접근법 고려
