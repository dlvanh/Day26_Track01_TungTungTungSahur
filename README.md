# Day26 · Track01 — Nhóm TungTungTungSahur

**Use case:** UniPilot (P-127), Trợ lý AI Tuyển sinh.

**Nội dung repo:**
- [`dashboard/dashboard_hanh_dong_v2.xlsx`](dashboard/dashboard_hanh_dong_v2.xlsx): bản cuối, sau kiểm tra chéo.
- [`memo/memo_quyet_dinh.md`](memo/memo_quyet_dinh.md): memo quyết định.
- [`v1/dashboard_hanh_dong_v1.xlsx`](v1/dashboard_hanh_dong_v1.xlsx): bản trước phản biện, giữ lại để đối chiếu.

Dashboard v2 có 8 sheet: phạm vi, chẩn đoán (5 câu hỏi · Gartner-Lite · Mollick · ADKAR), bằng chứng, AS-IS/TO-BE, lộ trình 30–60–90, Dashboard, thay đổi v1→v2, và sheet tự kiểm tính bằng công thức.

## 1. Thành viên

> Cột “Góp ý đã đưa cho nhóm bạn” và cột “Góp ý từ” (memo §3, sheet `7_Thay_doi_v1_v2`) là **minh hoạ**, viết theo cho phép của trợ giảng. Chi tiết ở [`minhhoa.md`](minhhoa.md).

| Họ tên | MSSV | Phần phụ trách | Góp ý đã đưa cho nhóm bạn |
| --- | --- | --- | --- |
| Đỗ Lê Việt Anh | 2A202602491 | Khoá phạm vi, chốt nguyên nhân gốc, memo quyết định | *Minh hoạ → nhóm giả định “Trợ lý AI soạn hợp đồng cho phòng pháp chế”* — Phạm vi: đang ôm 5 quy trình và “AI cho cả phòng pháp chế”; đề xuất khoá còn 1 sản phẩm + 3 quy trình (soạn nháp → rà điều khoản → phê duyệt). |
| Nguyễn Thị Minh Khánh | 2A202602546 | Gartner-Lite, readiness dữ liệu (data owner, lịch cập nhật nguồn) | *Minh hoạ → nhóm giả định “Trợ lý AI soạn hợp đồng cho phòng pháp chế”* — Framework: Gartner-Lite chấm Dữ liệu ĐẠT nhưng kho hợp đồng mẫu không có owner và phiên bản; đề xuất chấm lại THIẾU và đưa vào nguyên nhân gốc. |
| Lại Bá Quân | 2A202602495 | Mollick (ma trận chủ đề người–AI), AS-IS / TO-BE | *Minh hoạ → nhóm giả định “Trợ lý AI soạn hợp đồng cho phòng pháp chế”* — Framework: TO-BE chỉ chèn thêm bước “hỏi AI” vào AS-IS; đề xuất dùng Mollick tách rõ điều khoản rủi ro cao (phạt, bồi thường) cho người giữ quyền duyệt. |
| Nguyễn Quang Huy | 2A202602421 | Dashboard chỉ số: product/workflow metric, nguồn log, ngưỡng và hành động | *Minh hoạ → nhóm giả định “Trợ lý AI soạn hợp đồng cho phòng pháp chế”* — Chỉ số: dashboard chỉ có số lượt soạn bằng AI (activity); đề xuất đổi sang tỷ lệ hợp đồng không bị pháp chế trả về sửa, đo từ log phê duyệt. |
| Lê Thị Châm Anh | 2A202602846 | ADKAR, kế hoạch hỗ trợ cán bộ, lộ trình 30–60–90 | *Minh hoạ → nhóm giả định “Trợ lý AI soạn hợp đồng cho phòng pháp chế”* — Hành động: ADKAR ghi nghẽn ở Desire nhưng giải pháp duy nhất là mở lớp đào tạo; đề xuất hiển thị điều khoản nguồn để người dùng tự kiểm chứng. |
| Lê Thị Hoài Thương | 2A202602898 | Thu thập bằng chứng (log eval, git log, mã nguồn), tổng hợp thay đổi v1 → v2 | *Minh hoạ → nhóm giả định “Trợ lý AI soạn hợp đồng cho phòng pháp chế”* — Hành động: cột “khi chỉ số xấu” trống ở 3/5 dòng và lộ trình 30–60–90 không có gate; đề xuất mỗi dòng có ngưỡng số và một hành động cụ thể. |

## 2. Phạm vi

**1 sản phẩm:** UniPilot (P-127), pilot tại ĐH Công nghệ – ĐHQGHN. **1 nhóm người dùng chính:** cán bộ tư vấn tuyển sinh UET. **3 quy trình:** (WF1) trả lời câu hỏi lặp lại về điểm chuẩn, IELTS, học phí, học bổng · (WF2) chuyển giao ca khó qua Live Inbox · (WF3) cập nhật tri thức khi có văn bản mới.
**Vấn đề:** AI đã được triển khai nhưng chưa là bước trả lời chính thức, vì chưa ai chứng minh được câu trả lời nào đúng và còn hiệu lực.

