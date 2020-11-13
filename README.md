# 숫자 야구 게임
## 진행 방법
* 숫자 야구 게임 요구사항을 파악한다.
* 요구사항에 대한 구현을 완료한 후 자신의 github 아이디에 해당하는 브랜치에 Pull Request(이하 PR)를 통해 과제를 제출한다.

## 과제 제출 과정
* [과제 제출 방법](https://github.com/next-step/nextstep-docs/tree/master/precourse)


## 기능 요구사항

- 컴퓨터가 1부터 9까지 서로 다른 수로 이루어진 3자리의 수를 만든다.
- 사용자가 3자리의 숫자를 입력한다.
  - 같은 수가 같은 자리에 있으면 스트라이크
  - 같은 수가 다른 자리에 있으면 볼
  - 같은 수가 없으면 포볼 또는 낫씽
- 3자리의 수를 맞추기 전 까지 반복되고, 맞추면 게임이 종료되고, 새로 시작할지 종료할지 선택한다.
  - 1을 입력하면 게임을 새로 시작한다.
  - 2를 입력하면 완전히 종료한다.
  
## 객체 간단 모델링

### domain.AnswerNumber

- 사용자가 맞춰야 하는 수를 담은 객체
- (number)
- 3자리의 서로 다른 수를 가져야 한다.
- [x] 3자리의 서로 다른 숫자를 생성한다.
- [x] 숫자가 3자리를 가지면 true를 리턴한다.
- [x] 각 자리수에 같은 숫자가 있으면 true를 리턴한다.

### domain.UserNumber

- 사용자가 입력한 수를 담은 객체
- (number)
- 3자리의 서로 다른 수를 가져야 한다.
- [ ] 3자리를 가지지 않으면 예외를 발생시킨다.
- [ ] 각 자리수가 같은 숫자가 있으면 예외를 발생시킨다.

### domain.Referee

- UserNumber와 AnswerNumber를 비교해 스트라이크, 볼, 낫띵 을 판별하는 객체
- (userNumber, answerNumber)
