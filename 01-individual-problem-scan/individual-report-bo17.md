# 01 — Individual Problem Scan: BO-17 Interview Assist Agent

## Thông tin cá nhân

- Họ và tên: Vũ Văn Điền
- Mã học viên: 2A202602418
- Vai trò / bối cảnh: Học viên phân tích bài toán AI trong quy trình phỏng vấn tuyển dụng có cấu trúc
- Chủ đề phân tích: **BO-17 — AI Agent Trợ lý Phỏng vấn & Tổng hợp Đánh giá Ứng viên**
- Nhóm người dùng quan sát: Interviewer, Hiring Lead, Hiring Manager và Recruiter
- Phạm vi workflow: Từ lúc nhận Job Description (JD), chuẩn bị phỏng vấn, thu thập evidence, lập scorecard đến debrief

> **Lưu ý về bằng chứng:** Tài liệu BO-17 cung cấp workflow, actors, nguyên tắc an toàn và target metric nhưng chưa kèm log thời gian, transcript khảo sát hoặc phỏng vấn người dùng. Vì vậy, các số ghi là **baseline giả định để thiết kế pilot**, không được xem là kết quả validation thực tế. Những số này phải được đo lại với interviewer thật trước khi chốt Problem Statement.

---

## Phase 1 — Scan 5 problems

**Cách đọc:** Mỗi dòng nêu việc gì đang gây khó khăn, ai chịu ảnh hưởng và dấu hiệu có thể đo. Cột cuối phân biệt rõ bằng chứng đã có trong đặc tả với giả định cần kiểm chứng.

|   # | Lăng kính (Lặp lại / Tốn thời gian / AI có thể tốt hơn / Pain từ người khác) | Problem quan sát được                                                                                                                       | Ai chịu ảnh hưởng?                 | Dấu hiệu định lượng và trạng thái bằng chứng                                                                                                                             |
| --: | ---------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
|   1 | Tốn thời gian / Pain từ người khác                                           | Trong buổi phỏng vấn, interviewer phải đồng thời nghe, ghi chú, nghĩ follow-up, theo dõi thời gian và nhớ competency nào chưa đủ evidence   | Interviewer và ứng viên            | Đặc tả xác nhận**5 tác vụ diễn ra đồng thời**. Giả định cần đo qua 10 buổi: thiếu evidence ở **1-2 competency/buổi** và mất **5-10 phút cuối buổi** để rà lại            |
|   2 | Lặp lại / Tốn thời gian / AI có thể tốt hơn                                  | Mỗi khi mở một vị trí tuyển dụng, interviewer phải tự chuyển JD thành competency, trọng số, câu hỏi, follow-up, expected evidence và rubric | Interviewer, Hiring Lead           | Một plan có 6 competency cần ít nhất**24 thành phần nội dung**. Baseline giả định: **60-120 phút/plan**; target trong đặc tả: giảm **≥ 50%** thời gian chuẩn bị          |
|   3 | Tốn thời gian / AI có thể tốt hơn / Pain từ người khác                       | Hiring Lead phải tự ghép nhiều scorecard, phát hiện điểm lệch, đọc evidence và viết debrief brief trước cuộc họp                            | Hiring Lead, Hiring Manager        | Với 3 interviewer × 6 competency có**18 score cells** cần tổng hợp. Baseline giả định: **45-90 phút/candidate**; disagreement đáng kể khi `max(score) - min(score) >= 2` |
|   4 | AI có thể tốt hơn / Lặp lại                                                  | Sau phỏng vấn, interviewer phải đọc lại notes hoặc transcript, map từng câu trả lời sang competency/evidence rồi mới hoàn thành scorecard   | Interviewer, Recruiter             | Có ít nhất**3 bước chuyển đổi thủ công**: đọc notes → map evidence → điền scorecard. Giả định cần đo: **20-40 phút/buổi**; target evidence coverage **≥ 90%**            |
|   5 | Pain từ người khác / Lặp lại                                                 | Cách nhận diện evidence và chấm điểm chưa nhất quán; self-claim như “tôi khá giỏi database” có thể bị coi nhầm là bằng chứng mạnh           | Ứng viên, Interviewer, Hiring Lead | Cần audit**30-50 scorecard items** để đo unsupported evidence và so sánh ít nhất **10 interview plans** cùng vị trí. Nguyên tắc kiểm soát: **“No Evidence → No Score”**  |

