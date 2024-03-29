# 컴퓨터 구조
## 핵심 주제
* 컴퓨터가 이해하는 정보
    * 데이터와 명령어
* 컴퓨터의 네 가지 핵심 부품
    * CPU, 메모리, 보조기억장치, 입출력장치

---

### 문자 인코딩
* 문자 집합 : 컴퓨터가 인식할 수 있는 문자의 모음으로 인코딩 대상
* 유니코드 : 여러 나라의 문자들을 광범위하게 표현할 수 있는 통일된 문자 집합
    * UTF-8으로 다시 인코딩


## 명령어
* 명령어는 연산 코드(연산자)와 오퍼랜드(피연산자)로 구성
* 오퍼랜드 : 연산에 사용할 데이터 또는 연산에 사용할 데이터가 저장된 위치(메모리 주소나 레지스터 이름)
    * 오퍼랜드 필드를 주소 필드라고 부르기도 함
    * 오퍼랜드가 n개인 명령어 -> n-주소 명령어
* 연산 코드 : 명령어가 수행할 연산
    * 대표적인 연산 코드 유형
        1. 데이터 전송
        2. 산술/논리 연산
        3. 제어 흐름 변경
        4. 입출력 제어


### 주소 지정 방식
* 유효 주소 : 연산의 대상이 되는 데이터가 저장된 위치
* 주소 지정 방식 : 연산에 사용할 데이터 위치를 찾는 방법
* 각 주소 지정 방식이 오퍼랜드 필드에 명시하는 값
    1. 즉시 주소 지정 방식 : 연산에 사용할 데이터
        * 메모리 접근 없음
    2. 직접 주소 지정 방식 : 유효 주소(메모리 주소)
        * 메모리 접근 1회
    3. 간접 주소 지정 방식 : 유효 주소의 주소
        * 메모리 접근 2회
    4. 레지스터 주소 지정 방식 : 유효 주소(레지스터 이름)
        * 메모리 접근 없음
    5. 레지스터 간접 주소 지정 방식 : 유효 주소를 저장한 레지스터
        * 메모리 접근 1회


## CPU
* 메모리에 저장된 명령어를 읽어 들이고, 해석하고, 실행하는 장치
* 계산을 담당하는 ALU, 명령어를 읽어 들이고 해석하는 제어장치, 작은 임시 저장 장치인 레지스터로 구성


### ALU
* 레지스터로부터 피연산자를 받아들이고, 제어장치로부터 수행할 연산을 알려 주는 제어 신호를 받아들임
* 연산 수행 후 결괏값은 레지스터에 일시적으로 저장
* 연산 결과에 대한 추가적인 정보를 플래그 레지스터에 저장


### 제어장치
* 제어 신호를 내보내고 명령어를 해석하는 부품
* 제어 신호 : 컴퓨터 부품들을 관리하고 작동시키기 위한 일종의 전기 신호
* 제어 장치가 받아들이는 정보
    1. 클럭 신호
        * 클럭 : 컴퓨터의 시간 단위
    2. 해석해야 할 명령어
        * 명령어 레지스터로부터 명령어를 받아들임
    3. 플래그 레지스터 속 플래그 값
        * 플래그는 ALU 연산에 대한 추가적인 상태 정보
        * 제어장치는 플래그 값을 참고하여 제어 신호를 발생시킴
    4. 제어 버스로 전달된 제어 신호
        * CPU 외부 장치도 제어 신호를 발생시킴
* 제어장치가 내보내는 정보 : CPU 내/외부에 전달하는 제어 신호


### 레지스터
1. 프로그램 카운터 : a.k.a. 명령어 포인터, 메모리에서 읽어 들일 명령어의 주소를 저장
2. 명령어 레지스터 : 메모리에서 읽어 들인, 해석할 명령어를 저장
3. 메모리 주소 레지스터 : 메모리의 주소를 저장
    * CPU가 읽어들이고자 하는 주소 값을 주소 버스로 보낼 때 메모리 주소 레지스터를 거침
4. 메모리 버퍼 레지스터 : a.k.a. 메모리 데이터 레지스터, 메모리와 주고받을 값(데이터와 명령어)을 저장
    * 데이터 버스로 주고받을 값은 메모리 버퍼 레지스터를 거침
