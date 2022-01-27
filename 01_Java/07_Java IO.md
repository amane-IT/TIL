# Java I/O
## 개념
- 스트링(1 byte)의 데이터를 읽고 쓰거나 문자(2 byte)를 읽고 쓰는 것이 가능
- Stream: 입출력 장치에 의한 데이터 흐름
- Source Stream: 입력 데이터의 시작
- Sink Stream: 데이터 처리 후 출력되는 값
- Node Stream = Source + Sink


## File 클래스
- file에 대한 정보 제공

## Node Stream
### Byte Stream
- 1byte 단위 처리
- Source Stream: InputStream, FileInputStream
- Sink Stream: OutputStream, FileOutputStream

### Character Stream
- 문자 단위 처리에 적합(ex. 한글)
- Source Stream: Reader, FileReader
- Sink Stream: Writer, FileWriter

### 주요 메서드
- InputStream
  + read() / read(byte[] buf) / int read(byte[] buf, int offset, int length)
- OutputStream
  + write() / write(byte[] buf) / int write(byte[] buf, int offset, int length)


## Processing Stream
- Node Stream의 보조
- Node Stream만 사용하면 CPU의 효율성 / 속도 저하

### 장점
- 속도 향상
- Data Type 별 처리
- Object별로 처리

*** 입출력은 Scanner보다 Stream을 활용하는 것이 속도가 더 빠름 ***

- - -
## Serialization
- 직렬화
- 객체를 입출력하기 위해 필요
- **implements Serialiizable**을 하거나 implements Externalizable로 구현
- Serializable을 상속하고 **serialVersionUID**가 없으면 경고가 뜸
  + 없어도 실행되지만 버전 관리에 어려움
  + 명시적으로 표시해 개발자가 버전을 관리할 수 있도록 함
  + serialVersionUID: 현재 개발자가 개발하는 버전 넘버
  + 달라지면 변경 전의 버전을 불러올 수 없음