**AI đã dùng ở Phase 1:**

- Input cho AI: đặc tả sản phẩm BO-17 gồm current workflow, actors, modules, safety rules và MVP metrics.
- Ý dùng được: tách một sản phẩm lớn thành 5 pain cụ thể theo từng handoff thông tin; ba pain quan trọng nhất được phát triển tiếp thành Top 3 Problem Cards.
- Ý phải sửa: không coi target metric trong product spec là evidence đã được validation; mọi baseline thời gian và tần suất chưa có log đều được gắn nhãn **giả định cần kiểm chứng**.
- Ý loại bỏ: “AI tự chấm và chọn ứng viên tốt nhất”, vì trái với human-in-the-loop, tạo rủi ro fairness và vượt boundary của BO-17.

**Self-check Phase 1:**

- [x] Có đúng 5 problems; mỗi dòng có actor và cách đo cụ thể
- [x] Dùng đủ 4 lăng kính
- [x] Phân biệt bằng chứng trong tài liệu với baseline giả định
- [ ] Chưa có log hoặc phỏng vấn người dùng thật; cần validation trước khi coi các số là baseline chính thức

---

## Phase 2 — Top 3 Problem Cards

### 2.1. Chọn top 3

Tiêu chí chọn: actor cụ thể, workflow vẽ được trong 3-7 bước, bottleneck rõ, impact đo được, có phương án không dùng AI và có human boundary.

| Rank | Problem (rút từ bảng scan)                                                                  | Vì sao chọn                                                                                                                                                   | Điều còn chưa chắc                                                                                                             |
| ---: | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
|    1 | Trong interview, interviewer khó vừa phỏng vấn vừa theo dõi competency coverage và evidence | Pain xảy ra ngay trong workflow cốt lõi; có 5 tác vụ đồng thời; tác động trực tiếp đến chất lượng evidence; AI có lợi thế xử lý ngôn ngữ và cập nhật coverage | Độ chính xác khi transcript/noise kém; interviewer có bị AI suggestion làm mất tập trung không; chưa có baseline coverage thật |
|    2 | Chuẩn bị interview plan từ JD tốn nhiều bước chuyển đổi thủ công                            | Input/output rõ; dễ pilot với JD thật; có thể đo thời gian chuẩn bị, tỷ lệ câu hỏi được chấp nhận và số lần human edit                                        | Competency do AI trích xuất có bám framework công ty không; target giảm thời gian có làm giảm chất lượng plan không            |
|    3 | Hiring Lead phải tự tổng hợp nhiều scorecard và phân tích disagreement                      | Có handoff rõ giữa interviewer và Hiring Lead; phần phát hiện lệch điểm dùng rule tin cậy; LLM chỉ cần giải thích evidence khác nhau                          | Tần suất disagreement đáng kể trong thực tế; quy mô panel; cách tránh AI thiên vị một interviewer                              |

### 2.2. Problem Cards chi tiết

---

#### Problem Card #1 — Theo dõi competency coverage và evidence trong lúc phỏng vấn

