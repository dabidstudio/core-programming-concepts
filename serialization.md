<!-- 

최종편집: 2024-08-16
-->

### Python에서의 직렬화의 개념: 객체를 JSON으로 변환하고 다시 되돌리기

---
#### 핵심요약
1. 직렬화는 바이트 또는 문자열의 나열로 변환하는 것이다
2. 직렬화 하는 이유는 데이터의 이동이 편리하기 때문이다 (파일 형태로 이동하고 불러오면 됨)
3. 실무에서는 직렬화(Serialization) = JSON으로 변환
4. 반대로 역직렬화(Deserialization) = 프로그래밍 언어가 이해하도록 JSON을 다시 Python 객체로 변환하기
    
---

#### 직렬화 어원 설명 + 이해
- 직렬화에서 직렬(영문으로는 Series)는 바이트의 나열을 의미함
- 바이트나 문자열의 나열로 표현되어 있으면 파일로 저장하거나 전송하기 쉬움
- 대표적인 직렬이 JSON이나 CSV같은 파일임
- 반면에 직렬이 아닌 것은 파이썬에서 객체나 리스트 등 코딩을 수월하게 하기 위해서 추상화된 개념들임
- 이런 객체나 리스트를 다른 곳으로 쉽게 이동하려면 직렬화를 하는 것이 추천됨
- 예를 들어 데이터프레임(Dataframe)도 파이썬의 대표적인 객체 중 하나인데, 파이썬 안에서만 데이터프레임을 이용하고 실제로 데이터를 저장하거나 전송할 때는 csv로 직렬화해서 이동함
  - 그 다음 다른 컴퓨터나 프로그램에서도 csv의 직렬화된 데이터를 역직렬화해서 데이터프레임으로 사용할 수 있음

#### Python에서의 직렬화 예제 (datetime 객체)

**1단계: `datetime` 객체 생성 및 메서드 활용**
- 파이썬에서는 다양한 객체를 생성하고 사용하는데, 객체의 가장 큰 장점은 객체에 대한 다양한 메서드를 활용할 수 있다는 것임
```python
from datetime import datetime, timedelta

specific_date = datetime(2024, 1, 1, 18, 0)

# 메서드 1: 날짜에 5일 더하기
new_date = specific_date + timedelta(days=5)
print("New Date (5 days later):", new_date)

# 메서드 2: 요일 확인
day_of_week = specific_date.strftime("%A")
print("Day of the Week:", day_of_week)
```
출력:  
`New Date (5 days later): 2024-01-06 18:00:00`  
`Day of the Week: Monday`

**2단계: `datetime` 객체 직렬화**
- 만약 다른 코드나 파일에서 같은 객체를 활용하고 싶으면 먼저 직렬화를 해줄 수 있음
```python
import json

specific_date_json = json.dumps({"timestamp": specific_date.isoformat()})
print("Serialized JSON:", specific_date_json)
```
출력: `{"timestamp": "2024-01-01T18:00:00"}`

**3단계: JSON을 다시 `datetime` 객체로 역직렬화**
  
```python
data = json.loads(specific_date_json)
deserialized_date = datetime.fromisoformat(data["timestamp"])
print("Deserialized Datetime Object:", deserialized_date)
print("Is the original date equal to the deserialized date?", specific_date == deserialized_date)
```
출력:  
`Deserialized Datetime Object: 2024-01-01 18:00:00`  
`Is the original date equal to the deserialized date? True`

#### 요약
- `datetime` 객체는 날짜 연산이 가능함. 예를 들어, 날짜에 며칠을 더하거나 요일을 확인할 수 있음.
- JSON으로 직렬화할 때는 `isoformat()` 메서드를 사용하고, 다시 객체로 역직렬화할 때는 `fromisoformat()` 메서드를 사용함.
- 직렬화와 역직렬화를 통해 원본 데이터와 동일한 객체를 재구성할 수 있음.