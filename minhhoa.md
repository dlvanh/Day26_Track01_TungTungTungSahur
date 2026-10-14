# Phần minh hoạ trong repo

Nhóm TungTungTungSahur không có nhóm đối ứng ở chặng 3 (kiểm tra chéo). Theo cho phép của trợ giảng, phần góp ý dưới đây được viết **minh hoạ** để thể hiện cách phản biện theo 4 trục (Phạm vi · Framework · Chỉ số · Hành động). Đây **không** phải biên bản của một buổi phản biện đã diễn ra.

Các phần còn lại của bài (phạm vi, chẩn đoán, bằng chứng E1–E9, dashboard, memo, quyết định) **không** phải minh hoạ: đều lấy từ tài liệu và git log của dự án P-127. E10 (phỏng vấn cán bộ) được ghi rõ là kế hoạch, chưa thực hiện.

## 1. Những gì là minh hoạ

| Vị trí | Nội dung minh hoạ |
| --- | --- |
| `README.md`, mục 1: cột "Góp ý đã đưa cho nhóm bạn" | 6 góp ý cho một **nhóm giả định**, không phải nhóm có thật trong lớp |
| `memo/memo_quyet_dinh.md` §3: cột "Góp ý từ" | Nguồn của 6 thay đổi TĐ1–TĐ6, ghi là nhóm tự rà soát theo từng trục |
| `dashboard/dashboard_hanh_dong_v2.xlsx`, sheet `7_Thay_doi_v1_v2`: cột "Góp ý từ" | Giống memo §3 |

## 2. Góp ý minh hoạ đã "đưa" cho nhóm giả định

**Nhóm giả định:** "Trợ lý AI soạn hợp đồng cho phòng pháp chế". Đây là tình huống được dựng ra để minh hoạ, không gắn với nhóm hay doanh nghiệp nào.

| Thành viên | Trục | Góp ý |
| --- | --- | --- |
| Đỗ Lê Việt Anh | Phạm vi | Đang ôm 5 quy trình và "AI cho cả phòng pháp chế". Đề xuất khoá còn 1 sản phẩm + 3 quy trình (soạn nháp → rà điều khoản → phê duyệt). |
| Nguyễn Thị Minh Khánh | Framework (Gartner-Lite) | Chấm Dữ liệu ĐẠT nhưng kho hợp đồng mẫu không có owner và phiên bản. Đề xuất chấm lại THIẾU và đưa vào nguyên nhân gốc. |
| Lại Bá Quân | Framework (Mollick) | TO-BE chỉ chèn thêm bước "hỏi AI" vào AS-IS. Đề xuất tách rõ điều khoản rủi ro cao (phạt, bồi thường) cho người giữ quyền duyệt. |
| Nguyễn Quang Huy | Chỉ số | Dashboard chỉ có số lượt soạn bằng AI (activity). Đề xuất đổi sang tỷ lệ hợp đồng không bị pháp chế trả về sửa, đo từ log phê duyệt. |
| Lê Thị Châm Anh | Hành động (ADKAR) | Ghi nghẽn ở Desire nhưng giải pháp duy nhất là mở lớp đào tạo. Đề xuất hiển thị điều khoản nguồn để người dùng tự kiểm chứng. |
| Lê Thị Hoài Thương | Hành động (lộ trình) | Cột "khi chỉ số xấu" trống ở 3/5 dòng, lộ trình 30–60–90 không có gate. Đề xuất mỗi dòng có ngưỡng số và một hành động cụ thể. |

## 3. Nguồn minh hoạ của các thay đổi v1 → v2

Không có nhóm nào phản biện bài của nhóm. Sáu thay đổi TĐ1–TĐ6 đến từ việc nhóm **tự rà soát** bản v1 theo 4 trục phản biện; mỗi thay đổi được ghi tên một thành viên phụ trách trục đó:

| Thay đổi | Trục | Thành viên |
| --- | --- | --- |
| TĐ1: "Tỷ lệ AI trả lời" hạ xuống chỉ theo dõi | Chỉ số | Nguyễn Quang Huy |
| TĐ2: bỏ baseline 100% từ eval local | Chỉ số – bằng chứng | Lê Thị Hoài Thương |
| TĐ3: thêm W4 và P2 cho phía dữ liệu | Framework | Nguyễn Thị Minh Khánh |
| TĐ4: hành động khi xấu có ngưỡng số và owner là vai trò | Hành động | Đỗ Lê Việt Anh |
| TĐ5: lộ trình có gate | Hành động – lộ trình | Lê Thị Châm Anh |
| TĐ6: chỉ số giá trị đo từ log thay cho số tự khai | Chỉ số – giá trị | Lại Bá Quân |

Bản v1 vẫn được giữ ở `v1/dashboard_hanh_dong_v1.xlsx`, nên có thể đối chiếu từng thay đổi với bản v2.
