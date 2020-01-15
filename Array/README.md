# Array

1. 배열기본
  - 배열 정렬
   ```java
      Arrays.sort()
      public static void sort(int[] a)
      public static <T> void sort(T[] a, Comparator<? super T> c)
   ```
  - 배열 뒤집기
    ```java
      public static <T> void swap(T[] a, int idx1, int idx2){
        T temp = a[idx1];
        a[idx1] = a[idx2];
        a[idx2] = temp;
      }

      public static <T> void reverseArray(T[] a){
        for(int i=0; i < a.length/2; i++)
          swap(a, i, (a.length-1)-i );
      }
    ```
  - 배열 복사
     - Object클래스의 clone 사용 (다차원 배열은 깊은 복사가 되지 않음)
     - Arrays.copyOf(T[] a, int newArrayLength) (다차원 배열은 깊은 복사가 되지 않음)
     - System.arrayCopy (얕은 복사)
2. 기수변환
 -
  ```java
    static void swp(char[] a, int idx1, int idx2){
           char t = a[idx1];
           a[idx1] = a[idx2];
           a[idx2] = t;
       }

     static void reverse(int digits, char[] d){
         int len = (digits+1)/2;
         for(int i =0 ; i < len; i++){
             swp(d, i, digits-i);
         }
     }

     static char[] cardConvR(int x, int r, char[] d){
         int digits = 0;
         String dchar = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ";

         do {
             d[digits] = dchar.charAt(x % r);
              x = x/r;
              digits = digits + 1;
         }while(x != 0);

         reverse(digits-1, d);
         return d;
     }
  ```
3. 소수구하기
   ```java
       public class PrimeNumber {
        public static void main(String[] args) {

            int counter = 0;  //곱셈 & 나눗셈의 횟수
            int ptr = 0;
            int[] prime = new int[500];

            // 2와 3은 소수이다.
            prime[ptr++] = 2;
            prime[ptr++] = 3;

            for (int n = 5; n <= 1000; n += 2) {
                boolean flag = false;
                for (int i = 1; prime[i] * prime[i] <= n; i++) {
                    counter += 2;
                    if (n % prime[i] == 0) {
                        flag = true;
                        break;
                    }
                }

                if (!flag) {
                    prime[ptr++] = n;
                    counter++; // 위의 반복문을 빠져나올때 했던 prime[i]*prime[i] 연산 횟수
                }

                for(int i = 0; i< ptr; i++)
                    System.out.println(prime[i]);

                System.out.println("곱셈과 나눗셈을 수행한 횟수:"+counter);
            }
        }
    }
   ```

4. 기타
 - 윤년구하기
   ```java
    public static int isLeap(int year) {
          return (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0) ? 1 : 0;
      }
   ```
- 유클리드 호제법(최대공약수)
   ```java
     public static int gcd(int a, int b) {
      if(a%b == 0)
        return b;
      else
        return gcd(b, a%b);
    }
   ```
- 최소 공배수
  - (A*B) / gcd(A,B)
