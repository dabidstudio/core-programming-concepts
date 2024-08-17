<!-- 

최종편집: 2024-08-17
-->
### Python에서 TypedDict 사용하기

---

#### 핵심요약

- **TypedDict**는 Python에서 딕셔너리의 구조와 타입을 지정할 수 있는 도구로, TypeScript의 인터페이스와 유사함.
- **VS Code에서 타입 검사**를 활성화하려면 `settings.json`에 설정을 추가해야 함: 

    ```json
    {
      "python.analysis.typeCheckingMode": "basic"
    }
    ```


---

### TypedDict 개념

- Python의 **TypedDict**는 딕셔너리의 키와 값의 타입을 정의하는 도구로, TypeScript의 인터페이스와 유사
- 일반적인 Dictionary와의 차이점은 구체적으로 어떤 key/value가 있는지를 내가 지정해줄 수 있음
- 기본적으로 타입이 없는 파이썬의 단점을 보완한 개념이며 파이썬 3.8부터 지원

### TypedDict 사용 예제
- List, Dict 처럼 하나의 타입을 만드는 개념
- 그렇게 만들어진 타입은 person: Persons 형태로 사용할 수 있음

```python
from typing import TypedDict

class Persons(TypedDict):
    name: str
    year: str

person: Persons = {'name': 'Person1'}

print(person)
```

위 코드에서는 `Persons`라는 `TypedDict`를 정의하여 `name`과 `year`의 타입을 각각 `str`로 지정
- 하지만 `year` 키가 누락된 경우, 타입 검사 도구가 이를 감지하여 오류를 경고할 수 있음 (VS Code에서 디폴트로는 경고가 없고 별도 설정을 해줘야 함)

### 실전 예제: LangGraph의 활용

- TypedDict는 AI Agent 구축용 프레임워크인 **LangGraph**에서 State을 정의할 때 많이 활용됨
- 프로그램 전체에 통용되는 고정된 State 정의가 필요해서 아래와 같이 정의를 함

```python
from typing import TypedDict, List

class ResearchState(TypedDict):
    task: dict
    initial_research: str
    sections: List[str]
    research_data: List[dict]
    human_feedback: str
    title: str
    headers: dict
    date: str
    table_of_contents: str
    introduction: str
    conclusion: str
    sources: List[str]
    report: str
```

