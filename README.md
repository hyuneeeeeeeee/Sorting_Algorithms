# Sorting Algorithms

##### 버블, 선택, 삽입, 쉘 정렬 알고리즘을 이용하여 입력된 배열을 오름차순 정렬한다.

## 1. 버블 정렬

> 이웃한 두 원소의 값을 비교하여 서로의 값을 교환하여 정렬

- 입력 : 크기가 20 이하인 랜덤 배열
- 출력 : 오름차순 정렬된 배열

#### 코드

```java
    public static void Bubble(int[] arr) {
        for (int i = 0; i < arr.length - 1; i++) {
            for (int j = 0; j < arr.length - 1; j++) {
                if (arr[j] > arr[j + 1]) {      // 위의 원소가 아래의 원소보다 크면
                    int temp = arr[j + 1];
                    arr[j + 1] = arr[j];
                    arr[j] = temp;              // 서로 자리를 바꾼다
                }
            }
        }
    }
```

#### 시간 복잡도

- 평균 : O(n^2)
- 최선 : O(n^2)
- 최악 : O(n^2)

버블 정렬은 for 루프 속에서 for 루프가 수행된다.

루프 내부의 총 비교 횟수 : (n - 1) + (n - 2) + ⋯ + 1 = n(n - 1) / 2

안쪽 for 루프 내부의 if 조건이 참일 때의 자리 바꿈은 O(1)

따라서 시간 복잡도는 *n(n - 1) / 2 x O(1) = O(n^2) x O(1) = **O(n^2)***



## 2. 선택 정렬

> 전체 원소 중 최소값을 찾아 해당 순서에 맞는 위치에 원소를 정렬

- 입력 : 크기가 20 이하인 랜덤 배열
- 출력 : 오름차순 정렬된 배열

#### 코드 설명

1.  주어진 배열 중에서 최솟값을 찾는다.
2.  그 값을 맨 앞에 위치한 값과 교체한다.
3.  맨 처음 위치를 뺀 나머지 원소들을 같은 방법으로 교체한다.
4.  하나의 원소만 남을 때까지 위의 과정을 반복한다.

#### 코드

```java
    public static void Selection(int[] arr) {
        for (int i = 0; i < arr.length - 1; i++) { // arr.length - 1 : 마지막 요소는 자연스럽게 정렬됨
           int min = i;        // A[i]를 최솟값으로 놓는다
            for (int j = i + 1; j < arr.length; j++) // A[i] ~ A[n - 1]에서 최솟값을 찾는다
                if (arr[min] > arr[j])
                    min = j;
            int temp = arr[min];
            arr[min] = arr[i];
            arr[i] = temp;                  // for 루프에서 찾은 최솟값 A[min]을 A[i]와 교환
        }
    }
```

#### 시간 복잡도

- 평균 : O(n^2)
- 최선 : O(n^2)
- 최악 : O(n^2)

선택 정렬은 처음 for 루프가 (n - 1)번 수행된다.

루프 내부의 총 비교 횟수 : (n - 1) + (n - 2) + ⋯ + 1 = n(n - 1) / 2

안쪽 for 루프 내부의 if 조건이 참일 때의 자리 바꿈은 O(1)

따라서 시간 복잡도는 *n(n - 1) / 2 x O(1) = O(n^2) x O(1) = **O(n^2)***



## 3. 삽입 정렬

> 배열을 정렬된 부분과 정렬 안 된 부분으로 나누고, 정렬 안 된 부분의 가장 왼쪽 원소를 정렬된 부분의 적절한 위치에 삽입하여 정렬

- 입력 : 크기가 20 이하인 랜덤 배열
- 출력 : 오름차순 정렬된 배열

#### 코드 설명

정렬 안 된 부분의 숫자 하나가 정렬된 부분에 삽입됨으로써, 정렬된 부분의 원소 수가 1개 늘어나고, 동시에 정렬이 안 된 부분의 원소 수는 1개 줄어든다. 이를 반복하여 수행하면, 마지막에는 정렬이 안 된 부분엔 아무 원소도 남지 않고, 정렬된 부분엔 모든 원소가 있게 된다. 단, 정렬은 배열의 첫 번째 원소만이 정렬된 부분에 있는 상태에서 정렬을 시작한다.

