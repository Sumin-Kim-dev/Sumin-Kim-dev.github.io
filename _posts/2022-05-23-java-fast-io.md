---
title:  "[Java] 빠른 입출력 : BufferedReader / BufferedWriter"
categories: Java
tags: BufferedReader BufferedWriter StringTokenizer
last_modified_at: 2022-05-23 +0900
toc: true
toc_sticky: true
---

BufferedReader, BufferedWriter가 Scanner, print보다 훨씬 빠른 입출력을 제공한다.  
본인의 코드에서 시간이 문제가 된다면 입출력 방식을 바꿔보도록 하자.

## BufferedReader

버퍼를 사용하는 입력으로, Scanner보다 훨씬 빠른 속도를 자랑한다.  
Scanner와 크게 두 가지 차이점이 있다.

- 오직 엔터만을 경계로 인식한다.  
  - 스페이스 바 등을 경계로 인식하지 않는다.
  - StringTokenizer.nextToken(String s)로 추가적인 처리를 해야하는 경우도 있다.

- 입력된 값을 문자열로만 인식한다.  
  - int 등 다른 자료형으로 입력을 변환시키는 과정이 필요하다.
  - Integer.parseInt(String s)등을 사용하면 된다.

## BufferedWriter

버퍼를 사용하는 출력으로, print보다 속도가 빠르다.  
개행이 필요하다면 BufferedWriter.newLine()을 사용하면 된다.

## 예시 코드

[백준 15552번 - 빠른 A+B(Bronze 2)](https://www.acmicpc.net/problem/15552)의 정답 코드이다.

```java
import java.io.*;
import java.util.StringTokenizer;
public class Main {
    public static void main(String args[]) throws IOException{
        BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int t = Integer.parseInt(bf.readLine());
        
        StringTokenizer st;
        for(int i = 0; i < t; i++) {
            st = new StringTokenizer(bf.readLine());
            bw.write(Integer.parseInt(st.nextToken())+Integer.parseInt(st.nextToken()) + "");
            bw.newLine();
        }
        bw.flush();
        bw.close();
    }
}
```

BufferedReader도 close()해줘야 할 것 같은데, 이 문제 풀 때는 몰랐었다.  
BufferedWriter의 경우 위 코드에서는 flush()와 close()를 둘 다 사용했는데, close()가 flush()를 포함하고 있다. 이 문제 같은 경우는 close()만 써도 된다.