```text
Problem 1 câu:
Trong một buổi phỏng vấn, interviewer phải đồng thời nghe, ghi chú, nghĩ follow-up,
theo dõi thời gian và nhớ competency nào chưa đủ evidence, nên có nguy cơ kết thúc buổi
phỏng vấn khi vẫn còn 1-2 competency thiếu bằng chứng có thể dùng để chấm điểm.

Actor:
Interviewer thực hiện structured interview cho vị trí Junior/Middle, sử dụng interview
plan gồm khoảng 5-7 competency và phải nộp scorecard sau buổi phỏng vấn.

Thời điểm / bối cảnh:
Trong buổi phỏng vấn 45-60 phút, đặc biệt ở nửa sau khi thời gian còn ít, câu trả lời
dài và interviewer vừa ghi note vừa phải quyết định có hỏi sâu hay chuyển chủ đề.

Current workflow 3-7 bước:
1. Mở interview plan và chọn câu hỏi theo competency
2. Hỏi ứng viên và nghe câu trả lời
3. Ghi note hoặc đánh dấu câu trả lời trong tài liệu riêng
4. Tự đánh giá câu trả lời đã tạo đủ evidence hay chưa
5. Tự nghĩ follow-up nếu evidence còn yếu
6. Rà thời gian và chuyển sang competency tiếp theo
7. Cuối buổi kiểm tra lại phần nào chưa hỏi hoặc chưa đủ evidence

Bottleneck:
Bước 3-6: interviewer phải chuyển đổi liên tục giữa nghe, ghi, đánh giá evidence,
nghĩ câu hỏi và kiểm soát thời gian. Trạng thái coverage chỉ nằm trong trí nhớ hoặc
checklist thủ công nên dễ bị bỏ sót.

Impact:
- Có nguy cơ thiếu evidence ở 1-2 competency/buổi (giả định cần đo qua pilot)
- Mất khoảng 5-10 phút cuối buổi để rà coverage hoặc hỏi dồn (giả định)
- Scorecard sau đó có thể dựa trên self-claim hoặc trí nhớ thay vì source traceable
- Ứng viên có thể bị đánh giá không công bằng nếu một competency chưa từng được hỏi đủ

Success metric:
- Competency coverage đạt ≥ 95% trên số competency bắt buộc
- Evidence coverage đạt ≥ 90% trên số competency cần chấm
- Unsupported evidence rate xấp xỉ 0%
- Tỷ lệ AI suggestion được interviewer chấp nhận ≥ 70% trong pilot
- Cách đo: chạy 10 buổi phỏng vấn thử; reviewer độc lập đối chiếu transcript, evidence
  và scorecard; so sánh với 10 buổi dùng checklist thủ công

Non-AI alternative:
Dùng interview plan cố định, checklist competency và timer. Cách này rẻ, dễ kiểm soát
và vẫn phải là fallback; nhược điểm là checklist chỉ biết “đã hỏi/chưa hỏi”, không hiểu
được evidence trong câu trả lời đủ mạnh hay chưa.

AI hypothesis:
AI đọc transcript hoặc manual notes, trích evidence có liên kết về source, cập nhật từng
competency thành NOT_ASKED / ASKED_NO_EVIDENCE / WEAK_EVIDENCE / SUFFICIENT_EVIDENCE
và đề xuất follow-up khi còn gap. AI chỉ đề xuất; interviewer quyết định hỏi, bỏ qua hoặc
thay câu hỏi. Khi không đủ evidence, hệ thống phải trả UNKNOWN/INSUFFICIENT_EVIDENCE.

Quick gut:
[ ] No AI / process fix
[ ] Rule
[ ] Workflow
[x] Agent
[ ] Chưa biết
```

**Draft workflow Card #1:**