#### 코드

```java
    public static void Insertion(int[] arr) {
        int j = 0;
        for (int i = 1; i < arr.length; i++) {
            int temp = arr[i];      // 정렬 안 된 부분의 가장 왼쪽 원소
            for (j = i - 1; j >= 0 && temp < arr[j]; j--)
                arr[j + 1] = arr[j];
            arr[j + 1] = temp;
        }
    }
```

#### 시간 복잡도

- 평균 : O(n^2)
- 최선 : O(n)
- 최악 : O(n^2)

삽입 정렬은 처음 for 루프가 (n - 1)번 수행된다.

루프 내부의 총 비교 횟수 : (n - 1) + (n - 2) + ⋯ + 1 = n(n - 1) / 2

루프 내부의 수행 시간은 O(1)

따라서 시간 복잡도는 *n(n - 1) / 2 x O(1) = O(n^2) x O(1) = **O(n^2)***

=> 삽입 정렬은 입력의 상태에 따라 수행 시간이 달라질 수 있다.

------

**최선의 경우**

입력이 이미 정렬되어 있으면, 항상 각각 정렬 안 된 부분의 가장 왼쪽 원소가 자신의 왼쪽 원소와 비교 후 자리 이동 없이 원래 자리에 있게되고, while 루프의 조건이 항상 거짓이 되므로 원소의 이동도 없다. 따라서 (n - 1)번의 비교만 하면 정렬을 마치게 된다. 이때가 삽입 정렬의 최선 경우이고 시간 복잡도는 O(n)이다.

삽입 정렬은 거의 정렬된 입력에 대해서 다른 정렬 알고리즘보다 빠르다.

------



## 4. 쉘 정렬

> 일정한 간격으로 그룹을 나누고, 각 그룹에 있는 원소들에 대해 삽입 정렬을 하여 전체 원소들을 정렬

=> 삽입 정렬을 이용하여 배열 뒷부분의 작은 숫자를 앞부분으로 빠르게 이동시키고, 동시에 앞부분의 큰 숫자는 뒷부분에 이동시켜 가장 마지막에는 삽입 정렬을 수행한다.

- 입력 : 크기가 20 이하인 랜덤 배열
- 출력 : 오름차순 정렬된 배열

------

**간격(gap)**

쉘 정렬은 간격이 미리 정해져야 한다. 가장 큰 간격부터 차례로 간격에 따른 삽입 정렬이 수행된다. 마지막 간격은 반드시 1이어야 한다.(간격에 대해서 그룹별로 삽입 정렬을 수행하였기 때문에 아직 비교되지 않은 다른 그룹의 숫자가 있을 수 있기 때문)

------

#### 코드 설명

1. 먼저 정렬해야 할 리스트를 일정한 기준에 따라 분류
2. 연속적이지 않은 여러 개의 부분 리스트를 생성
3. 각 부분 리스트를 삽입 정렬을 이용하여 정렬
4. 모든 부분 리스트가 정렬되면 다시 전체 리스트를 더 적은 개수의 부분 리스트로 만든 후에 알고리즘을 반복
5. 위의 과정을 부분 리스트의 개수가 1이 될 때까지 반복

#### 코드

```java
    public static void Shell(int[] arr) {
        int gap = arr.length / 2;

        while( gap > 0 ) {
            for( int i = gap; i < arr.length; i++ ) {
                int temp = arr[i];
                int j = i;
                while( j >= gap && arr[j - gap] > temp ) {
                    arr[j] = arr[j - gap];
                    j -= gap;
                }
                arr[j] = temp;
            }
            gap /= 2;
        }
    }
```

#### 시간 복잡도

쉘 정렬은 입력 크기가 매우 크지 않은 경우에 매우 좋은 성능을 보인다.

- 평균 : O(n^1.25)
- 최선 : O(n)
- 최악 : O(n^2)

쉘 정렬의 수행 속도는 간격(gap) 선정에 따라 좌우된다.

=> 쉘 정렬은 간격(gap)을 어떻게 설정하는지에 따라 시간이 크게 달라진다. 간격은 홀수로 하는 것이 좋기 때문에 간격을 절반으로 줄일 때 짝수가 나오면 1을 더해서 홀수로 만들어준다.

