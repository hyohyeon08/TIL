## LLM에서의 Agent
LLM을 하나의 지성체로 보고 스스로 기억을 기반으로 계획하고, 행동하고, 도구를 사용하여 능동적으로 문제를 해결하는 하나의 존재 단위를 뜻함

## Multi Agent
왜 Multi Agent를 쓸까??
#### 글 내용이 복잡
- 많은 글에 대하여 디테일을 놓치지 않고 말해야 함
- 많은 양의 요구를 주고 사람한테 한 번에 다 하라면 못하겠죠? → 단계적으로 혹은 여러개로 분활해서 접근해야 해결할 수 있는 있음

#### Agent 책임 분리
- 기존의 Single Agent 구조에서 모든 작업을 하나의 Agent가 맡아서 했음
- A→B→C라는 작업을 해야하는데, 또 다른 문제에서는 A→B 작업만 하고 싶을 수 있음. 이 때 Single Agent Architecture에서는 각각의 경우에 대하여 Agent를 따로 만들어야 하는 문제가 있음 → 이는 하나의 Agent가 모든 책임을 갖고 있어서 발생하는 문제

#### Hallucination 발생을 최소화
- 틀린 말을 맞는것 처럼 말하는 LLM
- 이러면 큰 문제가 발생할수도 있음

 
위에서 언급한 문제를 해결하기 위해 Agent끼리 협동할 수 있는 Multi Agent Architecture를 구현함

### Multi Agent Architecture란
- Agent가 서로 협력하여 문제를 해결하는 구조를 말함
- Leader Agent와 Leader Agent가 생성하는 협업 Agent들로 Multi Agent 구조를 만듬
![alt text](image.png)
1. Leader Agent가 Key Point Analyzer Agent에게 복잡한 질문을 간단한 여러개의 Sub-question으로 나눠 달라 요청
2. Leader Agent가 Sub-question 목록을 받으면 각각의 Sub-question에 대하여 Question Answerer Agent을 생성하고 답해달라 요청
3. Question Answerer Agent는 각 Sub-question에 필요한 정보를 Vector Store에서 찾아 이를 참고하여 답함
4. Leader Agent는 각각 Sub-question에 대한 답을 합하여 사용자 질의에 대한 답을 생성하고, Reviewer에게 검토해달라 요청
5. Reviewer Agent는 Leader Agent로부터 전달받은 답변에 대한 피드백을 생성하고 Leader Agent는 그 피드백을 반영하여 최종 답변을 생성한 후 사용자에게 전달


텍스트 길이가 길어지며 전반적인 사용자의 요구를 이해하지 못하고 질문의 핵심과 떨어지는 답변만 수행 했음

그러나 Multi Agent Architecture에서는  Question Answerer Agent가 복잡한 질문을 간단한 질문으로 나누고, 각각 나눈 질문에 대하여 Question Answerer Agent가 고민한 답을 Leader Agent가 합하도록 함. 이에 요구에 더 집중된 답변을 생성할 수 있었음

참고

- https://medium.com/corca/llm-multi-agent-customer-service%EB%A5%BC-%EA%B8%B0%EA%B9%94%EB%82%98%EA%B2%8C-%EC%9E%90%EB%8F%99%ED%99%94%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95-2eaec7654385