```text
CURRENT STATE — 45-60 phút/buổi

[Mở plan] → [Hỏi] → [Nghe + ghi note] → [Tự nhớ coverage] → [Tự nghĩ follow-up]
→ [Chuyển competency] → [Rà lại cuối buổi]
                         ^ bottleneck: 5 tác vụ nhận thức diễn ra gần như đồng thời

FUTURE STATE — vẫn 45-60 phút, nhưng coverage và evidence được hỗ trợ liên tục

[Interviewer hỏi] → [Ứng viên trả lời] → [AI trích evidence + gắn source]
→ [AI cập nhật coverage] → [AI đề xuất follow-up/gap]
→ [Interviewer: Ask / Skip / Replace] → [Tiếp tục phỏng vấn]

Human boundary:
- AI không tự hỏi ứng viên, không tự chấm điểm và không ra quyết định tuyển dụng
- Interviewer kiểm tra evidence; Hiring Lead/Hiring Manager giữ quyền quyết định cuối

Fallback:
- Nếu transcript hoặc LLM lỗi, interviewer tiếp tục với plan + checklist + manual notes
- Raw notes/transcript luôn còn để kiểm tra; AI không là single point of failure
```

**File workflow:** [PNG](./01-individual-problem-scan-bo17-workflow-card-1.png) · [SVG nguồn](./01-individual-problem-scan-bo17-workflow-card-1.svg)

---

#### Problem Card #2 — Chuẩn bị interview plan từ Job Description

```text
Problem 1 câu:
Mỗi khi mở một vị trí tuyển dụng, interviewer phải chuyển JD thành competency, trọng số,
câu hỏi, follow-up, expected evidence và rubric bằng tay, dự kiến mất 60-120 phút cho
một interview plan nhưng chất lượng vẫn phụ thuộc kinh nghiệm từng người.

Actor:
Interviewer hoặc Hiring Lead chuẩn bị structured interview cho một job mới, đặc biệt
khi công ty chưa có bộ câu hỏi và competency framework hoàn chỉnh cho vị trí đó.

Thời điểm / bối cảnh:
Sau khi job được tạo và trước buổi phỏng vấn đầu tiên. Áp lực cao khi cần tuyển nhanh,
JD dài hoặc có nhiều yêu cầu kỹ thuật lẫn kỹ năng hành vi.

Current workflow 3-7 bước:
1. Đọc toàn bộ JD và seniority
2. Gạch chân kỹ năng, trách nhiệm và yêu cầu quan trọng
3. Nhóm các yêu cầu thành 5-7 competency
4. Đặt trọng số và định nghĩa expected evidence
5. Tự viết câu hỏi chính và follow-up cho từng competency
6. Tự viết strong/weak answer hoặc scoring rubric
7. Gửi người khác review và sửa plan

Bottleneck:
Bước 3-6 là chuỗi chuyển đổi semantic lặp lại. Interviewer phải vừa hiểu JD, vừa nhớ
framework công ty, vừa soạn nhiều dạng nội dung; thiếu một nguồn tham chiếu thống nhất.

Impact:
- Giả định mất 60-120 phút/interview plan; cần bấm giờ để xác nhận
- Plan 6 competency cần ít nhất 24 thành phần nội dung trước khi review
- Câu hỏi hoặc rubric giữa các interviewer có thể không nhất quán
- Có nguy cơ tập trung quá nhiều vào keyword trong JD và bỏ sót năng lực cốt lõi

Success metric:
- Giảm ≥ 50% thời gian chuẩn bị interview plan so với cách thủ công
- 100% competency có weight, question, expected evidence và rubric trước khi approve
- Question acceptance rate ≥ 70% (được giữ nguyên hoặc chỉ sửa nhẹ)
- 100% plan phải được human approve trước khi dùng
- Cách đo: cùng một interviewer chuẩn bị 5 JD thủ công và 5 JD với BO-17; log thời gian,
  số lần sửa và chấm chất lượng bằng checklist thống nhất

Non-AI alternative:
Dùng thư viện câu hỏi và template cố định theo job family/seniority. Đây là baseline tốt,
ít rủi ro hơn AI; nhược điểm là khó thích nghi với JD mới và vẫn cần người map thủ công.

AI hypothesis:
LLM phân tích nội dung JD và truy xuất competency framework/rubric đã được duyệt để tạo
draft plan có cấu trúc. Người dùng có quyền Approve, Edit, Regenerate, Delete hoặc Add
manual question. AI không được tự publish plan chưa qua human review.

Quick gut:
[ ] No AI / process fix
[ ] Rule
[x] Workflow
[ ] Agent
[ ] Chưa biết
```