## 전체 코드

```java
import java.util.Arrays;
import java.util.Random;

public class Sorting {
    // 버블 정렬(Bubble Sort)
    public static void Bubble(int[] arr) {
        for (int i = 0; i < arr.length - 1; i++) {
            for (int j = 0; j < arr.length - 1; j++) {
                if (arr[j] > arr[j + 1]) {      // 위의 원소가 아래의 원소보다 크면
                    int temp = arr[j + 1];
                    arr[j + 1] = arr[j];
                    arr[j] = temp;              // 서로 자리를 바꾼다
                }
            }
        }

        System.out.println("버블 정렬 : ");
        PrintArr(arr);
    }

    // 선택 정렬(Selection Sort)
    public static void Selection(int[] arr) {
        for (int i = 0; i < arr.length - 1; i++) { // arr.length - 1 : 마지막 요소는 자연스럽게 정렬됨
           int min = i;        // A[i]를 최솟값으로 놓는다
            for (int j = i + 1; j < arr.length; j++) // A[i] ~ A[n - 1]에서 최솟값을 찾는다
                if (arr[min] > arr[j])
                    min = j;
            int temp = arr[min];
            arr[min] = arr[i];
            arr[i] = temp;                  // for 루프에서 찾은 최솟값 A[min]을 A[i]와 교환
        }

        System.out.println("선택 정렬 : ");
        PrintArr(arr);
    }

    // 삽입 정렬(Insertion Sort)
    public static void Insertion(int[] arr) {
        int j = 0;
        for (int i = 1; i < arr.length; i++) {
            int temp = arr[i];      // 정렬 안 된 부분의 가장 왼쪽 원소
            for (j = i - 1; j >= 0 && temp < arr[j]; j--)
                arr[j + 1] = arr[j];
            arr[j + 1] = temp;
        }

        System.out.println("삽입 정렬 : ");
        PrintArr(arr);
    }

    // 쉘 정렬(Shell Sort)
    public static void Shell(int[] arr) {
        int gap = arr.length / 2;

        while( gap > 0 ) {
            for( int i = gap; i < arr.length; i++ ) {
                int temp = arr[i];
                int j = i;
                while( j >= gap && arr[j - gap] > temp ) {
                    arr[j] = arr[j - gap];
                    j -= gap;
                }
                arr[j] = temp;
            }
            gap /= 2;
        }

        System.out.println("쉘 정렬 : ");
        PrintArr(arr);
    }

    // 랜덤으로 입력된 배열
    public static void Random(int n){
        int[] R = init(n);
        System.out.println("랜덤 배열 : ");
        PrintArr(R);
        Bubble(R);
        Selection(R);
        Insertion(R);
        Shell(R);
        System.out.println();
    }

    // 랜덤 배열 초기화
    public static int[] init(int n) {
        Random random = new Random();

        int[] arr = new int [n];

        for (int i = 0; i < n; i++)
            arr[i] = random.nextInt(100);

        return arr;
    }

    // 오름차순 정렬된 배열을 순서를 살짝만 바꿔줌
    public static void Asc(int n){
        int[] Asc = init(n);
        Arrays.sort(Asc);       // 오름차순 정렬

        Shuffle(Asc);
        System.out.println("이미 오름차순 정렬된 데이터에서 순서가 조금 바뀐 배열 : ");
        PrintArr(Asc);
        Bubble(Asc);
        Selection(Asc);
        Insertion(Asc);
        Shell(Asc);
        System.out.println();
    }

    // 배열 섞기
    public static int[] Shuffle(int[] arr){
        int r1, r2;
        int temp;
        // 정렬된 배열 크기의 10퍼센트만 데이터를 바꿔준다
        for(int i = 0; i < arr.length * 0.1; i++){
            // for문이 돌아갈 때마다 배열 크기의 범위에서 랜덤으로 바뀌는 난수
            r1 = (int)(Math.random() * arr.length);
            r2 = (int)(Math.random() * arr.length);

            temp = arr[r1];
            arr[r1] = arr[r2];
            arr[r2] = temp;
        }

        return arr;
    }

    // 내림차순 정렬된 배열
    public static void Desc(int n){
        int[] Desc = init(n);

        for(int i = 0; i < Desc.length; i++)
            for(int j = i + 1; j < Desc.length; j++){
                if(Desc[i] < Desc[j]){
                    int temp = Desc[j];
                    Desc[j] = Desc[i];
                    Desc[i] = temp;

                }
                else
                    break;
            }

        System.out.println("내림차순 정렬된 배열 : ");
        PrintArr(Desc);
        Bubble(Desc);
        Selection(Desc);
        Insertion(Desc);
        Shell(Desc);
        System.out.println();
    }

    // 배열 출력
    public static void PrintArr(int[] arr){
        for(int i = 0; i < arr.length; i++)
            System.out.print(arr[i] + "\t");
        System.out.println();
    }

    public static void main(String[] args) {
        Random random = new Random();

        int n = random.nextInt(20);     // 배열 크기
        if(n == 0)						// 배열의 크기가 0이라면 난수를 다시 불러온다
            n = random.nextInt(20);

        Random(n);
        Asc(n);
        Desc(n);
    }
}
```