5. 플래그 레지스터 : 연산 결과 또는 CPU 상태에 대한 부가적인 정보 저장
6. 범용 레지스터 : 다양하고 일반적인 상황에서 자유롭게 사용 가능
7. 스택 포인터 : 메모리 스택 영역에 있는 스택의 꼭대기 주소 저장
    * 스택 주소 지정 방식 : 스택과 스택 포인터를 이용한 주소 지정 방식
8. 베이스 레지스터 : 베이스 레지스터 주소 지정 방식에 이용됨
    * 변위 주소 지정 방식
        * 오퍼랜드 필드의 값(변위)과 특정 레지스터의 값을 더하여 유효 주소를 얻어내는 주소 지정 방식
        * 상대 주소 지정 방식 : 오퍼랜드와 프로그램 카운터의 값을 더하여 유효 주소를 얻는 방식
        * 베이스 레지스터 주소 지정 방식 : 오퍼랜드(변위)와 베이스 레지스터의 값(기준 주소)을 더하여 유효 주소를 얻는 방식


### 명령어 사이클과 인터럽트
* 명령어 사이클 : CPU가 하나의 명령어를 처리하는 주기로, 인출, 실행, 간접, 인터럽트 사이클로 구성
    * 인출 사이클 : 명령어를 메모리에서 CPU로 가져오는 단계
    * 실행 사이클 : CPU로 가져온 명령어를 실행하는 단계로, 제어장치가 명령어 레지스터에 담긴 값을 해석하고 제어 신호를 발생시킴
    * 간접 사이클 : 명령어를 실행하기 위해 메모리 접근이 더 필요한 경우 이를 수행하는 단계
    * 인터럽트 사이클 : 아래 내용 참고


* 인터럽트 : CPU의 정상적인 작업을 방해하는 신호
    * 동기 인터럽트와 비동기 인터럽트로 구분
    * 동기 인터럽트(예외) : CPU가 명령어 처리 중 예외적인 상황에 마주쳤을 때 발생하는 인터럽트
    * 비동기 인터럽트(하드웨어 인터럽트) : 입출력장치에 의해 발생하는 인터럽트로 알림과 같음
        * CPU가 입출력 작업 도중에도 효율적으로 명령어를 처리할 수 있게 해줌


* 하드웨어 인터럽트 처리 순서
    1. 입출력장치가 CPU에 인터럽트 요청 신호를 보냄
    2. CPU가 실행 사이클과 인출 사이클 사이에 항상 인터럽트 여부를 확인
    3. CPU가 인터럽트 요청을 확인하고 인터럽트를 받아들일 수 있는지 확인
    4. 인터럽트를 받아들일 수 있다면 CPU가 수행하던 작업을 백업
    5. CPU가 인터럽트 벡터를 참조하여 인터럽트 서비스 루틴 실행
    6. 인터럽트 서비스 루틴 실행이 끝나면 4에서 백업해둔 작업을 복구하여 실행 재개

* 하드웨어 인터럽트 관련 용어
    * 인터럽트 플래그 : 인터럽트 요청 신호를 받아들일지 무시할지 결정하는 비트
    * 인터럽트 서비스 루틴 : a.k.a. 인터럽트 핸들러, 인터럽트를 처리하는 프로그램
    * 인터럽트 벡터 : 인터럽트 서비스 루틴의 시작 주소를 포함하는 인터럽트 서비스 루틴의 식별 정보


* 예외의 종류
    * 폴트 : 예외 처리 직후 예외가 발생한 명령어부터 실행을 재개하는 예외
    * 트랩 : 예외 처리 직후 예외가 발생한 명령어의 다음 명령어부터 실행을 재개하는 예외
    * 중단 : CPU가 실행 중인 프로그램을 강제로 중단시킬 수밖에 없는 심각한 오류를 발견했을 때 발생하는 예외
    * 소프트웨어 인터럽트 : 시스템 호출이 발생했을 때 나타나는 예외
    

## CPU 성능 향상 기법
* 클럭 : 클럭 속도가 높으면 CPU가 더 빠르게 동작하지만, 클럭 속도만으로 CPU의 성능을 올리는 것에는 한계가 있음
* 코어 : CPU 내에서 명령어를 실행하는 부품 (앞에서의 CPU와 동일 개념)
    * CPU는 보통 여러 개의 코어를 포함하고, 이를 멀티코어 프로세서 또는 멀티코어 CPU라고 부름
    * 코어 개수에 비례해서 연산 처리 속도가 빨라지는 것은 아님 -> 처리할 명령어를 적절하게 분배하는 것이 중요
