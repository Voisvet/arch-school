# Модель предметной области
<!-- Логическая модель, содержащая бизнес-сущности предметной области, атрибуты и связи между ними. 
Подробнее: https://confluence.mts.ru/pages/viewpage.action?pageId=375782602

Используется диаграмма классов UML. Документация: https://plantuml.com/class-diagram 
-->

```plantuml
@startuml
' Логическая модель данных в варианте UML Class Diagram (альтернатива ER-диаграмме).

namespace Conference {
  class Reporter {
    name : string
    email : string
    report : Report
  }

  class Viewer {
    name : string
    email : string
  }

  class Reviewer {
    name : string
    email : string
    role : ReviewerRole
    reports : Report[]
  }

  class Moderator {
    name : string
    email : string
    room : Room
  }

  class Administrator {
    name : string
    email : string
  }

  class ProgramEntity {
    report : Report
    startTime : datetime
  }

  class Report {
    topic : string
    presentation : string
    duration : integer
    status : ReportStatus
  }

  class Recommendation {
    autor : Reviewer
    report : Report
    comment : string
  }

  class Room {
    program : ProgramEntity[]
    translation : Translation
  }

  class Translation {}

  enum ReviewerRole {
    programCommittee
    lawyer
  }

  enum ReportStatus {
    draft
    declined
    accepted
    onReview
  }

  ReviewerRole -- Reviewer
  ReportStatus -- Report

  Reporter *-- "1" Report
  Reviewer *-- "0..*" Report
  Moderator *-- "1" Room
  ProgramEntity *-- "1" Report
  Report *-- "0..*" Recommendation
  Room *-- "1..*" ProgramEntity
  Room *-- "1" Translation
}
@enduml
```
