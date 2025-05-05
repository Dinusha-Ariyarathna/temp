flowchart LR
  %% Client Side
  subgraph Frontend [React SPA]
    direction TB
    CLI[User’s Browser\n(React Components)]
  end

  %% Security Layer
  subgraph Security [Spring Security & OAuth2]
    direction TB
    SC[SecurityConfig<br/>(CSRF, Session, OAuth2Login)] 
    CO[CustomOAuth2UserService]
    SC --> CO
  end

  %% Controllers
  subgraph Controllers [REST Controllers]
    direction TB
    C1[PostController<br/>/api/posts]
    C2[CommentController<br/>/api/comments]
    C3[LikeController<br/>/api/posts/{id}/likes]
    C4[ProfileController<br/>/api/users/**]
    C5[LearningPlanController<br/>/api/plans]
    C6[TagController<br/>/api/tags & /api/posts/{id}/tags]
    C7[NotificationController<br/>/api/notifications]
    C8[PostMediaController<br/>/api/posts/{id}/media]
  end

  %% Service Layer
  subgraph Services [Service Layer]
    direction TB
    S1[PostService]
    S2[CommentService]
    S3[LikeService]
    S4[UserService]
    S5[LearningPlanService]
    S6[TagService]
    S7[NotificationService]
    S8[FileStorageService]
  end

  %% Data Layer
  subgraph Repositories [JPA Repositories]
    direction TB
    R1[PostRepository]
    R2[CommentRepository]
    R3[LikeRepository]
    R4[UserRepository]
    R5[LearningPlanRepository]
    R6[TagRepository]
    R7[NotificationRepository]
  end

  %% Persistence & External
  DB[(MySQL Database)]
  FS[(File System: uploads/…)]
  GO[Google OAuth2 Provider]

  %% DevOps
  GH[GitHub Actions CI]

  %% Links
  CLI -->|HTTPS /api/**| SC
  SC -->|dispatch| C1 & C2 & C3 & C4 & C5 & C6 & C7 & C8
  C1 & C2 & C3 & C4 & C5 & C6 & C7 & C8 --> Services
  Services --> Repositories
  Services --> FileStorageService
  Repositories --> DB
  FileStorageService --> FS
  SC -- userInfoEndpoint --> CO --> GO

  GH -->|on push/PR|[ci.yml] GH_BUILD[Build & Test]

  style DB fill:#f9f,stroke:#333,stroke-width:1px
  style FS fill:#ff9,stroke:#333
  style GH_BUILD fill:#9ff,stroke:#333