* 스레드 : 실행 흐름의 단위
    * 하드웨어적 스레드
        * CPU에서의 스레드
        * 하나의 코어가 동시에 처리하는 명령어 단위 (명령어 처리 단위)
        * 하나의 코어로 여러 명령어를 동시에 처리하는 CPU를 멀티스레드 프로세서 또는 멀티스레드 CPU라고 부름
        * a.k.a. 논리 프로세서
        * 멀티스레드 프로세서의 코어는 하나의 명령어를 실행하기 위해 필요한 '레지스터 세트'를 여러 개 가짐
    * 소프트웨어적 스레드
        * 프로그래밍 언어, 운영체제에서의 스레드
        * 하나의 프로그램에서 독립적으로 실행되는 단위 (독립적 실행 단위)


### 명령어 병렬 처리 기법
* 명령어를 동시에 처리하는 기법
* 대표적인 기법에는 명령어 파이프라이닝, 슈퍼스칼라, 비순차적 명령어 처리가 있음
1. 명령어 파이프라이닝
    * 동시에 여러 개의 명령어를 겹쳐 실행하는 기법
    * 명령어 처리 과정을 클럭 단위로 나누면 명령어 인출, 해석, 실행, 결과 저장 단계로 구분됨
    * CPU는 겹치지 않는 각 단계를 동시에 실행 가능
    * 파이프라인 위험
        * 파이프라이닝이 성능 향상에 실패하는 특정 상황
        * 데이터 위험, 제어 위험, 구조적 위험이 있음
        * 데이터 위험
            * 명령어 간 데이터 의존성에 의해 발생
            * 데이터 의존적인 두 명령어를 무작정 동시에 실행하려고 하면 파이프라인이 제대로 작동하지 않는 것
        * 제어 위험
            * 분기 등으로 인한 프로그램 카운터의 갑작스러운 변화에 의해 발생
            * 프로그램 실행 흐름이 갑자기 바뀌면 명령어 파이프라인에서 미리 인출해서 처리 중이었던 명령어들은 쓸모없어짐
            * 이를 해결하기 위해 분기 예측 사용
                * 프로그램이 어디로 분기할지 미리 예측한 후 그 주소를 인출하는 기술
        * 구조적 위험
            * a.k.a. 자원 위험
            * 명령어들을 겹쳐 실행하는 과정에서 서로 다른 명령어가 동시에 ALU, 레지스터와 같은 CPU 부품을 사용하려고 할 때 발생

2. 슈퍼스칼라
    * CPU 내부에 여러 개의 명령어 파이프라인을 두는 기법 (공장 생산 라인 여러 개)
    * 슈퍼스칼라 구조로 명령어 처리가 가능한 CPU를 슈퍼스칼라 프로세서 또는 슈퍼스칼라 CPU라고 부름
    * 슈퍼스칼라 방식을 차용한 CPU는 파이프라인 위험을 방지하기 위해 고도로 설계되어야 함

3. 비순차적 명령어 처리
    * OoOE; Out-of-Order Execution
    * 파이프라인의 중단을 방지하기 위해 명령어를 순차적으로 처리하지 않는 기법
    * 명령어 파이프라이닝, 슈퍼스칼라 기법은 명령어의 순차적 처리를 상정


### CISC와 RISC
* 명령어 집합(instruction set) / 명령어 집합 구조(ISA; Instruction Set Architecture) : CPU가 이해할 수 있는 명령어들의 집합
    * CPU의 언어이자 CPU를 비롯한 하드웨어가 소프트웨어를 어떻게 이해할지에 대한 약속
    * CPU 하드웨어 설계에도 큰 영향을 미침
* RISC와 CISC : 각기 다른 성격의 ISA를 기반으로 만들어진 CPU 설계 방식

    |CISC|RISC|
    |---|---|
    |Complex Instruction Set Computer|Reduced Instruction Set Computer|
    |복잡하고 다양한 명령어|단순하고 적은 명령어|
    |가변 길이 명령어|고정 길이 명령어|
    |다양한 주소 지정 방식|적은 주소 지정 방식|
    |프로그램을 이루는 명령어 수가 적음|프로그램을 이루는 명령어 수가 많음|
    |여러 클럭에 걸쳐 명령어 수행|1클럭 내외로 명령어 수행|
    |파이프라이닝하기 어려움|파이프라이닝 하기 쉬움|


