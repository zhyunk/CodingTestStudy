* [프로그래머스](https://school.programmers.co.kr/learn/courses/30/lessons/42748)
* [자바 소스](../../../CoTeStudy/src/programmers/Test02.java)

## K번째수

### **문제 설명**

배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, 
k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면

1. array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
2. 1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
3. 2에서 나온 배열의 3번째 숫자는 5입니다.

배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, 
commands의 모든 원소에 대해
앞서 설명한 연산을 적용했을 때 나온 결과를 
배열에 담아 return 하도록 solution 함수를 작성해주세요.

### 제한사항

- array의 길이는 1 이상 100 이하입니다.
- array의 각 원소는 1 이상 100 이하입니다.
- commands의 길이는 1 이상 50 이하입니다.
- commands의 각 원소는 길이가 3입니다.

### 입출력 예

| array | commands | return |
| --- | --- | --- |
| [1, 5, 2, 6, 3, 7, 4] | [[2, 5, 3], [4, 4, 1], [1, 7, 3]] | [5, 6, 3] |

### 입출력 예 설명

[1, 5, 2, 6, 3, 7, 4]를 2번째부터 5번째까지 자른 후 정렬합니다.    
[2, 3, 5, 6]의 세 번째 숫자는 5입니다.    
[1, 5, 2, 6, 3, 7, 4]를 4번째부터 4번째까지 자른 후 정렬합니다.    
[6]의 첫 번째 숫자는 6입니다.    
[1, 5, 2, 6, 3, 7, 4]를 1번째부터 7번째까지 자릅니다.     
[1, 2, 3, 4, 5, 6, 7]의 세 번째 숫자는 3입니다.   

---

## 나의 접근 방법

먼저 foreach문을 사용해서 array의 제시된 부분을

Arrays 클래스의 copyOfRange( 원본배열 , 시작인덱스 , 끝인덱스 ) 메소드를 사용해

새로운 배열로 복사해온다.

그 다음 Arrays 클래스의 sort 메소드를 사용하여 정렬을 하고

결과를 담을 answer 배열에 제시된 인덱스의 값을 담아준다.

## 내 코드

```java
public int[] test(int[] array, int[][] commands) {
    int[] answer = new int[commands.length];
    int idx = 0;
    for (int[] arg : commands) {
        int[] list = Arrays.copyOfRange(array, arg[0] - 1, arg[1]);
        Arrays.sort(list);
        answer[idx++] = list[arg[2] - 1];
    }

    return answer;
}
```

### 1.  변수 생성

```java
// 결과값을 담을 answer 배열. 배열의 크기는 commands의 크기와 같다
int[] answer = new int[commands.length]; 

// answer의 인덱스 위치를 알려줄 변수
int idx = 0;
```

### 2. 배열 복사

```java
// 향상된 for문(= foreach)을 사용하여 2차배열인 commands의 내부 배열에 접근한다
for (int[] arg : commands) {
		// 새로운 배열 list로 
		// arg에 제시된 범위의 array 값들 복사
    int[] list = Arrays.copyOfRange(array, arg[0] - 1, arg[1]);

		// Arrays 클래스의 sort 메소드를 이용하여 정렬
    Arrays.sort(list);

		// answer 배열에 결과로 출력할 값을 담는다.
    answer[idx++] = list[arg[2] - 1];
}
```

## 다른 사람 코드

출처 : 프로그래머스 스쿨 -  [다른사람 풀이 첫번째](https://school.programmers.co.kr/learn/courses/30/lessons/42748/solution_groups?language=java)  

```java
public int[] test(int[] array, int[][] commands) {
    int[] answer = new int[commands.length];

    for (int i = 0; i < commands.length; i++) {
        int[] list = Arrays.copyOfRange(array, commands[i][0] - 1, commands[i][1]);
        Arrays.sort(list);
        answer[i] = list[commands[i][2] - 1];
    }

    return answer;
}
```
내 코드에서 볼 수 있듯이 나는 idx라는 변수를 새로 생성해서 answer 배열에 사용하였다.    
생각을 조금더 해봤었다면, 내 코드에서 사용된 idx 변수가 결국 commands의 길이 - 1 까지 증가할 것이고,    
그렇게 된다면 굳이 향상된 for문을 사용할 필요 없이   
기본 for문을 사용하는게 더 나았을거라는 생각을 했다.  
프로그래머스에서 가져온 다른 사람의 코드처럼 .. !! 🤓  
좀더 생각을 해보고 코드를 작성해보도록 노력해야겠다.  
앞으로도 화이팅 💪  