**Draft workflow Card #2:**

```text
CURRENT STATE — giả định 60-120 phút/JD

[Đọc JD: 10-20'] → [Tách competency: 15-25'] → [Viết câu hỏi: 20-40']
→ [Viết rubric: 15-30'] → [Review/sửa]
                         ^ bottleneck: chuyển đổi semantic thủ công, lặp lại theo từng JD

FUTURE STATE — mục tiêu giảm ≥ 50% thời gian chuẩn bị

[Nhập JD + seniority] → [AI trích draft competency] → [RAG lấy framework/rubric]
→ [AI sinh plan có cấu trúc] → [Human review + edit] → [Human approve]

Human boundary:
- Human chốt competency, trọng số, câu hỏi và rubric
- AI không được đưa plan vào phỏng vấn nếu chưa có trạng thái APPROVED

Fallback:
- Nếu AI/RAG lỗi, dùng default competency template và editor thủ công
- Lưu rõ nội dung do AI đề xuất và phần human đã sửa để audit
```

**File workflow:** [PNG](./01-individual-problem-scan-bo17-workflow-card-2.png) · [SVG nguồn](./01-individual-problem-scan-bo17-workflow-card-2.svg)

---

#### Problem Card #3 — Tổng hợp scorecard và phân tích disagreement

```text
Problem 1 câu:
Khi một ứng viên được đánh giá bởi nhiều interviewer, Hiring Lead phải tự ghép điểm,
evidence và nhận xét từ nhiều scorecard để phát hiện bất đồng, dự kiến mất 45-90 phút
mỗi candidate trước debrief và vẫn có thể bỏ sót khác biệt về cách hiểu competency.

Actor:
Hiring Lead điều phối debrief cho candidate đã trải qua 2-4 vòng phỏng vấn; Hiring
Manager cần một bản tổng hợp có source để đưa ra quyết định cuối cùng.

Thời điểm / bối cảnh:
Sau khi các interviewer submit scorecard và trước buổi debrief. Khó nhất khi cùng một
competency có chênh lệch điểm lớn nhưng mỗi người viện dẫn một loại evidence khác nhau.

Current workflow 3-7 bước:
1. Mở từng scorecard của các interviewer
2. Copy hoặc ghi lại điểm theo từng competency
3. Tự phát hiện điểm lệch đáng kể
4. Đọc comment/evidence của từng người ở competency bị lệch
5. Tự xác định họ đang đánh giá cùng hay khác subdimension
6. Viết debrief brief: strong, mixed, weak, missing evidence
7. Đưa các câu hỏi chưa rõ vào cuộc họp debrief

Bottleneck:
Bước 4-6: dữ liệu nằm ở nhiều scorecard và evidence dạng text. Phát hiện chênh lệch số
đơn giản, nhưng giải thích vì sao chênh lệch cần đọc và so sánh semantic giữa các nguồn.

Impact:
- 3 interviewer × 6 competency = 18 score cells/candidate cần tổng hợp
- Giả định mất 45-90 phút/candidate để chuẩn bị debrief
- Có nguy cơ lấy trung bình điểm máy móc dù interviewer đánh giá các subdimension khác nhau
- Hiring Lead có thể bỏ sót competency thiếu evidence hoàn toàn

Success metric:
- 100% trường hợp `max(score) - min(score) >= 2` được flag bằng rule
- Giảm ≥ 50% thời gian chuẩn bị debrief brief
- 100% nhận định trong brief liên kết được đến scorecard/evidence gốc
- 0 quyết định Proceed/Additional Interview/Reject được AI tự động thực hiện
- Cách đo: replay 10 bộ scorecard lịch sử đã ẩn danh; so sánh thời gian, số disagreement
  phát hiện được và độ chính xác của source link với bản human review

Non-AI alternative:
Dùng bảng tính tổng hợp điểm và conditional formatting để flag độ lệch. Cách này đủ tốt
cho numerical disagreement và phải được giữ lại; nó không giải thích được hai interviewer
đang dựa vào evidence hoặc subdimension khác nhau.

AI hypothesis:
Rule engine phát hiện disagreement theo ngưỡng xác định trước. Chỉ sau khi rule flag,
LLM mới so sánh evidence và tạo draft explanation/debrief questions. AI không tự average,
không chọn score đúng và không đưa ra kết luận hire/reject; Hiring Lead review toàn bộ.

Quick gut:
[ ] No AI / process fix
[ ] Rule
[x] Workflow
[ ] Agent
[ ] Chưa biết
```

