# 동적 프로그래밍(Dynamic Programmaing)

문제의 크기를 변화하면서(Dynamic) 정답을 계산하는데(Programming), 작은 문제의 결과를 이용해 큰 문제의 정답을 빠르게 계산하는 알고리즘

- 동적 프로그래밍 접근 시도
    - 문제가 원하는 정답을 찾기 위해 가장 먼저 **완전 탐색** 접근을 시도해본다.
    - 근데 완전 탐색 과정에서, **탐색 경우가 지나치게 많은 경우**,
    - 모든 경우를 빠르게 탐색하는 방법으로 **Dynamic Programming을 시도**해 볼 수 있다.

      → **규격화** 된 문제 풀이 순서를 외워 훈련해야한다.

- 동적 프로그래밍의 **규격화**된 방법
    1. **풀고싶은 가짜 문제 정의**
        - 문제 크기 N을 변수로 만들어서 표기하는 경우
            - dy[i] = 1~i 번 원소에 대해 조건을 만족하는 경우의 수
            - dy[i][j] = i ~ j 번 원소에 대해 조건을 만족하는 최대값
            - dy[i][j] = 수열[1..i]][1…j]에 대해 무언가를 계산한 값
        - 문제 크기 N과 마지막 상태를 함께 기록해주는 경우
            - dy[i][0] = i-1 번째 계단을 밟지 않고 i 번째 계단에 도착하여 얻는 최대 점수
            - dy[i][1] = i-1 번째 계단을 밟고서 i번째 계단에 도착하여 얻는 최대 점수
            - dy[i][last] = 길이가 i 이며 last로 끝나는 오르막수의 개수
        - 구간 L ~ R에 대한 문제를 해결할 때
        - 2차원 격자 배열에서 문제를 해결할 때
        - 트리 구조에서 문제를 해결 할 때
    2. **가짜 문제를 풀면 진짜 문제를 풀 수 있는가?**

       예시)

       진짜 문제 : 수열 A[1…N] 에서 조건을 만족하는 부분 수열의 개수

       가짜 문제 : dy[i] = 수열 A[1..i] 에서 조건을 만족하는 부분 수열의 개수

       가짜 문제를 푼다면, dy[1],dy[2] .. dy[N]을 모두 계산 했을 테니, dy[N]에 적혀 있는 값이 곧 진짜 문제가 원하는 값이다.

    3. **초기값을 어떻게 되는가?**

       가장 작은 문제 해결하기

       동적 프로그래밍은 **작은 문제인 초기값을 이용해서 큰 문제를 해결해간다.**

    4. **점화식 구하기**

       초기값 계산한 것을 기반으로 점점 큰 문제들을 해결해가며 dy 배열을 가득 계산하는 과정

    5. **진짜 문제 정답 출력하기**

       1 ~ 4 를 성공적으로 끝낸다면 dy 배열을 이용해 진짜 문제 해결하기

- 동적프로그래밍은 규격화된 형태가 있다. 그 형태를 성공만 하면 코딩의 양은 적다.

- [BOJ_9095](https://www.acmicpc.net/problem/9095)

  > 정수 n이 주어졌을 때, n을 1,2,3의 합으로 나타내는 방법의 수를 구하기
  순서가 다르면 다른 경우의 수로 판단
  >
    - 동적 프로그래밍의 접근
        - 완전 탐색 접근
            - 완전 탐색을 통해 모든 경우를 하나하나 찾아내보자.

              → N이 커질수록 탐색 경우가 엄청 많아진다.

        ---
        
        1. 풀고 싶은 가짜 문제 정의
            - hint) 진짜 문제 먼저 써보기
            - 진짜 문제 : 주어진 N에 대해 N을 1,2,3으로 표현하는 경우의 수
            - 가짜 문제 : dy[i] = i를 1,2,3의 합으로 표현하는 경우의 수
        2. 가짜 문제를 풀면 진짜 문제를 풀 수 있는가?
            - dy 배열을 가득 채울 수 있다면 진짜 문제에 대한 대답은 dy[N]이다.
        3. 초기값은 어떻게 되는가.
            - 초기값 : 쪼개지 않아도 풀 수 있는 ‘작은 문제’들에 대한 정답
                
                ![스크린샷 2022-10-29 오후 6.16.54.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8d8a81b7-82d3-470a-91ff-6f0ccf8d5095/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-10-29_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_6.16.54.png)
                
        4. 점화식 구해내기
            - dy[i] 계산에 필요한 탐색 경우를 **공통점끼리 묶어내기** (**Partitioning**)
                - 마지막에 어떤 숫자를 더했는지
            - 묶어낸 부분의 정답을 dy 배열을 이용해 빠르게 계산
                - 전체 경우의 수 = 각 Patition의 경우의 수 들의 합
                - dy[i] 계산에 필요한 탐색 경우들 
                    
                    | 마지막에 1을 
                    더하는 경우의 수 
                               =
                    합이 i-1인 경우들 | 마지막에 2를 
                    더하는 경우의 수
                               =
                    합이 i-2인 경우들 | 마지막에 3을 
                    더하는 경우의 수
                               =
                    합이 i-3인 경우들 |
                    | --- | --- | --- |
                    | dy[i-1] | dy[i-2] | dy[i-3] |
                - **dy[i] = dy[i-1] + dy[i-2] + dy[i-3]**
    - 시간 복잡도
        - dy 배열을 1번지부터 N번지  까지 채우는 것은 O(N) 이라는 시간복잡도면 충분하다.
    - 구현
        - 전처리(preprocessing) 하고, 입력 받으면 바로 결과값이 도출 되도록 구현
        
        ```java
        static int[] dy;
        
        static void preprocess(){
        	dy = new int[15];
        	// TODO : 초기값 구하기
        	dy[1] = 1;
        	dy[2] = 2;
        	dy[3] = 4;
        
        	// TODO : 점화식을 토대로 dy 배열 채우기
        	for(int i=4;i<=11;i++){
        		dy[i] = dy[i-1]+dy[i-2]+dy[i-3];
        	}
        }
        ```
      
