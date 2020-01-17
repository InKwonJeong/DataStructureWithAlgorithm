# Recursion

### 재귀의 개념
- 어떤 사건이 자신을 포함하고 다시 자기 자신을 사용하여 정의 될때 재귀적이라 한다.

1. 하노이의 탑

```java
  static void hanoiMove(int num , int x, int y){
    // 중간 기둥으로 옮기기
    if(num > 1){
      hanoiMove(num - 1, x, 6 - x - y);
    }

    // 가장 아래 원반 옮기기
    System.out.printf("원반[%d]을 %d번 기둥에서 %d번 기둥으로 이동/n", num, x, y);

    // 중간기둥에서 마지막 기둥으로 옮기기
    if(num > 1){
      hanoiMove(num - 1, 6 - x - y, y);
    }
  }
```

2. 8퀸 문제


```java

class EightQueen {
   static boolean[] flag_a = new boolean[8];   // 각 행에 퀸을 놓았는지 체크
   static boolean[] flag_b = new boolean[15];    // ／대각선 방향으로 퀸을 놓았는지 체크
   static boolean[] flag_c = new boolean[15];    // ＼ 대각선 방향으로 퀸을 놓았는지 체크
   static int[] pos = new int[8];            // 각 열의 퀸의 위치

   // 각 열의 퀸의 위치를 출력
   static void print() {
      for (int i = 0; i < 8; i++)
         System.out.printf("%2d", pos[i]);
      System.out.println();
   }

   // i열의 알맞은 위치에 퀸을 배치
   static void set(int i) {
      for (int j = 0; j < 8; j++) {             // 현재 위치에 놓을수 있는지 검사한다.
         if (flag_a[j] == false &&              // 가로(j행)에 아직 배치하지 않았습니다.
             flag_b[i + j] == false &&           // 대각선 ／에 아직 배치하지 않았습니다.
             flag_c[i - j + 7] == false) {     // 대각선 ＼에 아직 배치하지 않았습니다.

            pos[i] = j;                       // 퀸을 j행에 배치합니다.

            if (i == 7)                     // 모든 열에 배치한다면(마지막 퀸을 배치했다면 어디에 배치했는지 출력)
               print();
            else {                          // 마지막 퀸을 배치한게 아니라면
               flag_a[j] = flag_b[i + j] = flag_c[i - j + 7] = true; // 지금 배치한 퀸의 행과 두 대각선을 배치했다고 체크
               set(i + 1); // 다음 열에 퀸을 배치
               flag_a[j] = flag_b[i + j] = flag_c[i - j + 7] = false; // 이전 배치한 퀸의 행과 두 대각선을 배치했다고 체크해제.
            }
         }
      }
   }

   public static void main(String[] args) {
      set(0);
   }
}
```
