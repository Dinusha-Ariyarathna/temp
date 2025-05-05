```mermaid
flowchart LR
  %% Controllers Layer
  subgraph Controllers [REST Controllers]
    direction LR
    PC(PostController<br/>POST /api/posts)
    GP(GetPostsController<br/>GET /api/posts)
    UP(UpdatePostController<br/>PUT /api/posts/{id})
    DP(DeletePostController<br/>DELETE /api/posts/{id})
    CC(CommentController<br/>POST /api/comments/{postId})
    GC(GetCommentsController<br/>GET /api/comments/{postId})
    DC(DeleteCommentController<br/>DELETE /api/comments/{commentId})
    LC(LikeController<br/>POST /api/posts/{postId}/likes)
    UC(UnlikeController<br/>DELETE /api/posts/{postId}/likes)
    GL(GetLikesController<br/>GET /api/posts/{postId}/likes)
    MPU(MyPostsController<br/>GET /api/users/me/posts)
    UPF(UserProfileController<br/>GET /api/users/{userId}/profile)
    CPC(CreatePlanController<br/>POST /api/plans)
    GPC(GetPlansController<br/>GET /api/plans)
    GPEC(GetPlanController<br/>GET /api/plans/{id})
    UPC( UpdatePlanController<br/>PUT /api/plans/{id})
    DPC(DeletePlanController<br/>DELETE /api/plans/{id})
    TG(GetTagsController<br/>GET /api/tags)
    CT(CreateTagController<br/>POST /api/tags)
    ATP(AssignTagsController<br/>POST /api/posts/{postId}/tags)
    PT(GetPostsByTagController<br/>GET /api/tags/{tagName}/posts)
    MEP(UploadMediaController<br/>POST /api/posts/{postId}/media)
    GN(GetNotificationsController<br/>GET /api/notifications)
    RN(MarkReadController<br/>PUT /api/notifications/{id}/read)
  end

  %% Services Layer
  subgraph Services [Service Layer]
    direction LR
    PS(PostService)
    CS(CommentService)
    LS(LikeService)
    US(UserService)
    LPS(LearningPlanService)
    TS(TagService)
    NS(NotificationService)
    FSS(FileStorageService)
  end

  %% Repositories Layer
  subgraph Repositories [JPA Repositories]
    direction LR
    PR(PostRepository)
    CR(CommentRepository)
    LR2(LikeRepository)
    UR(UserRepository)
    LPR(LearningPlanRepository)
    TR(TagRepository)
    NR(NotificationRepository)
  end

  %% External Systems
  DB[(MySQL Database)]
  FS[(File System\nuploads/)]
  GO((Google OAuth2))

  %% Draw arrows
  Controllers --> Services
  Services --> Repositories
  Repositories --> DB
  Services --> FSS
  FSS --> FS
  US --> GO