## 메모리와 캐시 메모리
* 보조기억장치는 비휘발성이지만 CPU는 보조기억장치에 직접 접근하지 못함
* 비휘발성 저장 장치인 보조기억장치에는 '보관할 대상'을 저장하고, 휘발성 저장 장치인 RAM에는 '실행할 대상'을 저장
* CPU가 실행하고 싶은 프로그램이 보조기억장치에 있다면 이를 RAM으로 복사하여 저장한 뒤 실행
* RAM 용량이 충분히 크면 보조기억장치에서 많은 데이터를 가져와 저장할 수 있으므로 많은 프로그램들을 동시에 빠르게 실행하는 데 유리


### RAM의 종류
    1. DRAM
        * Dynamic RAM, 저장된 데이터가 동적으로 변하는(사라지는) RAM
        * 시간이 지나면 저장된 데이터가 점차 사라짐
        * 일정 주기로 데이터를 재활성화(다시 저장)해야 함
        * 일반적으로 메모리로써 사용
        * 소비 전력이 비교적 낮고, 저렴하고, 집적도가 높으므로 대용량으로 설계하기 용이
    2. SRAM
        * Static RAM, 저장된 데이터가 변하지 않는 RAM
        * 시간이 지나도 저장된 데이터가 사라지지 않음 (휘발성 메모리이므로 전원이 공급되지 않으면 저장된 내용 날아감)
        * 데이터 재활성화 필요 없음
        * DRAM보다 속도 빠르나, 집적도가 낮고, 소비 전력이 크며, 가격이 더 비쌈
        * 대용량으로 만들어질 필요는 없지만 속도가 빨라야 하는 저장 장치인 캐시 메모리에서 사용
    3. SDRAM
        * Synchronous Dynamic RAM
        * 클럭 신호와 동기화된 DRAM
        * 클럭 신호에 맞춰 동작하며 클럭마다 CPU와 정보를 주고받을 수 있는 DRAM
    4. DDR SDRAM
        * Double Data Rate SDRAM
        * 대역폭을 넓혀 속도를 빠르게 만든 SDRAM
        * 대역폭(data rate) : 데이터를 주고받는 길의 너비
        * 한 클럭당 두 번씩 CPU와 데이터를 주고받을 수 있으므로 SDR SDRAM보다 전송 속도가 두 배가량 빠름
        * 최근에 흔히 사용하는 메모리는 DDR4 SDRAM으로 SDR SDRAM보다 16배 넓은 대역폭을 가짐


### 메모리의 주소 공간
* 주소 : 메모리에 저장된 정보의 위치
* 물리 주소 : 메모리 하드웨어가 사용하는 주소, 정보가 실제로 저장된 하드웨어상의 주소
* 논리 주소 : CPU와 실행 중인 프로그램이 사용하는 주소, 실행 중인 프로그램 각각에 부여된 0번지부터 시작되는 주소
* 메모리 관리 장치(MMU; Memory Management Unit)
    * CPU와 주소 버스 사이에 위치한 하드웨어
    * 논리 주소를 물리 주소로 변환
    * 베이스 레지스터에 프로그램의 첫 물리 주소를 저장하고, 이에 논리 주소(프로그램 시작점으로부터 떨어진 거리)를 더하여 물리 주소를 얻음
* 메모리 보호 기법
    * 논리 주소 범위를 벗어나는 명령어 실행을 방지하고 실행 중인 프로그램이 다른 프로그램에 영향을 받지 않도록 보호할 방법이 필요
    * 한계 레지스터 : 논리 주소의 최대 크기를 저장
        * 프로그램의 물리 주소 범위는 베이스 레지스터 값 이상, 베이스 레지스터 값 + 한계 레지스터 값 미만이 됨
        * CPU가 접근하려는 논리 주소는 한계 레지스터 값보다 작아야 함 -> 그렇지 않다면 인터럽트(트랩) 발생