## 3. Nguyên nhân gốc

**NN1:** chuỗi tin cậy bị đứt. Nguồn dữ liệu không có người phụ trách và lịch cập nhật; đầu ra không có QA mẫu và không có kênh báo sai. Framework: Gartner-Lite (Dữ liệu và Absorption THIẾU) + ADKAR (Desire nghẽn).
**NN2:** chưa chia lại việc người–AI theo mức rủi ro của từng chủ đề, và chưa có owner cho chất lượng câu trả lời. Framework: Mollick + ADKAR (Awareness nghẽn).
**Bằng chứng**, lấy từ log và tài liệu repo P-127:
- Eval ngày 26/09/2026 chỉ trả lời được 11/20 câu (55%) và từ chối đúng 0/4 câu.
- 0/11 kịch bản kiểm thử đã chạy.
- 2 lỗi số liệu nguồn (học phí, bảng IELTS lẫn năm) chỉ được phát hiện qua commit sửa code.
- Dashboard admin chỉ đo activity.
- Case tham khảo: *Moffatt v. Air Canada* (2024) và nghiên cứu "Jagged Frontier" (2023).

## 4. Cách làm mới

- **Nguồn kiểm chứng:** mọi câu trả lời phải kèm trích nguồn và năm áp dụng. Mỗi nhóm tài liệu (5 nhóm) có data owner; tài liệu chỉ được bật sau khi eval hồi quy đạt.
- **Người chịu trách nhiệm:** tổ trưởng tổ tư vấn là QA owner (QA mẫu 50 hội thoại/tuần). Học phí, học bổng, quy đổi IELTS chuyển sang chế độ AI soạn nháp, cán bộ duyệt. Trưởng ban tuyển sinh là chủ nghiệp vụ.
- **Khi AI không chắc:** AI chuyển người kèm tóm tắt hội thoại. Cán bộ đóng ticket phải ghi nguyên nhân; nguyên nhân "thiếu dữ liệu" tự tạo đề xuất cho data owner. Có nút "Báo sai" cho thí sinh và cán bộ. Lỗi nghiêm trọng thì bật kill-switch cho chủ đề đó trong vòng 1 giờ.

## 5. Chỉ số

Trích từ sheet `Dashboard` của bản v2 (đủ 12 chỉ số ở đó):

| Loại | Chỉ số | Baseline | Target | Nguồn | Owner |
| --- | --- | --- | --- | --- | --- |
| Product | **P1** Tỷ lệ câu trả lời đúng và còn hiệu lực (QA mẫu) | Chưa có trên hội thoại thật, đo tuần 1–2 (eval local chỉ để tham chiếu: trả lời được 11/20 câu) | ≥90% (≥95% với chủ đề rủi ro cao) | Phiếu QA mẫu từ bảng messages + citations | Tổ trưởng tổ tư vấn |
| Product | **P3** Số lỗi nghiêm trọng đến tay thí sinh | Chưa có kênh ghi nhận; 2 lỗi nguồn được sửa qua commit | 0/tháng | Nút Báo sai + QA mẫu + khiếu nại | Trưởng ban tuyển sinh |
| Workflow | **W1** Tỷ lệ câu lặp lại AI xử lý xong mà cán bộ không phải làm lại | Đo tuần 1–2 từ log | ≥75% | conversations + tickets | Tổ trưởng tổ tư vấn |
| Workflow | **W4** Độ trễ cập nhật nguồn | Không đo được; 0/5 nhóm tài liệu có owner | ≤3 ngày làm việc; 5/5 có owner | knowledge_documents | Data owner từng nhóm |

Mỗi chỉ số trong file đều có ngưỡng xấu và hành động khi xấu. "Tỷ lệ AI trả lời" chỉ còn là chỉ số theo dõi, không dùng để ra quyết định.

## 6. Quyết định

**SỬA.** Tiếp tục pilot tại UET, nhưng AI chỉ tự động trả lời các chủ đề rủi ro thấp; học phí, học bổng và IELTS chuyển sang nháp–duyệt; chưa mở rộng sang trường khác trước gate 90 ngày.
**Lý do:** hướng đi đúng và kỹ thuật đã đủ, nhưng chất lượng chưa được chứng minh trên hội thoại thật và nguồn chưa có người phụ trách.
**Thay đổi so với v1** (6 thay đổi, chi tiết ở sheet `7_Thay_doi_v1_v2` và memo §3), hai thay đổi chính:
- "Tỷ lệ AI trả lời" từ chỉ số quyết định hạ xuống chỉ theo dõi, thay bằng W1 và P1.
- Baseline 100% lấy từ eval local được bỏ, thay bằng QA mẫu trên hội thoại thật. Thêm W4 để đo phía dữ liệu của NN1.

---
*Toàn bộ số liệu lấy từ tài liệu và git log công khai trong repo dự án P-127. Không chứa dữ liệu cá nhân của thí sinh hay khoá API. Các ô ghi "đo tuần 1" là số cần thu thập, không phải số giả định.*
