## 0327

### 排序算法

选择排序：每次都要遍历无序的数据，找到最小（最大）的和无序数据第一位进行交换， O(n*n)

~~~C++
void selectsort(vector<int>& nums, int n) {
	for(int i=0; i<n-1; i++) { 
        int min = i;
        for(int j=i+1; j<n; j++) {
            if(nums[j] < nums[min]) {
				min = j;
            }
        }
        swap(nums[min], nums[i]);
    }
}
~~~

冒泡排序：从前往后多次扫描，每次都会比较相邻两个数，如何和需要的次序不符时，就交换相关数据位置

**如果是升序排序，每次都会得到最大的数据 到最后位置，每一轮比较次数比前一轮少一次**

~~~C++
void bubblesort(vector<int>& nums, int n) {
    for(int i=0; i<n; i++) {
        for(int j=0; j<n-i; j++) {
			if(a[j] > a[j+1])
                swap(nums[j], nums[j+1]);
        }
    }
}
~~~



插入排序：初始认为第一个数排好序，然后将第一个未排序的数据 和 前面已排好序的进行对比，直到找到合适的位置插入

~~~C++
void insertsort(vector<int>& nums, int n) {
	for(int i=1; i<n; i++) {
        //第一个数认为已经排好序
        int key = nums[i];
        int j=i-1;
        while(j>=0 && nums[j]>key) {
			a[j+1]=a[j];
            j--;
        }
        a[j+1]=key;
    }
}
~~~

堆排序：

**升序用大顶堆**

~~~C++
//下标0标识根节点情况下
//下标为i的父节点下标 (i-1)/2 整数除法
//下标为i的左孩子 i*2+1
//下标为i的有孩子 i*2+2

//heapify维护堆的性质
//假设是大顶堆
void heapify(vector<int>& nums, int n, int i) {
    int largest = i;
    int left = i*2+1, right = i*2+2;
    if(left < n && nums[largest]<nums[left]) largest = left;
    if(right < n && nums[largest]<nums[right]) largest = right;
    if(largest != i) {
        swap(nums[largest], nums[i]);
        heapify(nums, n, largest);
    }
}

void heapsort(vector<int>& nums, int n) {
	//建堆
    for(int i=(n-1)/2; i>=0; i--) 
        heapify(nums, n, i);
    
    for(int i=n-1; i>=0; i++) {
        swap(nums[i], nums[0]);
        heapify(nums, i, 0);
    }
}
~~~







![C++排序算法](D:\02实习\02Notes\InterviewNotes\笔记图片\C++排序算法.png)



**插冒龟**  插入排序、冒泡排序、归并排序

**桶计鸡**  桶排序、计数排序、基数排序

**都是稳定的**







## 0313

自己实现一个String类，包括无参构造函数、含参构造函数、拷贝构造函数、赋值构造函数、析构函数







## 0309

**priority_queue**

第一个参数是存储对象的类型，第二个参数是存储元素的底层容器，第三个参数是函数对象

~~~C++
priority_queue<float> q;    //默认的是大顶堆 
priority_queue<float, vector<float>, less<int>> q;    //大顶堆 
priority_queue<float, vector<float>, greater<int>> q;  //小根堆
~~~



- 默认是大顶堆 **默认队头元素 优先级最高**

  ~~~C++
  priority_queue<float> q;    //默认的是大顶堆 
  q.push(66.6);
  q.push(22.2);
  q.push(77); 
  
  // read and print two elements
  cout << q.top() << ' ';         //queue当中是q.front();
  q.pop();
  cout << q.top() << endl;
  q.pop(); 
  
  // insert three more elements
  q.push(11.1);
  q.push(55.5);
  q.push(33.3); 
  
  // pop and print remaining elements
  while (!q.empty())
  {
      cout << q.top() << ' ';
      q.pop();
  }
  cout << endl;
  
  //77 66.6
  //55.5 33.3 22.2 11.1 
  ~~~

- 将节点存入到优先队列 **一**

  ~~~C++
  struct Node
  {
      string name;
      int value;
      bool operator <(Node a) const  {  return value < a.value; }
      bool operator >(Node a) const  {  return value > a.value; }
  };
  // priority_queue<Node> A;                    //大根堆
  // priority_queue<Node, vector<Node>, greater<Node> > B;    //小根堆 
  
  priority_queue<Node, vector<Node>, less<Node>> q;    //大顶堆 
  q.push(Node{"aaa", 100});
  q.push(Node{"bbb",200});
  cout << q.top().name << ' '<<q.top().value<<endl;  //queue当中是q.front();
  q.pop();
  cout << q.top().name << ' '<<q.top().value; 
  q.pop(); 
  
  //bbb 200
  //aaa 100
  
  ~~~

- 节点放入优先队列 **二**

  ~~~C++
  struct Node{
          string name;
          int value; 
      };
  
      struct Cmp {
          bool operator() (Node a, Node b) {
              return a.value > b.value;
          }//相当于 less
          //创建 大根堆
      };
  ~~~

  



**快排**

时间复杂度 nlogn 最坏情况 n*n

空间复杂度 logn （递归栈



**归并排序使用场景**

时间复杂度 nlogn   空间复杂度 n

**外部排序，处理超过内存限度的数据**

![阿里云面试01](D:\02实习\02Notes\1准备暑期实习\笔记图片\阿里云面试01.png)