### 캐시 메모리
* CPU의 메모리 접근 속도는 연산 속도보다 훨씬 느리므로 이를 극복하기 위한 저장 장치가 필요 -> 캐시 메모리
* 저장 장치 계층 구조 : 각기 다른 용량과 성능의 저장 장치들을 계층화하여 표현한 구조
    * 일반적으로 CPU와 가까운 저장 장치는 빠르고, 멀리 있는 저장 장치는 느림
    * 속도가 빠른 저장 장치는 저장 용량이 작고, 가격이 비쌈
    * 컴퓨터가 사용하는 저장 장치들은 'CPU에 얼마나 가까운가'를 기준으로 계층적으로 나타낼 수 있음
    * 보조기억장치 -> 메모리 -> 레지스터
        * 오른쪽으로 갈수록 CPU에 가깝고, 속도가 빠르고, 용량이 작고, 가격이 비쌈
* 캐시 메모리
    * CPU와 메모리 사이에 위치하는 SRAM 기반의 저장 장치
    * 레지스터보다 용량이 크고, 메모리보다 빠름
    * CPU 연산 속도와 메모리 접근 속도의 차이를 줄이기 위한 저장 장치
    * 보조기억장치 -> 메모리 -> 캐시 메모리 -> 레지스터 (저장 장치 계층 구조)
    * 컴퓨터 내부에는 여러 개의 캐시 메모리가 있음
        * CPU(코어)와 가까운 순서대로 계층을 구성함, L1, L2, L3 캐시
        * 보조기억장치 -> 메모리 -> L3 캐시 -> L2 캐시 -> L1 캐시 -> 레지스터 (저장 장치 계층 구조)
        * 메모리의 데이터가 필요하면 L1, L2, L3, 메모리 순으로 데이터 검색
        * 멀티 코어 프로세서에서 L1, L2 캐시는 코어마다 고유한 캐시 메모리로 할당되고, L3 캐시는 여러 코어가 공유하는 형태로 사용
        * 분리형 캐시 : 접근 속도를 더 빠르게 하기 위해 L1 캐시를 명령어만을 저장하는 L1I 캐시와 데이터만을 저장하는 L1D 캐시로 분리하는 경우도 있음
* 참조 지역성 원리
    * 캐시 메모리는 CPU가 사용할 법한 데이터를 예측하여 저장
    * CPU가 필요로 하는 데이터가 캐시 메모리에 존재하여 활용되는 경우 -> 캐시 히트
    * CPU가 필요로 하는 데이터가 캐시 메모리에 없어 메모리에서 직접 데이터를 가져와야 하는 경우 -> 캐시 미스
    * 캐시 적중률 : 캐시가 히트되는 비율
        * 캐시 메모리의 이점을 제대로 활용하려면 CPU가 사용할 법한 데이터를 제대로 예측해서 캐시 적중률을 높여야 함
        * 캐시 메모리는 참조 지역성의 원리에 입각해 CPU가 사용할 법한 데이터를 예측하고 메모리로부터 가져옴
    * CPU가 메모리에 접근할 때의 주된 경향
        * CPU는 '최근에 접근했던 메모리 공간에 다시 접근하려는 경향'이 있음 (시간 지역성)
        * CPU는 '접근한 메모리 공간 근처를 접근하려는 경향'이 있음 (공간 지역성)
            * 메모리에서 연관된 데이터들은 모여서 저장되어 있음


## 보조기억장치
### 하드 디스크
* 자기적인 방식으로 데이터를 저장하는 보조기억장치, 자기 디스크의 일종
* 플래터 : 데이터가 저장되는 동그란 원판
* 스핀들 : 플래터를 회전시키는 부품
* RPM : Revolution Per Minute
* 헤드 : 플래터를 대상으로 데이터를 읽고 쓰는 부품
* 디스크 암 : 원하는 위치로 헤드를 이동시킴
* 하드 디스크는 여러 겹의 플래터로 이루어져 있고, 플래터 양면을 모두 사용 가능
    * 양면 플래터의 경우 플래터당 두 개의 헤드가 사용되며, 모든 헤드는 디스크 암에 부착되어 다같이 이동
* 트랙 : 플래터를 여러 동심원으로 나누었을 때 그중 하나의 원
* 섹터 : 하드 디스크의 가장 작은 전송 단위
    * 하나 이상의 섹터를 묶어 블록이라고 표현하기도 함