#### 실행 결과

![image](https://user-images.githubusercontent.com/80511341/117117571-aa793000-adca-11eb-8504-d6931d907fcd.png)



## 성능 분석

#### 시간 차이 구하기

```java
        long beforetime = System.nanoTime();
		/*
		함수 실행
		*/
        long aftertime = System.nanoTime();
        long difftime = (aftertime - beforetime);
        System.out.println("시간 차이 : " + difftime);
```



##### 아예 랜덤한 데이터

| 배열 크기      | 100    | 200    | 300    | 400    | 500    | 600    | 700    | 800    | 900    | 1000    |
| -------------- | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------- |
| 버블 시간 차이 | 320000 | 955800 | 457700 | 447300 | 637800 | 543900 | 703700 | 797000 | 880400 | 1001100 |
| 선택 시간 차이 | 107600 | 393400 | 241100 | 343100 | 542500 | 96300  | 116200 | 219600 | 90300  | 110600  |
| 삽입 시간 차이 | 3500   | 7100   | 11900  | 15100  | 18800  | 17600  | 20300  | 28200  | 26800  | 33200   |
| 쉘 시간 차이   | 13700  | 37700  | 68100  | 90400  | 118100 | 123900 | 148900 | 219000 | 25000  | 40200   |



##### 이미 정렬되었지만 배열 크기의 10퍼센트만 순서를 바꿔서 어느 정도만 정렬된 데이터

| 배열 크기      | 100    | 200    | 300    | 400    | 500    | 600    | 700    | 800    | 900    | 1000   |
| -------------- | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 버블 시간 차이 | 199500 | 517100 | 416800 | 383700 | 413700 | 483500 | 337500 | 461500 | 386700 | 749300 |
| 선택 시간 차이 | 79600  | 399900 | 197200 | 343700 | 322600 | 97600  | 166000 | 80100  | 86200  | 190100 |
| 삽입 시간 차이 | 3300   | 7300   | 10900  | 14200  | 14500  | 17900  | 27200  | 29500  | 29500  | 36400  |
| 쉘 시간 차이   | 13300  | 39200  | 70800  | 94700  | 116600 | 123300 | 187100 | 39900  | 28900  | 53100  |

##### 내림차순으로 정렬된 데이터

| 배열 크기      | 100    | 200    | 300    | 400    | 500    | 600    | 700    | 800    | 900    | 1000    |
| -------------- | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------- |
| 버블 시간 차이 | 308000 | 280300 | 462100 | 442100 | 443400 | 560300 | 663000 | 810400 | 907600 | 1240100 |
| 선택 시간 차이 | 78700  | 398900 | 193900 | 352500 | 89100  | 96100  | 200500 | 108400 | 134100 | 202600  |
| 삽입 시간 차이 | 3300   | 7300   | 10700  | 14600  | 15400  | 18700  | 25800  | 29100  | 33600  | 39000   |
| 쉘 시간 차이   | 14000  | 41300  | 68800  | 94000  | 87600  | 122500 | 183600 | 47000  | 31100  | 57100   |
