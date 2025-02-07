## 🚀 기능 요구 사항

우아한테크코스에서는 교육생(이하 크루) 간 소통 시 닉네임을 사용한다. 간혹 비슷한 닉네임을 정하는 경우가 있는데, 이러할 경우 소통할 때 혼란을 불러일으킬 수 있다.

혼란을 막기 위해 크루들의 닉네임 중 **같은 글자가 연속적으로 포함** 될 경우 해당 닉네임 사용을 제한하려 한다. 이를 위해 같은 글자가 연속적으로 포함되는 닉네임을 신청한 크루들에게 알려주는 시스템을 만들려고 한다.


신청받은 닉네임 중 **같은 글자가 연속적으로 포함** 되는 닉네임을 작성한 지원자의 이메일 목록을 return 하도록 solution 메서드를 완성하라.

### 제한사항

- 두 글자 이상의 문자가 연속적으로 순서에 맞추어 포함되어 있는 경우 중복으로 간주한다.
- 크루는 1명 이상 10,000명 이하이다.
- 이메일은 이메일 형식에 부합하며, 전체 길이는 11자 이상 20자 미만이다.
- 신청할 수 있는 이메일은 `email.com` 도메인으로만 제한한다.
- 닉네임은 한글만 가능하고 전체 길이는 1자 이상 20자 미만이다.
- result는 이메일에 해당하는 부분의 문자열을 오름차순으로 정렬하고 중복은 제거한다.

### 실행 결과 예시

| forms | result |
| --- | --- |
| [ ["jm@email.com", "제이엠"], ["jason@email.com", "제이슨"], ["woniee@email.com", "워니"], ["mj@email.com", "엠제이"], ["nowm@email.com", "이제엠"] ] | ["jason@email.com", "jm@email.com", "mj@email.com"] |

---
## 📄 기능 목록

### 전체 동작 과정
0. **class TwoLetter** : 중복된 단어인지 확인
   1. **compareTo()** : 오름차순으로 정렬
1. **addAllTwoLettersInTreeSet()** : 닉네임 두글자씩 잘라서 twoLetterTreeSet에 저장
   1. **cutNicknameByTwoLetters()** : 닉네임 두글자씩 자름
   2. **addTwoLettersInTreeSet()** :
      - cutNickname이 각각 Treeset에 저장되어 있는지 확인
      - 저장되어 있다면, TwoLetter.overlap=true로 설정
      - 저장되지 않았다면, 새로 저장
2. **findOverlapNickname** : 중복 닉네임을 가진 이메일 찾음
    1. **cutNicknameByTwoLetters()** : 닉네임 두글자씩 자름
    2. **isOverlapNickname()** : cutNickname의 overlap이 true인지 확인
    3. **overlap==true**인 닉네임 이메일 추출
3. **emailSortAndDeduplication** 오름차순으로 이메일 정렬 & 중복 제거

### 함수별 입출력 및 동작 과정
0. **class TwoLetter**
    - String letter, boolean overlap
    1. **compareTo()**
        : letter를 기준으로 오름차순 정렬
1. **addAllTwoLettersInTreeSet()**
    - 입력 : 크루form (List<List<String>> forms)
    - 동작과정 : 
        - cutNicknameByTwoLetters()
        - addTwoLettersInTreeSet()
        - form 끝날 때까지 반복
2. **cutNicknameByTwoLetters()**
    - 입력 : 닉네임 (String nickname)
    - 동작과정 : HashSet<String> cutNickname에 두글자씩 잘라서 넣음 (중복제거)
    - 출력 : 자른닉네임 (HashSet<String> cutNickname)
3. **addTwoLettersInTreeSet()**
   - 입력 : 자른닉네임 (HashSet<String> cutNickname)
   - 동작과정 :
     - twoLetterTreeSet이 비었다면 cutNickname 저장
     - twoLetterTreeSet에 저장되어 있는 글자인지 확인
     - 저장되어 있다면, overlap을 true로 바꿔줌
     - 저장되지 않았다면, cutNickname 저장
     - cutNickname 끝날 때까지 반복
4. **findOverlapNickname**
   - 입력 : 크루 form (List<List<String>> forms)
   - 동작과정 :
       - cutNicknameByTwoLetters()
       - isOverlapNickname()
       - overlap==true인 닉네임 이메일 추출
   - 출력 :
5. **isOverlapNickname()**
   - 입력 : 자른닉네임 (HashSet<String> cutNickname)
   - 동작과정 : overlap==true가 나오면 중복된 글자이므로 retrun true, 나온 적 없으면 return false
   - 출력 : 중복이면 true, 중복이 아니면 false
6. **emailSortAndDeduplication**
    - 입력 : 이메일 (List<String> email)
    - 동작과정 : 
      - TreeSet에 email 넣음 (중복제거 및 오름차순)
      - TreeSet을 ArrayLsit로 변환
    - 출력 : 이메일 리스트 (Lsit<String> resultEmail)


---
## 💡 기타 내용 정리

### Set
1. HashSet
2. TreeSet
3. LinkedHashSet

### List
1. ArrayList
2. LinkedList
    