* 실린더 : 여러 겹의 플래터 상에서 같은 트랙이 위치한 곳을 모아 연결한 논리적 단위
    * 연속된 정보는 보통 한 실린더에 기록됨 -> 디스크 암을 움직이지 않고도 데이터에 접근 가능하기 때문
* 하드 디스크가 저장된 데이터에 접근하는 시간
    1. 탐색 시간 : 접근하려는 데이터가 저장된 트랙까지 헤드를 이동시키는 시간
    2. 회전 지연 : 헤드가 있는 곳으로 플래터를 회전시키는 시간
    3. 전송 시간 : 하드 디스크와 컴퓨터 간에 데이터를 전송하는 시간


### 플래시 메모리
* 전기적으로 데이터를 읽고 쓸 수 있는 반도체 기반의 저장 장치
* 셀 : 플래시 메모리에서 데이터를 저장하는 가장 작은 단위
* 하나의 셀에 저장할 수 있는 비트 수에 따라 SLC, MLC, TLC 타입으로 분류됨

|구분|SLC|MLC|TLC|
|---|:---:|:---:|:---:|
|셀당 bit|1bit|2bit|3bit|
|수명|길다|보통|짧다|
|읽기/쓰기 속도|빠르다|보통|느리다|
|용량 대비 가격|높다|보통|낮다|

* 셀 -> 페이지 -> 블록 -> 플레인 -> 다이 순으로 계층 형성
* 읽기/쓰기는 페이지 단위로, 삭제는 페이지보다 큰 블록 단위로 이루어짐 (플래시 메모리의 가장 큰 특징 중 하나)
* 페이지는 Free, Valid, Invalid의 3가지 상태를 가질 수 있음
    1. Free 상태 : 어떠한 데이터도 저장하고 있지 않아 새로운 데이터를 저장할 수 있는 상태
    2. Valid 상태 : 이미 유효한 데이터를 저장하고 있는 상태
    3. Invalid 상태 : 쓰레기값이라 부르는 유효하지 않은 데이터를 저장하고 있는 상태
    * 플래시 메모리는 하드 디스크와 달리 덮어쓰기가 불가능하여 Valid, Invalid 상태인 페이지에는 새 데이터 저장 불가
* 가비지 컬렉션 : 유효한 페이지들만 새로운 블록으로 복사한 후 기존 블록을 삭제하여 공간을 정리하는 기능


### RAID의 정의와 종류
* RAID
    * Redundant Array of Independent Disks
    * 주로 하드 디스크와 SSD를 사용하는 기술로, 데이터의 안전성 혹은 높은 성능을 위해 여러 개의 물리적 보조기억장치를 마치 하나의 논리적 보조기억장치처럼 사용하는 기술
* RAID의 종류
    * RAID 0 : 데이터를 단순히 병렬로 분산하여 저장
        * 하나의 대용량 저장 장치를 사용할 때보다 저장된 데이터를 읽고 쓰는 속도가 빠름
        * 저장된 정보가 안전하지 않음
    * RAID 1 : 완전한 복사본을 만듦
        * 저장된 정보는 안전하지만 복사본 용량만큼 사용 가능한 용량이 적어짐
    * RAID 4 : 패리티를 저장한 장치를 따로 둠
        * 패리티 비트 : 오류를 검출하고 복구하기 위한 정보
        * RAID 4는 RAID 1보다 적은 하드 디스크로도 데이터를 안전하게 보관 가능
        * 새로운 데이터가 저장될 때마다 패리티를 저장하는 디스크에도 데이터를 쓰게 되므로 패리티를 저장하는 장치에 병목 현상이 발생함
    * RAID 5 : 패리티를 분산하여 저장
        * RAID 4의 병목 현상 해결
    * RAID 6 : 서로 다른 두 개의 패리티를 둠
        * 오류 검출/복구 수단이 두 개이므로 RAID 4, 5보다 안전한 구성
        * 새로운 정보를 저장할 때마다 함께 저장할 패리티가 두 개이므로 쓰기 속도는 RAID 5보다 느림
        * 저장 속도를 조금 희생하더라도 데이터를 더욱 안전하게 보관하고 싶은 경우 사용


