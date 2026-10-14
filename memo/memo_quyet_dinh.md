# Memo quyết định — UniPilot (P-127) · Trợ lý AI Tuyển sinh

**Gửi:** Trưởng ban tuyển sinh UET · Product lead P-127
**Ngày:** 14/10/2026 · **Phiên bản:** sau kiểm tra chéo (khớp `dashboard/dashboard_hanh_dong_v2.xlsx`)
**Quyết định đề xuất:** 🟡 **SỬA** — tiếp tục pilot tại UET nhưng thu hẹp phạm vi AI tự động; chưa mở rộng sang trường khác.

---

## 1. Vấn đề và nguyên nhân gốc

**Phạm vi:** UniPilot × cán bộ tư vấn tuyển sinh UET × 3 quy trình: (WF1) trả lời câu hỏi lặp lại, (WF2) chuyển giao ca khó qua Live Inbox, (WF3) cập nhật tri thức khi trường ban hành văn bản mới.

**Vấn đề quan sát được (triệu chứng):** UniPilot đã được *triển khai* (deployment) với đủ RAG có trích nguồn, guardrail, Live Inbox và kill-switch, nhưng chưa được *áp dụng* (adoption): AI chưa phải là một bước đáng tin trong quy trình tư vấn. Chưa ai chứng minh được câu trả lời nào đúng và còn hiệu lực, còn dashboard thì chỉ đếm tỷ lệ AI trả lời, token và chi phí.

Hỏi tiếp *"vì sao?"* thì ra hai nguyên nhân gốc:

| Mã | Nguyên nhân gốc |
| --- | --- |
| **NN1** | **Chuỗi tin cậy bị đứt ở hai đầu.** Đầu vào: nguồn dữ liệu không có người phụ trách và lịch cập nhật. Đầu ra: không có QA mẫu và không có kênh báo sai. Vì vậy không ai chứng minh được câu trả lời đúng và còn hiệu lực. |
| **NN2** | **Chưa thiết kế lại cách chia việc người–AI.** Chưa có ma trận "chủ đề nào AI tự động / AI soạn nháp – người duyệt / người giữ quyền", chưa có owner cho chất lượng câu trả lời, và luồng bàn giao người↔AI còn chưa ổn định. |

"Cán bộ ít dùng" hay "chưa được đào tạo" **không** phải nguyên nhân gốc. Nút nghẽn nằm ở Desire và Awareness (xem §2), nên mở lớp đào tạo không giải quyết được.

## 2. Framework đã dùng và bằng chứng

| Framework | Dùng cho | Kết luận | Dẫn tới |
| --- | --- | --- | --- |
| **Gartner-Lite** | Readiness của tổ chức | Direction **ĐẠT**: PRD rõ mục tiêu, pilot 1 trường. Dữ liệu **THIẾU**: 0/5 tệp nguồn có người phụ trách. Governance **MỘT PHẦN**: có RBAC và kill-switch nhưng chưa quy định chủ đề nào AI được tự trả lời. Vận hành và học từ lỗi **THIẾU**. | NN1 |
| **Mollick** | Chia việc người–AI | Ba vùng chưa được định nghĩa. Học phí, học bổng, quy đổi IELTS là chủ đề rủi ro cao nhưng AI đang trả lời thẳng mà không ai kiểm. | NN2 |
| **ADKAR** | Cán bộ tư vấn kẹt ở đâu | **Awareness NGHẼN** (không biết loại câu nào giao AI) và **Desire NGHẼN** (ngại chịu trách nhiệm khi AI sai số tiền hoặc điều kiện). Knowledge, Ability, Reinforcement: cần làm. | NN1 + NN2 |

Ba framework dẫn về cùng một chỗ: không có cơ chế chứng minh chất lượng, và không có phân vai rõ ràng. Đây là lý do cán bộ không thể tin AI.

**Bằng chứng** (chi tiết ở sheet `3_Bang_chung`):

