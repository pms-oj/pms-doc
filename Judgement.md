## 채점 방식(Batch)

TODO

## 채점 방식(OutputOnly)

TODO

## 채점 방식(Communication)

IOI의 CMS 채점 방식과 유사한 방식을 따른다.

### 채점 준비

pms-master가 할당된 pms-slave에게 사용자에게 요청된 파일, `{checker file}`, `{manager file}`을 각각 설정된 언어의 UUID와 함께, 채점이 요청된 언어의 UUID를 `${uuid}`라고 하면, `graders/${uuid}`폴더를 `gzip`으로 압축하여 보낸다.

### pms-slave에 도달

pms-slave는 `{checker file}`과 `{manager file}`을 컴파일하고 `graders/${uuid}`를 임시 디렉토리 `${tmp}`에서 압축 해제한다.
그리고, `${tmp}`에 사용자에게 요청된 파일을 복사하고 (격리된 공간 요구 안됨) `${tmp}`에서 `make`를 실행한다. (GNU make 권장)
이때 나오는 파일은 모두 단일 파일이어야 한다. (`stub.toml`에서 설정됨)

### 채점 과정

`isolate` 샌드박스에서 `{manager file}`과 `stub`을 컴파일해서 생성된 실행 파일을 pipe먹여서 실행한다. (이때, `{manager file}`은 항상 arguments를 `<stdin 파일> <stdout 파일 지정>` 으로 받아야한다)
그리고, `isolate` 샌드박스에서 `{checker file}`을 컴파일해서 생성된 실행 파일을 `<stdin 파일> <stdout 파일> <**원본** stdout 파일> <보고 파일> -appes` arguments로 실행한다. (IOI를 위해 수정된 testlib 사용을 권장한다)
그리고 RTE, TLE, MLE 등의 요인이 발생하지 않은 이상 출력된 보고 파일을 전송한다.(XML, `JudgeState::Report`)

### 채점 완료

pms-master는 slave로부터 받은 결과를 바탕으로 사용자에게 피드백을 제공한다.

## 채점 방식(TwoStep)

TODO