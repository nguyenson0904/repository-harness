> Với setup này, nếu kịch bản sau xảy ra thì nó sẽ được cải thiện như thế nào ở những lần tiếp theo
>  - promt 1: tôi yêu cầu implement tính năng call api đến đối tác để đồng bộ dữ liệu vào db, ai agent sau khi done báo đã hoàn thành công việc
>  Thực tế tôi kiểm tra vẫn chưa có record nào được kéo về
>  - Yêu cầu ai agent tạo smoke test để xem có thực sự đã kết nối được với api của đối tác không
>  - AI agent lúc này mới phát hiện lỗi, fix và thực sự hoàn thành tính năng


• Với setup agent-harness-lite, kịch bản này sẽ cải thiện bằng cách biến “lỗi bị phát hiện muộn” thành rule/checklist bắt buộc cho lần sau.

  Cụ thể sau incident này nên cập nhật 3 nơi:

  1. Story hiện tại trong docs/stories/

  Trong story của tính năng sync đối tác, ghi lại validation thật:

  ## Validation

  - [x] Unit:
  - [x] Integration:
  - [x] Smoke:
    - Command: `<command smoke test>`
    - Result: pass
    - Evidence: pulled 12 records from partner API into local DB
  - [ ] Not run / reason:

  Và thêm closeout note:

  ## Closeout Notes

  Initial implementation was reported complete before proving partner API connectivity.
  Smoke test later found the real integration issue. Future partner sync stories must
  include a smoke test that verifies at least one successful pull into DB.

  2. Backlog hoặc friction trong docs/stories/backlog.md

  Ghi một follow-up để cải thiện harness:

  ### Require smoke proof for partner API sync

  - Status: accepted
  - Risk: normal
  - Discovered while: Partner sync implementation was marked done before any data was pulled.
  - Current pain: Agent claimed completion based on code changes, not real external API proof.
  - Suggested improvement: Add a required smoke-test checklist for external API sync stories.
  - Notes: Smoke proof must verify API connectivity and DB write result.

  3. Coding/workflow rule hoặc template

  Cập nhật docs/templates/story.md để các story external integration luôn có mục smoke proof:

  ## External Integration Proof

  Required when this story touches partner APIs, webhooks, queues, provider SDKs, or external services.

  - [ ] Connectivity verified against the configured environment.
  - [ ] At least one real or sandbox response was received.
  - [ ] Data mapping was verified.
  - [ ] Expected DB write/update was verified.
  - [ ] Failure case was checked or documented.
  - [ ] Evidence:

  Có thể thêm rule vào docs/FEATURE_INTAKE.md:

  External provider behavior is high-risk unless scoped to mock-only work.
  A story touching partner APIs must include smoke validation before it can be marked implemented.

  Kết quả ở lần tiếp theo:

  - Agent thấy task “call API đối tác để đồng bộ DB” sẽ classify thành high-risk hoặc normal với strong validation, vì chạm external systems + data model.
  - Agent phải tạo/cập nhật story trước khi implement.
  - Story template nhắc rõ phải có External Integration Proof.
  - Khi close task, agent không được chỉ nói “done” vì code đã viết xong; phải ghi evidence kiểu:
      - gọi được API môi trường nào,
      - nhận response gì,
      - mapping ra sao,
      - DB có bao nhiêu record được insert/update,
      - smoke test command/result.

  - Nếu không có credential/sandbox/API thật, agent phải nói rõ blocked/partial, không được claim hoàn thành.

  Nói ngắn gọn: Harness không tự ngăn bug, nhưng nó biến bug đó thành memory của repo. Lần sau, agent được guide bởi story template + intake rule + backlog
  friction để không lặp lại kiểu “hoàn thành trên giấy nhưng chưa prove external integration”.