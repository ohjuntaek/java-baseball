# 숫자 야구 게임
## 진행 방법
* 숫자 야구 게임 요구사항을 파악한다.
* 요구사항에 대한 구현을 완료한 후 자신의 github 아이디에 해당하는 브랜치에 Pull Request(이하 PR)를 통해 과제를 제출한다.

## 과제 제출 과정
* [과제 제출 방법](https://github.com/next-step/nextstep-docs/tree/master/precourse)


## 기능 요구사항

<숫자 야구 게임>

- 컴퓨터가 1부터 9까지 서로 다른 수로 이루어진 3자리의 수를 만든다.
- 사용자가 3자리의 숫자를 입력한다.
  - 같은 수가 같은 자리에 있으면 스트라이크
  - 같은 수가 다른 자리에 있으면 볼
  - 같은 수가 없으면 ~~포볼 또는~~ 낫씽
- 3자리의 수를 맞추기 전 까지 반복되고, 맞추면 게임이 종료되고, 새로 시작할지 종료할지 선택한다.
  - 1을 입력하면 게임을 새로 시작한다.
  - 2를 입력하면 완전히 종료한다.
  
## 용어 사전

| 용어 | 의미 | 동의 용어들
| --- | -------------- | --- |
| 게임 숫자 | 숫자 야구 게임에서 사용하는 세 자리 수의 숫자 | 숫자 야구 게임 숫자/수 |
| 숫자 | 일반적인 의미의 숫자 | 수 |
| 정답 | 하나의 숫자 야구 게임에서 맞춰야하는 게임 숫자 | 정답 게임 숫자 |
| 매치 타입 | 스트라이크, 볼 | 일치 유형 |
| 매치 카운트 | ex) 2 스트라이크면 매치 카운트는 2 이다. | |
| 추측 | 유저가 게임 숫자를 입력해 정답을 맞추기 위해 하는 행위, 추측 결과를 반환한다 | |
  
## 객체 모델링

> - 정의한 객체는 _이탤릭체_ 로 나타냈습니다.
>   - 테스트 로직 안에서는 이탤릭체 생략, 괄호로 객체의 영어명 기입 
> - 용어 사전에서 정의한 용어는 `백틱`으로 강조했습니다.

### GameDigit (한 자리 게임 숫자)

- 숫자 야구 게임에서 사용하는 한 자리 수를 가진 객체
- (int digit)
- [x] 생성 시 한 자리의 숫자가 아니면 예외를 발생시킨다.

### GameDigitRepository (게임 숫자 저장소)

- 0 부터 9 까지의 _한 자리 게임 숫자(GameDigit)_ 를 가지고 있는 객체.
- [x] 숫자로 된 문자열을 받아서 한 자리 게임 숫자(GameDigit) 리스트를 반환한다.
- [x] 입력한 개수 만큼의 중복 되지 않는 한 자리 게임 숫자(GameDigit) 를 제공한다.

### MatchType (매치 타입)

- 스트라이크, 볼 여부
- 스트라이크(STRIKE)
  - 같은 수가 같은 자리에 있으면 스트라이크
- 볼(BALL)
  - 같은 수가 다른 자리에 있으면 볼
- 매치 없음(NO_MATCH)
  - 스트라이크도 아니고 볼도 아님

### GameNumber (게임 숫자)

- ([GameDigit] digits)
- GameDigit 일급 컬렉션
- 항상 3개의 서로 다른 _한 자리 게임 숫자_ 를 가지고 있다.
  - 3개의 서로 다른 _한 자리 게임 숫자_ = digits
- [x] 생성 시 3개의 한 자리 게임 숫자(GameDigit) 를 가지지 않으면 예외를 발생시킨다.
- [x] 생성 시 중복된 한 자리 게임 숫자(GameDigit) 가 있으면 예외를 발생시킨다.
- [x] 한 자리 게임 숫자(GameDigit) 를 받아서 자신이 가진 digits 에 대해 매치 타입(MatchType) 을 반환한다.

### BaseballGame (숫자 야구 게임)

- 한 게임당 랜덤으로 새롭게 생성된 `정답 게임 숫자` 하나를 가진다.
- [x] 게임을 새로 시작한다 <> 랜덤한 게임 숫자(GameNumber) 를 `정답`으로 가진 숫자 야구 게임(BaseballGame) 을 제공한다.
- [x] 유저가 입력한 게임 숫자(GameNumber) 를 받아 정답 추측 결과(GuessResult) 를 제공한다.

### GuessResult ((정답) 추측 결과)

- 한 `추측`에 대해 매치 타입 별로 매치 카운트를 가지고 있는 객체
- 즉, 스트라이크는 몇개고 볼은 몇 개 인지 가지고 있는 객체
- (MatchTypeCounts)
- [x] 스트라이크 개수를 제공한다.
- [x] 볼 개수를 제공한다.
- [ ] 3 스트라이크 여부를 제공한다.
- [ ] 낫띵 여부를 제공한다.
- [ ] 입력 받은 _매치 타입_ 의 `매치 카운트`를 증가시킨다.

### MatchTypeCounts (매치 타입 카운트)

- (Map<MatchType, Integer> countByMatchTypes) 를 갖고 있는 일급 컬렉션
- [ ] _매치 타입_ 별로 `매치 카운트`를 제공한다.
- [ ] 입럭받은 _매치 타입_ 의 `매치 카운트` 를 증가시킨다.

### BaseballGameMachine

- 숫자 야구 게임을 _추측 결과_ 와 유저 입력에 따라 새로 시작하고 종료시키는 객체
- 숫자 야구 게임 지속 여부(baseballGameContinue)를 가지고 있다.
- (BaseballGame baseballGame, boolean baseballGameContinue)
- [ ] 숫자 야구 게임을 시작한다.
- [ ] 유저가 입력한 _게임 숫자_ 를 받아 _추측 결과_ 를 반환한다.
- [ ] _추측 결과_ 에 따라 `추측` 을 계속할지 말지 여부를 제공한다.
- 유저의 입력에 따라 숫자 야구 게임 지속 여부의 값을 결정한다.
  - [ ] 유저가 1을 입력하면 숫자 야구 지속 여부를 true로 하고 새로운 숫자 야구 게임을 실행한다.
  - [ ] 유저가 2를 입력하면 숫자 야구 지속 여부를 false로 한다.
- [ ] 숫자 야구 게임 지속 여부를 제공한다.

---

- GameNumber랑 GameDigit 랑 구분한 이유
  - 처음엔 GameNumbers(게임 숫자들), GameNumber(게임 숫자)를 쓸려 했으나,
   정답인 게임 숫자들, 유저가 입력한 게임 숫자들이라고 부를려니 의미가 안 맞는 거 같아 구분함.