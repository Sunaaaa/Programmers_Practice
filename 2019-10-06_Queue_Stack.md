## Queue

![1570367363460](https://user-images.githubusercontent.com/39547788/66256625-c372c700-e7ca-11e9-8fa3-e9e0c99b534b.png)

<br>

- 일반적으로 FIFO (First-In-First-Out)
- 입력 : put()
- 출력 : get()

- Queue(): 가장 일반적인 큐 자료 구조 ( FIFO )
- LifoQueue(): 나중에 입력된 데이터가 먼저 출력되는 구조 (스택과 유사 방식) ( LIFO )
- PriorityQueue(): 데이터마다 우선순위를 넣어서, 우선순위가 높은 순으로 데이터 출력 ( (우선순위, 데이터) )

<br>

### Queue 연습

- FIFO와 LIFO Queue 구현하는 클래스를 생성한다.

  ```python
  # 추상 클래스 만들기
  from abc import *
  
  class AbstractQueue(metaclass=ABCMeta):
  
      @abstractmethod
      def enqueue(self, data):              # 데이터의 추가
          raise NotImplemented
  
      @abstractmethod    
      def dequeue(self):                     # 데이터의 꺼내오기
          raise NotImplemented
          
  
  # AbstractQueue 클래스를 상속받는 클래스 만들기             
  
  class MyFIFOQueue(AbstractQueue):
      
      def __init__(self):
          self.items = list()
          
      def enqueue(self, data):              # 데이터의 추가
          self.items.append(data)
  
      def dequeue(self):                     # 데이터의 꺼내오기
          data = self.items[0]
          del self.items[0]
          return data
          
          
  class MyLIFOQueue(AbstractQueue):
  
      def __init__(self):
          self.items = list()
  
      def enqueue(self, data):              # 데이터의 추가
          self.items.append(data)
  
      def dequeue(self):                     # 데이터의 꺼내오기
          data = self.items[-1]
          del self.items[-1]
          return data
  
          
  a = MyFIFOQueue()
  a.enqueue([1,2,3,4,5])
  a.enqueue('a')
  print(a.dequeue())	# [1, 2, 3, 4, 5]
  print(a.dequeue())	# a
  
  
  b = MyLIFOQueue()
  b.enqueue([1,2,3,4,5])
  b.enqueue('a')
  print(b.dequeue())	# a
  print(b.dequeue())	# [1, 2, 3, 4, 5]
  
  ```

<br>

- 하나의 클래스 구현으로 FIFO, LIFO, Priority 지정하여 Queue 생성

  - 인자값으로 Queue의 종류를 지정한다.

    - 'FIFO' : FIFO Queue
    - 'LIFO' : LIFO Queue
    - 'PRIORITY' 또는 'FIFO'와 'LIFO'를 제외한 모든 값 : Priority Queue

    ```python
    # 하나의 클래스 구현으로 FIFO, LIFO, Priority 지정하여 Queue 생성
    
    
    from abc import *
    
    class AbstractQueue(metaclass=ABCMeta):
        
        @abstractmethod
        def enqueue(self, data):              # 데이터의 추가
            raise NotImplemented
    
        @abstractmethod    
        def dequeue(self):                     # 데이터의 꺼내오기
            raise NotImplemented
    
    import queue
    
    class MyQueue(AbstractQueue):
        def __init__(self, type):
            if type == 'FIFO':
                self.data = queue.Queue()
            elif type == 'LIFO':
                self.data = queue.LifoQueue()
            else :
                self.data = queue.PriorityQueue()
            
        def enqueue(self, data):              # 데이터의 추가
            self.data.put(data)
    
        def dequeue(self):                     # 데이터의 꺼내오기
            return self.data.get()
        
        
        
    data_fq = MyQueue('FIFO')
    for i in range(5):
        data_fq.enqueue(i)
    
    for i in range(5):
        print('FIFO_QUEUE : ', i, '번째 : ', data_fq.dequeue())
        
    # FIFO_QUEUE :  0 번째 :  0
    # FIFO_QUEUE :  1 번째 :  1
    # FIFO_QUEUE :  2 번째 :  2
    # FIFO_QUEUE :  3 번째 :  3
    # FIFO_QUEUE :  4 번째 :  4
       
        
    data_lq = MyQueue('LIFO')
    for i in range(5):
        data_lq.enqueue(i)
    
    for i in range(5):
        print('LIFO_QUEUE : ', i, '번째 : ', data_lq.dequeue())
    
    # LIFO_QUEUE :  0 번째 :  4
    # LIFO_QUEUE :  1 번째 :  3
    # LIFO_QUEUE :  2 번째 :  2
    # LIFO_QUEUE :  3 번째 :  1
    # LIFO_QUEUE :  4 번째 :  0
            
            
    data_pq = MyQueue('PRIORITY')
    
    data_pq.enqueue((10,0))
    data_pq.enqueue((1,1))
    data_pq.enqueue((5,2))
    data_pq.enqueue((20,3))
    data_pq.enqueue((6,4))
    
    for i in range(5):
        print('PRIORITY_QUEUE : ', i, '번째 : ', data_pq.dequeue())
    
    # PRIORITY_QUEUE :  0 번째 :  (1, 1)
    # PRIORITY_QUEUE :  1 번째 :  (5, 2)
    # PRIORITY_QUEUE :  2 번째 :  (6, 4)
    # PRIORITY_QUEUE :  3 번째 :  (10, 0)
    # PRIORITY_QUEUE :  4 번째 :  (20, 3)
    ```

    <br>

    <br>



## Stack

![1570362023812](https://user-images.githubusercontent.com/39547788/66269637-b9fa6500-e885-11e9-9b2b-93d1477568cd.png)

<br>

- LIFO (Last-In-First-Out)
- 저장소의 끝 부분 : top
- 입력 : push(data)
- 출력 (맨 위의 값을 리턴하고 삭제함) : pop()
- 엿보기 : 맨 위 갓을 반환하고 삭제는 하지 않음 :peek()
- 비어있는지 확인 (boolean) : is_empty()

<br>

### Stack 연습

- list 활용

  ```python
  # python list를 활용한 stack 구현
  
  
  class MyStack(list):
      push = list.append    # Insert
      
      # 데이터가 있는지 확인
      def is_empty(self):
          if not self:
              return True
          else :
              return False
          
          
      # 최상단 데이터 확인
      def peek(self):
          return self[-1]
      
  if __name__ == "__main__":
      a = MyStack()
      a.push(1)
      a.push(2)
      a.push(3)
  
      print(a)
      
      while a:
          data = a.pop()
          print(data, end=' ')
  
  # [1,2,3]
  # 3 2 1
  ```

  

<br>

- node로 구현

  ```python
  # node를 활용한 stack 구현
  # head만 있어도 구현 가능
  
  # node 생성
  class Node :
      def __init__(self, data):
          self.data = data
          self.next = None
  
  class MyNodeStack:
      
      def __init__(self):
          self.head = None
                  
      
      # 데이터가 있는지 확인
      def is_empty(self):
          if not self.head:
              return True
          
          return False
  
      
      def push(self, data):
          new_node = Node(data)
          new_node.next = self.head
          self.head = new_node
      
      
      def pop(self):
          if self.is_empty():
              return None
          
          ret_data = self.head.data
          self.head = self.head.next
          
          return ret_data
  
          
      def peek(self):
          if self.is_empty():
              return None
          return self.head.data
          
          
      
  if __name__ == "__main__":
      s = MyNodeStack()
      
      print(s.is_empty())  # True
      
      s.push(1)
      s.push(2)
      s.push(3)
      s.push(4)
      s.push(5)
      s.push(6)
      
      # 1->2->3->4->5->6
  
      print('peek of data : ', s.peek())   # 6
      
      while not s.is_empty():
          print(s.pop(), end=' ')
  
          
  # True
  # peek of data :  6
  # 6 5 4 3 2 1 
  ```

  <br>

  - s = MyNodeStack()

    ![1570366832667](https://user-images.githubusercontent.com/39547788/66269638-b9fa6500-e885-11e9-9f0b-14e5f4286f70.png)

    <br>

  - s.push(1)

    ![1570366873520](https://user-images.githubusercontent.com/39547788/66269639-b9fa6500-e885-11e9-8a0e-df7b973316a9.png)

    <br>

  - s.push(2)

    ![1570366912454](https://user-images.githubusercontent.com/39547788/66269640-b9fa6500-e885-11e9-8b6d-ca90756467ee.png)

    <br>

  - s.pop()

    ![1570367900546](C:\Users\USER\AppData\Roaming\Typora\typora-user-images\1570367900546.png)

    <br>

