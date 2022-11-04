---
title:  "[우아한테크코스] 5기 프리코스 1주차(온보딩) 회고"
categories: woowacourse
tags: 프리코스 회고
date : 2022-11-02 22:23
last_modified_at: 2022-11-05
toc: true
toc_sticky: true
---

![우아한테크코스](/assets/img/woowacourse.jpg "우아한테크코스"){: .center}

우아한테크코스 5기에 지원했다.  
4기까지는 코딩테스트와 지원서를 통해 한 번 걸러서 프리코스 참여자를 선정했는데, 이번에는 지원서를 낸 모두에게 프리코스 참여 기회가 주어졌다.  

## 프리코스 1주차(온보딩) 미션 내용과 내가 제출한 코드

프리코스 1주차 문제 : [프리코스 1주차(온보딩)](https://github.com/woowacourse-precourse/java-onboarding)  
내가 제출한 코드 : [제출한 코드](https://github.com/Sumin-Kim-dev/java-onboarding/tree/sumin-kim-dev)

## 프리코스 1주차(온보딩) 미션을 받고

4기까지의 프리코스 1주차는 숫자 야구 미션이었다.
 개인적으로 공부하면서 숫자 야구를 한번 구현해봤고, 1주차 제출날까지는 개인적으로 바쁜 일도 있었기 때문에 좀 편하게 할 수 있겠지라고 생각을 하고 있었는데...

정작 프리코스 시작 당일, 10월 26일 오후 3시에 열어본 미션 내용은 기존과 완전히 달랐다.
일단 제목부터 온보딩이었고, 내용을 보니 코딩 테스트에서나 볼 법한 문제 7개가 있었다.
기존에 코딩테스트 준비를 해왔기는 해서 크게 어렵다고 느끼지는 않았으나, 좀 당황스러웠다.
아무래도 기존의 코딩테스트가 프리코스 1주차로 대체된 것으로 보인다.

## 미션을 진행하는 동안

우아한테크코스 측에서 지원자들끼리 소통할 수 있는 슬랙을 열어주었다.
사실 원래 개설 의도대로면 미션과 관련된 질문을 하면 안되는 공간이지만, 첫주차에는 이게 지켜지지 않았다.
그래서 미션의 요구 조건 해석과 관련된 질답들이 매우 많았고, 테스트 케이스 공유도 이루어졌다.

내가 미션을 해석하면서 고민했던 것은 크게 두가지였다.

### 입력에 대한 예외 처리를 해야하는가?

사실 1번 문제의 경우에는 예외 처리를 따로 할 의미가 없기는 하다.
문제 조건에 예외는 -1을 반환하라고 적혀있기 때문이다.
나머지 문제들이 애매했는데, 나는 입력에 대한 예외 처리를 전부 하기로 했다.
덕분에 코드가 전체적으로 길어지긴 했다.

### 문제의 애매한 조건을 어떻게 처리할 것인가?

1번 문제 게임 규칙 6번, 시작 면이나 마지막 면이 나오도록 책을 펼치지 않는다. 조건의 해석이 애매했다.
일단 나는 1과 400이 나오지 않는다는 의미로 해석했다.
실제로 이 조건에 대한 질문이 슬랙에 1주차 진행 기간 내내 많이 올라오기도 했다.
이외에 2번 문제에서 "baabb"는 빈 문자열 ""이 되는가 "b"가 되는가도 논란이 된적이 있는데, 이건 문제 설명에 따르면 b가 맞다는 쪽으로 결론이 났었다.

## 미션을 수행하면서 배운 것

사실 나는 앞에서 말했듯이 1주차에는 시간이 좀 부족했다.
그래서 코드에 전체적으로 많이 신경을 쓰지 못했는데, 그래도 배운 점은 많았다.

### 1. 정규식

입력 예외 처리를 전부 하려다보니 문자열을 다룰 일이 많아졌다.
처음 2번 문제를 풀 때는 소문자로 이루어져 있는지만 확인하면 끝이라, 일단 대충 아래처럼 짰는데...

```java
static boolean validation(String cryptogram) {
    int length = cryptogram.length();
    if (length == 0 || length > 1000) return false;
    for (char c : cryptogram.toCharArray()) {
    if (!Character.isLowerCase(c)) return false;
    }
    return true;
}
```

6번 문제의 예외 처리를 하려고 보니 한글 검증을 해야한다.
이건 위의 방식으로는 답이 없겠다 싶어서 구글링을 막 해본 결과, 정규식에 대해 알게 되었다.

내가 짠 정규식을 사용한 6번 문제의 한글 검증 부분 코드는 아래와 같다.

```java
static boolean violationNickname(String nickname) {
    if (nickname.length() == 0 || nickname.length() >= 20) return true;
    String regex = "^[ㄱ-ㅎㅏ-ㅣ가-힣]*$";
    return !Pattern.matches(regex, nickname);
}
```

문제를 다 풀고 리팩토링을 하면서, 2번 문제의 소문자 검증도 정규식을 활용하도록 바꾸기도 했다.

### 2. 함수 분할

이번 미션의 요구 사항은 아니긴 한데, 작년 미션 요구 사항에 있던 "인덴트 depth를 2 이하로 맞추기"와 "함수의 길이가 15줄을 넘지 않을 것"을 최대한 지키려고 했더니 함수 분할이 반드시 필요했다.

처음에 짠 7번 코드의 일부

```java
public static List<String> solution(String user, List<List<String>> friends, List<String> visitors) {
    if (violateId(user)) return Collections.emptyList();
    if (violateFriends(friends)) return Collections.emptyList();
    if (violateVisitors(visitors)) return Collections.emptyList();

    Map<String, Integer> score = new HashMap<>();
    Map<String, Set<String>> friendMap = setFriendMap(friends);
    Set<String> myFriends = friendMap.getOrDefault(user, new HashSet<>());
    for (String other : friendMap.keySet()) {
        if (other.equals(user)) continue;
        if (myFriends.contains(other)) continue;
        friendMap.get(other).retainAll(myFriends);
        score.put(other, friendMap.get(other).size() * 10);
    }

    for (String visitor : visitors) {
        if (visitor.equals(user)) continue;
        if (myFriends.contains(visitor)) continue;
        score.put(visitor, score.getOrDefault(visitor, 0) + 1);
    }

    return score.keySet()
        .stream()
        .sorted((o1, o2) -> {
            int score1 = score.getOrDefault(o1, 0);
            int score2 = score.getOrDefault(o2, 0);
            if (score1 != score2) {
            return score2 - score1;
            }
            return o1.compareTo(o2);
        })
        .collect(Collectors.toList())
        .subList(0, Math.min(score.size(), 5));
    }
```

딱 봐도 길이가 너무 길다.  
아무리 명백한 요구 사항이 없었다고는 하지만 이건 아닌 것 같아서, 실제 제출 때는 점수를 구하는 부분과 추천 리스트를 구하는 부분으로 쪼개서 제출했다.

실제 제출 코드의 일부

```java
public static List<String> solution(String user, List<List<String>> friends, List<String> visitors) {
        final List<String> ERROR = Collections.emptyList();
        if (violateId(user)) return ERROR;
        if (violateFriends(friends)) return ERROR;
        if (violateVisitors(visitors)) return ERROR;

        return recommendList(scores(user, friends, visitors));
    }

    static Map<String, Integer> scores(String user, List<List<String>> friends, List<String> visitors) {
        Map<String, Integer> scores = new HashMap<>();
        Map<String, Set<String>> friendMap = setFriendMap(friends);
        Set<String> myFriends = friendMap.getOrDefault(user, new HashSet<>());
        for (String other : friendMap.keySet()) {
            if (other.equals(user)) continue;
            if (myFriends.contains(other)) continue;
            friendMap.get(other).retainAll(myFriends);
            scores.put(other, friendMap.get(other).size() * 10);
        }

        for (String visitor : visitors) {
            if (visitor.equals(user)) continue;
            if (myFriends.contains(visitor)) continue;
            scores.put(visitor, scores.getOrDefault(visitor, 0) + 1);
        }
        return scores;
    }

    // 친구추천점수가 주어졌을 때 가장 높은 점수 5명(0점 아닌 인원이 5명 아래면 전부) 출력
    static List<String> recommendList(Map<String, Integer> scores) {
        List<String> recommendList = scores.keySet()
                .stream()
                .filter(o -> scores.get(o) > 0)
                .sorted((o1, o2) -> {
                    int score1 = scores.get(o1);
                    int score2 = scores.get(o2);
                    if (score1 != score2) {
                        return score2 - score1;
                    }
                    return o1.compareTo(o2);
                })
                .collect(Collectors.toList());
        return recommendList.subList(0, Math.min(recommendList.size(), 5));
    }
```

훨씬 보기도 좋거니와, 고치는 과정에서 추천 점수가 0점인 경우를 빼먹었다는 사실을 발견하기도 했다. 역시 가독성이 좋은 코드가 실수 찾기도 좋다.

### 3. 테스트의 중요성

사실 이 부분은 지금은 폐쇄된 슬랙의 테스트 케이스 채널에서 도움을 좀 받았다.
2번 문제에서 문제를 잘못 이해해서 구현을 잘못한 것도 있었고(하필 주어진 예제 테스트 케이스는 거기에 걸리질 않았다), 7번 문제에서 추천 점수가 0점인 경우를 거르는 걸 빼먹기도 했었고.
테스트 추가로 안해보고 냈으면 진짜 큰일날 뻔했다.

### 4. 작명의 어려움

변수명, 함수명 짓기 진짜 어렵다. 영어를 못해서 더 심한 것 같다. 이름 짓겠다고 구글 번역기를 엄청 쓰기도 했다...

## 미션을 제출하고

시간이 조금만 더 있었다면 하는 아쉬움이 많이 남았다. 위에서 말했듯, 나는 다른 일정과 겹치는 바람에 1주차에는 시간을 많이 쓰지 못했다.
일주일짜리를 거의 하루만에 하다보니 아무래도 리팩토링에 신경을 많이 못 썼다.

1주차의 요구 사항은 아니었지만, 작년 요구 사항을 따라서 구현할 기능 목록 작성 및 기능 단위 커밋을 시도하려 했는데 반만 성공했다.
기능을 쓸데없이 많이 쪼개놓음 + 시간 부족으로 마음이 급하다보니 기능 여러개를 한번에 커밋하는 일이 많았던 것이다.

2주차는 그래도 시간 여유가 좀 있는 만큼, 기능 단위 커밋과 코드 리팩토링에 신경을 더 쓰면서 진행을 해야겠다.