- **Log eval (E1):** lần chạy ngày 26/09/2026 trả lời được 11/20 câu có đáp án (**55%**), đúng 11/11 câu đã trả lời, và từ chối đúng **0/4** câu thiếu dữ liệu. Judge cùng họ Gemini với model trả lời, nên đánh giá chưa độc lập.
- **Tài liệu dự án (E2, E3):** `eval/results/report.md` có **0/11** kịch bản kiểm thử đã chạy. Benchmark 75 câu chưa chạy đủ. Bảng học phí ghi "do người dùng cung cấp, chưa ghi năm áp dụng hoặc văn bản nguồn".
- **Dấu hiệu trong workflow (E4, E6):** commit `7c201d4` sửa học phí 2 ngành, commit `6a2a037` gắn nhãn năm cho bảng quy đổi IELTS (lỗi lẫn năm). Cả hai lỗi đều do dev phát hiện chứ không qua kênh vận hành. Riêng ngày 11/10 có 5 commit sửa luồng hủy chuyển giao.
- **Quan sát sản phẩm (E5):** dashboard admin chỉ có tỷ lệ AI trả lời, token, chi phí và cache. Không có chức năng báo sai cho từng câu trả lời.
- **Case tham khảo (E8, E9):** vụ *Moffatt v. Air Canada* (2024) cho thấy tổ chức phải chịu trách nhiệm về thông tin sai do chatbot của mình đưa ra. Nghiên cứu "Jagged Frontier" (Dell'Acqua, Mollick và cộng sự, 2023) cho thấy tác vụ nằm ngoài biên năng lực của AI thì cần người giữ.
- **Còn thiếu:** chưa phỏng vấn cán bộ (E10). Việc này được đưa vào điều kiện của gate 30 ngày.

## 3. Thay đổi sau phản biện (v1 → v2)

*Góp ý minh hoạ, viết theo cho phép của trợ giảng: nhóm không có nhóm đối ứng ở chặng 3, nên các thay đổi đến từ tự rà soát theo 4 trục phản biện.*

| # | Bản v1 | Bản v2 | Góp ý từ |
| --- | --- | --- | --- |
| **TĐ1** | "Tỷ lệ AI trả lời" là chỉ số quyết định, mục tiêu ≥75% | Hạ xuống chỉ theo dõi (T1). Thay bằng **W1**: tỷ lệ câu lặp lại AI xử lý xong mà cán bộ không phải làm lại, và **P1**: QA mẫu 50 hội thoại thật mỗi tuần | *Minh hoạ: tự rà soát theo trục Chỉ số (Nguyễn Quang Huy)* |
| **TĐ2** | Baseline chất lượng = 100% (11/11, eval local) | P1 chưa có baseline cho tới khi đo trên hội thoại thật với 2 người chấm độc lập. Thêm **P4** (từ chối đúng, baseline 0/4) | *Minh hoạ: tự rà soát theo trục Chỉ số – bằng chứng (Lê Thị Hoài Thương)* |
| **TĐ3** | Không có chỉ số nào cho phía dữ liệu của NN1 | Thêm **W4** (độ trễ cập nhật nguồn, mục tiêu 5/5 nhóm tài liệu có owner) và **P2** (có nguồn kèm năm áp dụng) | *Minh hoạ: tự rà soát theo trục Framework (Nguyễn Thị Minh Khánh)* |
| **TĐ4** | Cột "khi chỉ số xấu" chung chung; owner là "Nhóm P-127" | Mỗi dòng có ngưỡng bằng số, hành động có thời hạn, và owner là một vai trò trong tổ chức | *Minh hoạ: tự rà soát theo trục Hành động (Đỗ Lê Việt Anh)* |
| **TĐ5** | Lộ trình 30–60–90 là danh sách việc | Mỗi giai đoạn có gate định lượng và owner riêng, kèm quy tắc mở rộng / sửa / dừng | *Minh hoạ: tự rà soát theo trục Hành động – lộ trình (Lê Thị Châm Anh)* |
| **TĐ6** | Mục tiêu "+10% tỷ lệ nộp hồ sơ" và CSAT là chỉ số quyết định | Tỷ lệ nộp hồ sơ chuyển sang theo dõi (V2, mục tiêu "không giảm"). Giá trị đo bằng **V1**: giờ cán bộ tính từ log, thay cho số tự khai 4–6 giờ/ngày | *Minh hoạ: tự rà soát theo trục Chỉ số – giá trị (Lại Bá Quân)* |

## 4. Quyết định: **SỬA**

**Tiếp tục pilot tại UET, nhưng:**

1. AI chỉ **tự động** trả lời nhóm chủ đề rủi ro thấp: điểm chuẩn lịch sử, ngành và tổ hợp, hướng dẫn sử dụng, thủ tục đã công bố.
2. Học phí, học bổng và quy đổi IELTS chuyển sang chế độ **AI soạn nháp, cán bộ duyệt** cho tới khi QA mẫu của từng chủ đề đạt ≥95%.
3. **Chưa mở rộng** sang tenant khác cho tới gate 90 ngày.

**Lý do (một câu):** Hướng đi đúng và kỹ thuật đã đủ, nhưng chất lượng chưa được chứng minh trên hội thoại thật và nguồn dữ liệu chưa có người phụ trách, nên mở rộng lúc này chỉ nhân thêm rủi ro sai số liệu.

**Vì sao không DỪNG:** Direction đạt, và các cơ chế an toàn cần thiết (grounding, guardrail, kill-switch, Live Inbox) đã có sẵn. Thứ còn thiếu là quy trình và đo lường, phần này sửa được trong 90 ngày.

## 5. Bước tiếp theo và owner

| Giai đoạn | Việc chính | Owner | Gate / dấu hiệu hoàn thành |
| --- | --- | --- | --- |
| **0–30 ngày**<br>Chứng minh vấn đề | Phỏng vấn 3 cán bộ và quan sát 1 ca trực. Chốt ma trận chủ đề. Chỉ định data owner cho 5 nhóm tài liệu. Chạy đủ eval 75 câu và 11 kịch bản kiểm thử. Đo baseline QA mẫu. Thêm nút "Báo sai" và trường "nguyên nhân đóng ticket". | Product lead P-127 + Trưởng ban tuyển sinh UET | Có baseline cho đủ 9 chỉ số quyết định. 5/5 nhóm tài liệu có owner. Nếu chưa đạt thì kéo dài 2 tuần và **không** bật thêm chủ đề. |
| **31–60 ngày**<br>Chứng minh chất lượng | Bật chế độ nháp–duyệt. Hiển thị nguồn kèm năm áp dụng. QA mẫu hằng tuần. Hướng dẫn 45 phút và 1 tuần đi kèm (shadow). | Tổ trưởng tổ tư vấn (QA owner) + Tech lead AI | QA đúng ≥90% trong 3 tuần liên tiếp. 0 lỗi nghiêm trọng. Độ trễ cập nhật nguồn ≤3 ngày làm việc. |
| **61–90 ngày**<br>Quyết định mở rộng | So sánh với mục tiêu. Chuyển các chủ đề đạt ≥95% sang tự động. Rà soát governance (NĐ 13/2023). | Trưởng ban tuyển sinh UET | **Mở rộng** nếu P1, P3, W1 đạt và ≥7/9 chỉ số quyết định đạt. **Sửa** nếu chất lượng đạt nhưng quy trình chưa đạt. **Dừng chủ đề** nếu QA <80% hoặc có ≥2 lỗi nghiêm trọng/tháng. |

**Quy tắc khẩn:** nếu có bất kỳ lỗi nghiêm trọng nào đến tay thí sinh (P3 ≥1), trong vòng 1 giờ phải bật kill-switch cho chủ đề đó, liên hệ thí sinh bị ảnh hưởng, và làm post-mortem trong 48 giờ.
