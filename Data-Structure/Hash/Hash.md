# Hash

### Hash Function( 해시 함수 )

- 단방향 암호화 기법
- 임의의 길이 데이터 → 고정된 길이의 데이터로 변환(매핑)
    - 매핑 되기 전의 데이터 : key
    - 매핑 후 데이터 : Hash Value

![Alt text](https://user-images.githubusercontent.com/84346055/250495862-45722bfa-0f53-4d99-81e1-db2e276fc5ab.png)

- 문제점
    - 해시 충돌 !
        - 입력 데이터의 길이에 상관없이 매핑되는 데이터는 고정 길이
        - 데이터의 개수가 무수히 많아진다면 입력값이 다르더라도 같은 결과값 경우 발생

**해시 충돌 원리**

- 비둘기집 원리
    - N+1마리의 비둘기를 N개의 집에 넣을 때 적어도 한 개의 집에는 비둘기가 2마리 이상이다.
- 해시 테이블의 키의 조합은 해시 테이블의 인덱스의 개수보다 많기 때문에 해시 충돌이 일어난다.

*중요 관점은 해시 충돌을 완벽하게 없애는 것이 아니라 발생 확률을 줄이는 것이다 !*

### 해시 테이블

- 해시 함수를 이용하여 Key를 Hash Value로 매핑 , Hash Value를 index나 주소로 사용하여 데이터 값을 키와 함께 저장하는 자료구조
- index만 알 경우 빠르게 검색 가능

### 해시 충돌 해결 방법

**체이닝**

- 해시 테이블의 각 버켓에 대하여 연결 리스트를 할당
    - 해시 충돌이 발생하여도 데이터 손실이 없이 모든 값을 다룰 수 있다.
    - 자바의 **해시테이블 , 해시맵**이 사용하는 방식

![Alt text](https://user-images.githubusercontent.com/84346055/250495840-f9adfbdf-525e-4446-93d4-28f7ad0f0a31.png)

**개방 주소법**

- 해시 충돌이 발생할 경우 다른 버켓에 데이터를 저장한다.
- **검색시**
    - 충돌 검색이 이루어진다면 근처 버켓을 순회하면서 탐색 !
        - 선형 탐색 : 충돌에 대하여 몇 개의 버킷을 건너뛰고 탐색
        - 제곱 탐색 : 제곱수만큼 증가하여 탐색
        - 이중 해시 : 해시 함수를 한번 더 적용

**체이닝 VS 개방 주소법**

- 데이터의 개수가 적은 경우에는 개방 주소법 , 많은 경우에는 체이닝이 효율적

## Java에서의 Hash

- 자바에서 Hash에 대한 구현체는 크게 3가지 존재한다.
    - HashMap
    - HashTable
    - HashSet

### HashMap

- (Key , Value) 형식의 데이터를 저장하는 자바의 자료구조 → Map 인터페이스를 상속받는다.
    - 내부적인 저장에 해싱을 사용 !

```java
public class HashMap<K,V>
{
		static final int MAXIMUM_CAPACITY = 1 << 30 ; //1073741824 

		static final float DEFAULT_LOAD_FACTOR = 0.75f;
}
```

- LOAD_FACTOR 는 일종의 비율이다.
    - HashMap의 테이블에 LOAD_FACTOR의 비율만큼 데이터가 차게 될 경우 Capacity(용량)을 2배로 증가시킨다.
    - 동적으로 조절 가능하다.

**내부 구현**

**Node**

```java
 class Node<K,V> implements Map.Entry<K,V> {
     final int hash;
     final K key;
     V value;
     Node<K,V> next;

     Node(int hash, K key, V value, Node<K,V> next) {
         this.hash = hash;
         this.key = key;
         this.value = value;
         this.next = next;
     }
}
```

- Key , Value 형태의 데이터를 저장하는 Node가 static class로 구현되어 있다.
- 충돌 완화를 위해 체이닝 방식을 사용하기 때문에 next 필드를 가지고 있는 것도 확인할 수 있다.
    - Node가 Tree형이면 Tree에 새로 연결 treeifyBin(tab, hash)

Node Table

```
transient Node<K,V>[] table;
```

**put**

```java
public class HashMap<K, V> extends AbstractMap<K, V>
    implements Map<K, V>, Cloneable, Serializable{

    static final int hash(Object key) {
        int h;
        return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
    }
    
    public V put(K key, V value) {
        return putVal(hash(key), key, value, false, true);
    }
    
    final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
   }
    
}
```

- put 메소드를 사용해 데이터를 삽입할 때는 hashCode 메소드를 호출해서 Key를 기반으로 해싱을 진행해 고정된 크기의 int 값을 반환
- put을 자세히 보면 체이닝 방식에 있어 링크드 리스트를 사용하기도 하지만 트리를 사용하기도 한다.

**get**

```java
class HashMap<K,V>
{
		final Node<K,V> getNode(Object key) {
        Node<K,V>[] tab; Node<K,V> first, e; int n, hash; K k;
        if ((tab = table) != null && (n = tab.length) > 0 &&
            (first = tab[(n - 1) & (hash = hash(key))]) != null) {
            if (first.hash == hash && // always check first node
                ((k = first.key) == key || (key != null && key.equals(k))))
                return first;
            if ((e = first.next) != null) {
                if (first instanceof TreeNode)
                    return ((TreeNode<K,V>)first).getTreeNode(hash, key);
                do {
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        return e;
                } while ((e = e.next) != null);
            }
        }
        return null;
    }

		public V get(Object key) {
        Node<K,V> e;
        return (e = getNode(key)) == null ? null : e.value;
    }
}
```

1. table이 없다면 → null
2. table이 존재하고, 해당 table 배열의 길이가 0 보다 크고, 배열의 해당 자리에 값이 null 이 아니면!
    1. Hash값이 동일하고, 키값이 정확히 같다면 객체 반환
    2. a 케이스가 아니고, 값이 존재하면
        1. TreeNode라면 Tree 순회해서 값 여부 판단 및 객체 반환
        2. 아니라면 LinkedList를 순회하면서 해당 객체를 찾고 반환

### HashMap VS HashTable

- `Thread-safe 여부`
    - Hashtable은 `Thread-safe`하고, HashMap은 `Thread-safe`하지 않다는 특징을 가지고 있습니다.
        - 단일 스레드 환경이라면 HashMap이 성능상 이점을 가진다.
- `Null 값 허용 여부`
    - Hashtable은 key에 null을 허용 X, HashMap은 key에 null을 허용 O.
- `Enumeration 여부`
    - Hashtable은 not fail-fast Enumeration을 제공하지만, HashMap은 Enumeration을 제공하지 않습니다.
- HashMap은 보조해시를 사용하기 때문에 보조 해시 함수를 사용하지 않는 Hashtable에 비하여 해시 충돌(hash collision)이 덜 발생할 수 있어 상대적으로 성능상 이점이 있습니다.

### HashSet

- 객체를 중복해서 저장할 수 없다. null 값은 1개만 허용
- 내부적으로 HashMap을 가지고 있다.
    - `private transient HashMap<E,Object> map;`
