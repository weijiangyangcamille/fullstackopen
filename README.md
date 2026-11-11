# fullstackopen
[ Alice 客户端 ]         [ NestJS API / Gateway ]      [ PostgreSQL ]       [ Bob 客户端 (协同者) ]
       │                           │                         │                       │
       │── 1. 提交修改 (Patch) ───>│                         │                       │
       │   (activityId, 15:00)     │── 2. RBAC权限校验       │                       │
       │                           │   & 数据合法性审查      │                       │
       │                           │                         │                       │
       │                           │── 3. 写入事务 ─────────>│                       │
       │                           │<─ 4. 持久化成功 ────────│                       │
       │                           │                                                 │
       │<─ 5. HTTP 200 / ACK ──────│                                                 │
       │   (乐观UI转正)            │                                                 │
       │                           │── 6. WebSocket 房间广播 (activity_updated) ────>│
       │                           │      (附带修改人信息与变更差量)                 │
       │                           │                                                 │── 7. 局部 DOM/State 更新
       │                           │                                                 │   (14:00 平滑过渡到 15:00)
       │                           │                                                 │   (轻微绿色闪烁提示高亮)