**Draft workflow Card #3:**

```text
CURRENT STATE — giả định 45-90 phút/candidate

[Mở scorecard A/B/C] → [Chép điểm] → [Tìm chênh lệch] → [Đọc từng evidence]
→ [Tự giải thích disagreement] → [Viết debrief brief]
                                  ^ bottleneck: ghép và so sánh text từ nhiều nguồn

FUTURE STATE — mục tiêu giảm ≥ 50% thời gian chuẩn bị debrief

[Thu scorecard đã submit] → [Rule flag score lệch ≥ 2] → [LLM so sánh evidence]
→ [Sinh draft debrief có source link] → [Hiring Lead review/edit]
→ [Human chủ trì debrief và quyết định]

Human boundary:
- Rule chỉ flag; LLM chỉ giải thích và gợi ý câu hỏi
- Hiring Lead/Hiring Manager quyết định score cuối và kết quả tuyển dụng

Fallback:
- Nếu LLM lỗi, hệ thống vẫn hiển thị raw scores, raw evidence và rule flags
- Có thể export bảng tổng hợp để debrief thủ công
```

**File workflow:** [PNG](./01-individual-problem-scan-bo17-workflow-card-3.png) · [SVG nguồn](./01-individual-problem-scan-bo17-workflow-card-3.svg)

---

### 2.3. Card muốn pitch nhất (chuẩn bị 2 phút)

**Card tôi muốn pitch nhất:**

```text
Card #1 — Theo dõi competency coverage và evidence trong lúc phỏng vấn
```

**Vì sao:**

```text
Trong 45-60 phút phỏng vấn, interviewer phải làm ít nhất 5 tác vụ nhận thức gần như
đồng thời: hỏi, nghe, ghi note, đánh giá evidence và theo dõi coverage/thời gian. Điểm
nghẽn không phải interviewer thiếu chuyên môn mà là trạng thái evidence đang phân tán
giữa transcript, notes và trí nhớ. Nếu pilot xác nhận còn 1-2 competency thiếu evidence
mỗi buổi, AI có thể tạo giá trị rõ bằng cách trích evidence, gắn source, cập nhật coverage
và đề xuất follow-up; quyền hỏi, chấm điểm và tuyển dụng vẫn hoàn toàn thuộc về con người.
```

**Câu hỏi tôi muốn nhóm challenge:**

```text
1. Evidence Extractor phải đạt precision/recall bao nhiêu thì suggestion đủ an toàn để
   dùng trong interview mà không khiến interviewer bị dẫn dắt sai?
2. Nếu transcript nhận sai thuật ngữ kỹ thuật hoặc thiếu ngữ cảnh, UX nào giúp interviewer
   kiểm tra source nhanh hơn so với tự ghi note?
3. Liệu checklist + timer + rubric tốt có giải được 80% pain với chi phí và rủi ro thấp hơn
   một AI agent chạy trong buổi phỏng vấn không?
```

**AI phản biện Card:**

