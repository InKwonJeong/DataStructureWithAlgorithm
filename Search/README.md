# Search

### 검색개념
- 선형검색
  - 무작위로 저장된 데이터 모임
  - 데이터 전체를 검색해야 한다
  - 느린 검색
- 이진검색
  - 일정한 규칙으로 저장된 데이터 모임 (정렬)
  - 빠른검색
- 해시법
  - 추가, 삭제가 자주 일어나는 데이터 모임
  - 빠른검색
- 체인법
  - 같은 해시 값의 데이터를 선형 리스트로 연결하는 방법
- 오픈주소법
  - 데이터를 위한 해시값이 충돌할때 재해시 하는 방법

1. 선형검색
```java
public static <T extends Comparable<? super T>> int seqSearch(T[] a, T key ){
  for(int i=0; i<a.length; i++){
    if(a[i].equals(key))
    return i;
    return -1;
  }
}
```

2. 이진검색
```java
public static <T extends Comparable<? super T>> int binSearch(T[] a, T key ){

  int start = 0;
  int end = a.length-1;

  while(start<=end){
    int mid = (start+end)/2;

    if(a[mid].compareTo(key) == 0)
    return mid;
    else if(a[mid].compareTo(key) < 0)
    start = mid+1;      
    else if(a[mid].compareTo(key) > 0)
    end = mid-1;
  }
  return -1;
}
```
3. Comparable & Comparator
- Comparable
  - 객체를 비교할 때 기본으로 적용되는 기준이 되는 메소드를 정의하는 인터페이스
```java
class A implements Comparable<A>{

  @Override
  public int compareTo(A c){
    // this가 c보다 크면 양
    // this와 c가 같으면 0
    // this가 c보다 작으면 음

  }
}

```

- Comparator
  - 객체를 비교할 때 기본으로 적용되는 기준이 아닌 다른 기준을 정의하는 인터페이스
```java
class X{
  public static final Comparator<T> COMPARATOR = new Comp();

  private static class Comp implements Comparator<T>{
    @Override
    public int compare(T d1, T d2){
      // d1가 d2보다 크면 양
      // d1와 d2가 같으면 0
      // d1가 d2보다 작으면 음
    }
  }
}

```
