# GitHub Actions

- 특정한 event가 발생했을때 자동으로 내가 원하는 작업을 수행할 수 있도록 만들어주는 툴
- GitHub Actions를 사용하여 리포지토리에서 바로 소프트웨어 개발 워크플로우 자동화, 사용자 지정 및 실행 가능
- Event
    - main 브랜치로 머지하거나 커밋 푸시 등의 이벤트를 의미
    - workflow를 실행하는 특정 활동이나 규칙을 정의한 것

- workflow
  - GitHub Actions의 가장 상위 개념으로, 특정한 이벤트가 발생했을때 수행할 일을 명시하는 것
  - 여러 job으로 구성되고 yaml파일로 작성한 후 Github Repository의 .github/workflows 폴더 아래에 저장

- Job
  - 여러 Step으로 구성되어 독립된 VM or 컨테이너에서 돌아가는 처리 단위를 의미
  - Step : Task의 집합으로 커맨드, 스크립트, action 등을 의미

- Action
  - GitHub Actions에서 빈번하게 필요한 반복 단계를 재사용하기 용이하도록 제공되는 일종의 작업 공유 메커니즘
  - 개인이 만든 것 or marketplace에 있는 공용 Action 사용 가능

- Runner
  - workflow가 실행될 인스턴스