## 입출력장치
* 장치 컨트롤러
    * a.k.a. 입출력 제어기, 입출력 모듈
    * 모든 입출력장치는 장치 컨트롤러라는 하드웨어를 통해 컴퓨터 내부와 정보를 주고받고, 장치 컨트롤러는 하나 이상의 입출력장치와 연결되어 있음
    * 역할
        * CPU와 입출력장치 간의 통신 중개
            * 입출력장치마다 데이터 전송 형식이 다르므로 다양한 입출력장치와 정보를 주고받는 방식을 규격화함 (일종의 번역가 역할)
        * 오류 검출
            * 입출력장치에 문제 없는지 오류 검출
        * 데이터 버퍼링
            * 전송률 : 데이터 교환 속도를 나타내는 지표
                * 일반적으로 CPU와 메모리의 전송률은 높지만 입출력장치의 전송률은 낮음
            * 버퍼링 : 전송률이 높은 장치와 낮은 장치 사이에 주고받는 데이터를 버퍼라는 임시 저장 공간에 저장하여 전송률을 비슷하게 맞추는 방법
            * 장치 컨트롤러는 CPU와 입출력장치 간 전송률 차이를 데이터 버퍼링으로 완화
    * 내부 구조
        * 데이터 레지스터
            * CPU와 입출력장치 사이에 주고받을 데이터가 담기는 레지스터
            * 데이터 버퍼링의 버퍼 역할
        * 상태 레지스터
            * 입출력장치의 상태 정보가 저장
        * 제어 레지스터
            * 입출력장치가 수행할 내용에 대한 제어 정보와 명령 저장
* 장치 드라이버 : 장치 컨트롤러의 동작을 감지하고 제어함으로써 장치 컨트롤러가 컴퓨터 내부와 정보를 주고받을 수 있게 하는 프로그램


### 입출력 방법
* CPU와 장치 컨트롤러가 정보를 주고받는 방법
* 프로그램 입출력
    * 프로그램 속 명령어로 입출력장치를 제어하는 방법
* 메모리 맵 입출력 : 메모리에 접근하기 위한 주소 공간과 입출력장치에 접근하기 위한 주소 공간을 하나의 주소 공간으로 간주하는 방법
* 고립형 입출력 : 메모리를 위한 주소 공간과 입출력장치를 위한 주소 공간을 분리하는 방법

|메모리 맵 입출력|고립형 입출력|
|---|---|
|메모리와 입출력장치는 같은 주소 공간 사용|메모리와 입출력장치는 분리된 주소 공간 사용|
|메모리 주소 공간이 축소됨|메모리 주소 공간이 축소되지 않음|
|메모리와 입출력장치에 같은 명령어 사용 가능|입출력 전용 명령어 사용|

* 인터럽트 기반 입출력 : 인터럽트를 기반으로 하는 입출력
    * 폴링 : CPU가 주기적으로 장치 컨트롤러(입출력장치)의 상태를 확인하는 방식 -> 인터럽트와 대조됨
        * CPU의 부담이 더 큼
    * 여러 입출력장치에서 동시에 인터럽트가 발생한 경우, 우선순위를 반영하여 다중 인터럽트를 처리해야 함 -> PIC 사용
    * 프로그래머블 인터럽트 컨트롤러(PIC)
        * 여러 장치 컨트롤러에 연결되어 장치 컨트롤러에서 보낸 하드웨어 인터럽트 요청들의 우선순위를 판별한 뒤 CPU에 가장 먼저 처리할 인터럽트를 알려주는 하드웨어
* DMA 입출력
    * CPU를 거치지 않고 메모리와 입출력장치 간의 데이터를 주고받는 입출력 방식
    * 시스템 버스에 연결된 DMA 컨트롤러가 CPU 대신 메모리, 장치 컨트롤러와 상호작용
    * 프로그램 기반 입출력과 인터럽트 기반 입출력에서는 입출력장치와 메모리 간 데이터 이동을 CPU가 주도하고, 이동하는 데이터도 반드시 CPU를 거침 -> CPU 부담이 가중되므로 이를 해결하기 위한 방식
    * CPU는 입출력의 시작과 끝에만 관여
    * 시스템 버스는 공용 자원이므로 DMA 컨트롤러가 시스템 버스를 사용할 경우 CPU는 사용 불가
        * DMA 컨트롤러와 장치 컨트롤러들을 입출력 버스라는 별도의 버스에 연결하여 DMA 컨트롤러의 시스템 버스 사용 빈도를 줄임
        * 입출력 버스는 입출력장치를 컴퓨터 내부와 연결 짓는 통로