- Điểm yếu 1: Đặc tả hiện tại đi từ solution “AI Interview Assist Agent” trước khi có baseline người dùng; chưa chứng minh interviewer thực sự thiếu coverage bao nhiêu.
- Điểm yếu 2: Realtime transcription không nằm trong MVP nhưng Card #1 dễ bị hiểu là phụ thuộc realtime. MVP nên hỗ trợ **manual notes hoặc paste transcript** trước, sau đó mới pilot live transcript.
- Điểm yếu 3: Coverage 95% không tự động đồng nghĩa với interview tốt; hỏi đủ competency nhưng evidence kém vẫn không được chấm.
- Tôi sửa gì: Tách rõ `coverage` và `evidence sufficiency`; giữ trạng thái `INSUFFICIENT_EVIDENCE`; bắt buộc source link và human review; dùng checklist thủ công làm control group trong pilot.

---

## Kế hoạch validation tối thiểu trước khi chốt bài toán

| Hoạt động                 |  Mẫu tối thiểu | Dữ liệu cần thu                                                                  | Quyết định sau validation                    |
| ------------------------- | -------------: | -------------------------------------------------------------------------------- | -------------------------------------------- |
| Phỏng vấn interviewer     |      3-5 người | Cách chuẩn bị plan, số tác vụ trong buổi, pain lớn nhất, mức tin tưởng AI        | Xác định Card#1 hay #2 đau hơn               |
| Bấm giờ workflow hiện tại | 5 JD + 10 buổi | Thời gian chuẩn bị, số competency thiếu evidence, thời gian hoàn thành scorecard | Chốt baseline thay cho số giả định           |
| Audit scorecard ẩn danh   |    30-50 items | Source có tồn tại không, self-claim có bị tính điểm không, score lệch bao nhiêu  | Đo unsupported evidence và disagreement rate |
| Prototype Wizard-of-Oz    |      5-10 buổi | Question acceptance, evidence precision/recall, số lần human override            | Quyết định Go / Not Yet / No-Go cho AI agent |

**Tiêu chí Go sơ bộ:**

```text
- Pain được ít nhất 3/5 interviewer xác nhận là xảy ra thường xuyên
- Baseline cho thấy competency/evidence thực sự bị bỏ sót hoặc tốn thời gian đáng kể
- Evidence extraction đạt precision ≥ 90% trên tập pilot đã human-label
- Không có unsupported evidence đi vào scorecard sau human review
- Workflow vẫn hoạt động khi LLM hoặc transcript không khả dụng
```

**Boundary của đề xuất:**

```text
Trong scope:
- Phân tích JD, tạo draft interview plan, trích evidence, theo dõi coverage
- Draft scorecard, phát hiện disagreement, tạo debrief brief có source
- Human approve/edit/override ở mọi điểm có hệ quả

Ngoài scope:
- Tự động hire/reject hoặc tự xếp hạng ứng viên toàn công ty
- Suy đoán tuổi, giới tính, sắc tộc, cảm xúc, tính cách, ngoại hình hoặc accent
- Face recognition, emotion detection và voice personality analysis
- Coi self-claim là evidence mạnh hoặc gán score khi thiếu evidence
```

### Self-check nộp phần 01

- [x] Có đúng 5 problems và top 3 Problem Cards đủ field
- [x] Mỗi Card có current/future workflow, bottleneck, metric, human boundary và fallback
- [x] Có so sánh với phương án Non-AI / Rule trước khi chọn Workflow hoặc Agent
- [x] Đã chọn 1 card pitch và chuẩn bị câu hỏi challenge đúng chỗ yếu
- [x] Không trao cho AI quyền chấm điểm cuối hoặc quyết định tuyển dụng
- [x] Mọi evidence do AI trích xuất phải liên kết về nguồn
- [ ] Cần thu log/phỏng vấn thật trước khi thay nhãn “giả định” bằng “baseline đã kiểm chứng”
