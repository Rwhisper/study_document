> List는 순서를 갖고 원소들을 저장하는 자료구조이다. sequence라고도 불림
> ArrayList, LinkedList로 구현이 가능하다

## Array List
> 배열을 기반으로 구성된 list 자료구조, static array(정적배열)로 구현할수 있고 dynamic array(동적 배열)로 구현 가능

### 배열 Static Array
> 배열의 특성
> 1. 고정된 저장 공간(fixed-size)
> 2. 순차적인 데이터 저장

배열은 선언 시에 size를 정하여 해당 size만큼의 연속된 메모리를 할당 받아 data를 연속적/순차적으로 저장하는 자료구조

``` java
int arr[3] = {1, 2, 3};  // size가 3인 int형 배열 선언 
```
 위 예시에서는 배열의 size를 3으로 정했기 때문에 int형 데이터(4 byte) 3개를 저장할 메모리 공간인 12Byte를 미리 할당을 받는다. 이처럼 고정된 size를 갖게 되기 때문에 static array라고 부르기도 한다.
 또한 배열의 데이터를 연속적이고 순차적으로 메모리에 저장한다.

#### Random access
메모리에 저당된 데이터에 접근하려면 주소 값을 알아야 한다. 배열변수는 자신이 할당받은 메모리의 첫 번째 주소값을 가리킨다. 배열은 연속적/순차적으로 저장되어 있기 때문에 첫 주소값만 알고 있다면 어떤 index에도 즉시 접근이 가능하다. 이를 direct access 또는 random access라고도 부른다. 첫 번째 데이터가 저장된 주소값이 0x4AF55라면 2번 째 데이터는 0x4AF55 + 4*1(byte)에 저장되어있을것이고 n번째 데이터는 0x4AF55 + 4*(n-1)에 저장되어 있을 것이다.  아무리 긴 배열이더라도 한번의 연산으로 원하는 데이터에 바로 접근할 수 있기에 O(1)의 시간복잡도를 가진다.

### 동적 배열 dynamic array
> 선언 이후에 size를 변경할 수 없는 정적배열(Static Array)과 다르게 동적 배열(dynamic Array)는 size를 늘릴 수 있다.

 동적 배열(dynamic array)은 배열의 크기(size)를 변경(resizing)할 수 있는 배열이다. fixed-size인 Statix Array의 한계점을 보안하고자 고안되었다. 동적배열에 데이터를 계속 추가하다가 기존에 할당된 size를 초과하게 되면, size를 늘린 배열을 새로 선언하고 그곳으로 모든 데이터를 옮긴다. 그리고 기존의 배열은 메모리에서 삭제한다. 이과정을 resize라고 한다. resize를 한칸씩 늘린다면 비효율적이므로 일반적으로 2배 큰 크기로 resize한다. 이를 더블링(Doubling)이라고 한다. resize를 활용하면 데이터를 추가로 계속 저장 할 수 있게 된다.

#### Dynamic Array 사용법
 선언시에 배열의 크기를 정하지 않아도 되기 때문에 코딩테스트에서 dynamic array를 자주 사용하게 된다. java에서는 resize를 지원해주는 ArrayList를 주로 사용한다.
 #### ArrayList 구현(add) // 귀찮아서 add만 만듬...
 
``` java
// arrayList
public class CustomArrayList<T> {  
    int size;       // 현재 값이 배정되어 있는 원소의 크기  
    int capacity;   // 현재 배정된 메모리의 크기 무조건 capacity >= 이어야 함  
    int growthFactor = 2;   // size와 곱해서 새로 지정할 배열을 크기를 지정할 기준  
  
    Object[] arrPointer = null; // 실제로 저장할 배열  
  
    CustomArrayList(){  
        this.size = 0;  
        this.capacity = this.growthFactor * 1;  
        this.arrPointer = new Object[this.capacity];  
    }  
  
    /**  
     * 객체 추가  
     * @param newElement  
     */  
    void add(Object newElement){  
        if(this.size < this.capacity){  
            // size가 capacity보다 작을때는 현재 배열에 해당 값 추가  
            arrPointer[this.size] = newElement;  
        }else{  
            // size가 capacity와 같아지므로 array의 크기를 더 크게 만들어서 잡아줘야 함  
            this.capacity = this.size * this.growthFactor;  
            Object[] newArrayPoint = new Object[this.capacity];  
            for (int i = 0; i < this.size; i++) {  
                 newArrayPoint[i] = this.arrPointer[i];  
            }  
            this.arrPointer = newArrayPoint;  
            this.arrPointer[this.size] = newElement;  
        }  
        this.size++;  
    }  
}
```
 
#### ArrayList 사용법
##### 1. ArrayList 생성
``` java
import java.util.ArrayList;
...
ArrayList<Integer> arr1 = new ArrayList<>(); // 타입 생략
ArrayList<Integer> arr2 = new ArrayList<Integer>(); // 타입 지정
ArrayList<Integer> arr3 = new ArrayList<>(10); // 초기 용량(capacity) 설정
ArrayList<Integer> arr4 = new ArrayList<>(arr1); // 다른 collection값으로 초기화
ArrayList<Integer> arr5 = new ArrayList<>(ArraysasList(1,2,3,4,5)); // Arrays.asList()

```
###### 2. ArrayList 추가/ 변경/삭제
- add(newElement) : 추가
- set(index, updateElement) : 변경
- remove(index) : 삭제
``` java
ArrayList<Integer> arrs = new ArrayList<>();
arrs.add(2);
arrs.add(2);
arrs.add(3);
arrs.add(4);
arrs.set(0,1);
int removeInt = arrs.remove(3);
System.out.println(removeInt); // 4
System.out.println(arrs); // [1, 2, 3]
```

###### 3. ArrayList 값 확인
- get(index) : 해당 인덱스 값 조회
- contains(value) : 값이 존재하는지 확인
- indexOf(value) : 값이존재할때 해당 값의 인덱스를 반환
``` java
ArrayList<Integer> arrs = new ArrayList<>();
arrs.add(1);
arrs.add(10);
System.out.println(arrs.get(0)); // 1
System.out.println(arrs.get(1)); // 10
System.out.println(arrs.contains(1)); // true
System.out.println(arrs.contains(2)); // fasle
System.out.println(arrs.indexOf(1)); // 0
System.out.println(arrs.indexOf(2)); // -1
```
## Linked List
> Linked List는 Node라는 구조체가 연결되는 형식으로 데이터를 저장하는 자료구조로
> node는 데이터값(value>과 다음 주소(next)로 구성되어있다.

### 물리적 비연속적, 논리적 연속적
Linked List 메모리상에서는 비연속적으로 저장이 되어 있지만, 각각의 node가 다음 노드의 메모리 주소값을 가리킴으로써 논리적으로 연속성을 가지게 된다.
Array의 경우 연속성을 유지하기 위해 메모리 상에서 순차적으로 데이터를 저장하는 방식을 사용하였지만, Linked list에서는 메모리 상에서 연속성을 유지하지 않아도 되기 때문에 메모리 사용이 좀 더 자유롭다.

### Linked List 구현

