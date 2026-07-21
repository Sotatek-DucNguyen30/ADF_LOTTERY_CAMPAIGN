Nhiệm vụ: mở file output đã có sheet "Screen_SLC0104 重複チェック", ĐỐI CHIẾU và BỔ SUNG
(không tạo sheet mới) cho ĐÚNG 1 màn hình SLC0104.

═══════════════════════════════════════════════════════════════
A. NGUYÊN TẮC CỐT LÕI (đọc hết trước khi làm bất kỳ bước nào)
═══════════════════════════════════════════════════════════════

【NC1 — KHÔNG SUY DIỄN】
Mọi field/button/action/business rule đưa vào sheet PHẢI có ít nhất 1 trong 3 bằng chứng:
  (a) Nhìn thấy trực tiếp trong ảnh UI — mô tả được vị trí/hình dạng/text.
  (b) Trích dẫn nguyên văn từ Feature List (cột G) — ghi rõ Feature List No.
  (c) Trích dẫn nguyên văn từ Comment Figma (cột E/F) — ghi rõ Comment Figma No.
Chỉ cần 1 trong 3 là đủ. Bằng chứng (a) một mình đã đủ mạnh, không cần (b)/(c) bổ trợ.
KHÔNG có bằng chứng nào → KHÔNG đưa vào. Ghi "-" thay vì đoán.
CẤM suy diễn theo "pattern UI phổ biến" / "form thường có nút X" / "theo thông lệ thiết kế".
Áp dụng cho MỌI nơi trong sheet: bảng mục 3/4, text tự do mục 1/2, block sub-screen mục 5.

【NC2 — THỨ TỰ ƯU TIÊN NGUỒN】
(1) Ảnh UI gốc = NGUỒN CHÍNH. Field nhìn thấy trên ảnh PHẢI vào sheet, kể cả khi Feature
    List / Comment Figma không nhắc.
(2) Feature List + Comment Figma = BỔ SUNG (Required, Validation Rule, logic ẩn). Không được
    dùng làm điều kiện lọc field từ ảnh.

【NC3 — KHÔNG GỘP FIELD】
Mỗi ô input/output trên ảnh = 1 dòng riêng trong bảng mục 3, tên field = label CHÍNH XÁC
trên ảnh. TUYỆT ĐỐI KHÔNG gộp nhiều field thành 1 dòng tổng quát.
Đặc biệt với BẢNG/DANH SÁCH LẶP LẠI: nếu ảnh hiển thị bảng có N dòng dữ liệu thật (VD
mapping field→cột CSV), PHẢI liệt kê ĐẦY ĐỦ từng dòng (VD "氏名 → cột AA", "メールアドレス
→ cột AB"...), KHÔNG được tóm tắt thành 1-2 dòng header chung ("フィールド名", "マッピング列").
Nếu ảnh không đủ rõ để đọc hết, liệt kê dòng đọc rõ + ghi "⚠ ảnh có thêm N dòng không đọc
rõ — cần xác nhận".
Kiểm tra: đếm số ô input trên ảnh = số dòng trong bảng mục 3. Không khớp → tìm và bổ sung.

【NC4 — STATUS CHỈ THUỘC MÀN HÌNH LIST】
Field "ステータス"/"Status" KHÔNG được xuất hiện ở màn hình Settings/Create/Edit (SLC0101–
SLC0206). Chỉ thuộc màn hình List (SLC0301...). Mặc định KHÔNG thêm trừ khi có bằng chứng
cực kỳ rõ ràng từ ảnh UI.

【NC5 — REQUIRED CHỈ KHI CÓ DẤU ※】
Chỉ ghi Required="Có" khi Feature List cột G có dấu ※ gắn TRỰC TIẾP vào tên field đó
(VD "CPID※"). Phải trích nguyên văn cụm từ có ※ trước khi gán.
Giá trị hệ thống tự tính (status, số tự sinh, kết quả tính toán) → I/O="Output",
Required="-", Validation Rule = mô tả logic tự tính.

【NC6 — CẤU TRÚC MAIN SCREEN + SUB-SCREEN】
Nếu Screen ID có nhiều state (VD 6 state của SLC0104, 2 state 作成前/作成後 của SLC0101...):

▸ MAIN SCREEN chỉ giữ 2 mục (tránh trùng lặp với sub-screen):
  (1) Screen Overview — mô tả tổng quan chung cho toàn bộ Screen ID (context, mục đích,
      URL, display conditions, initial behavior, business rules chung).
  (2) Screen Layout — mô tả layout tổng thể + CHÈN ẢNH UI của TẤT CẢ state (như hiện tại
      ở mục 2: mỗi state 1 ảnh kèm label, người đọc thấy toàn cảnh các state).
  ⚠ KHÔNG có mục 3 (Input/Output) và mục 4 (Actions) ở main screen — vì đó là "union"
  trùng lặp với nội dung đã viết chi tiết ở từng sub-screen bên dưới.

▸ MỖI SUB-SCREEN (state) = 1 MÀN HÌNH RIÊNG ĐẦY ĐỦ 4 mục:

  (1) Screen Overview — mô tả tổng quan state này (context, khác gì so với state khác).

  (2) Screen Layout Description — mô tả layout CỤ THỂ cho state này + CHÈN ẢNH UI TRỰC TIẾP
      vào ngay dưới dòng (2) bằng openpyxl add_image.
      ⚠ PHẢI copy ảnh từ thư mục ảnh UI gốc (hoặc từ mục 2 nếu cùng ảnh) và INSERT vào đúng
      vị trí trong block sub-screen này. TUYỆT ĐỐI KHÔNG chỉ viết text tham chiếu kiểu
      "参照画像: mục2 ①適格条件追加前" — đó KHÔNG phải là gắn ảnh.
      Mỗi sub-screen phải có ảnh NHÌN THẤY ĐƯỢC ngay trong block của nó.

  (3) Input/Output Items — BẢNG ĐẦY ĐỦ CÁC CỘT giống hệt cấu trúc bảng chuẩn:
      No | Display Item Name | Type | Required | I/O | Data Type | Max Length |
      Default Value | Validation Rule | Error Message | Remarks
      Liệt kê CHỈ các field THUỘC RIÊNG state này (xuất hiện trên ảnh UI của state này).
      Mỗi field = 1 dòng riêng với đầy đủ tất cả cột.

  (4) Screen Actions — BẢNG ĐẦY ĐỦ CÁC CỘT giống hệt cấu trúc bảng chuẩn:
      No | Action Name | Event | Input Information | Output/Destination |
      Processing Details | Error Handling
      Liệt kê CHỈ các action THUỘC RIÊNG state này.

  Breadcrumb, button đặc thù từng state phải nằm đúng block tương ứng.

  ⚠ TUYỆT ĐỐI KHÔNG viết kiểu tóm tắt 1 dòng như:
     "(3) Input/Output: 条件を選択(Dropdown)、この条件を削除(Link)。※mục3 No.4,21参照。"
  PHẢI viết thành BẢNG có đầy đủ cột, mỗi field 1 dòng riêng.

【NC7 — ERROR MESSAGE CHUẨN HOÁ】
Mọi field Required="Có" dùng CHUNG: 「必須項目を入力してください。」
Ngoại lệ: ảnh UI/Comment Figma hiển thị rõ message khác (lỗi format, trùng lặp) → giữ riêng.

【NC8 — GIÁ TRỊ MẶC ĐỊNH CHO Ô KHÔNG XÁC ĐỊNH】
Khi không có đủ thông tin cho 1 cột (Required, Validation Rule, Error Message, Remarks...)
và không trích dẫn được nguồn → ghi "-" (KHÔNG ghi "TBD - cần xác nhận", KHÔNG tự đoán).

【NC9 — REMARKS PHẢI CÓ NỘI DUNG THẬT, KHÔNG GHI SỐ SUÔNG】
Cột Remarks (và Error Handling) PHẢI ghi NỘI DUNG CỤ THỂ, không được chỉ ghi số tham chiếu.

  ❌ SAI (chỉ ghi số, không biết nói gì):
     "Comment Figma No.19,29。"
     "画像/Comment Figma。"
     "- (Comment Figma No.16)"

  ✅ ĐÚNG (trích nội dung chính):
     "Theo Comment Figma No.19: 条件を選択すると、それに合わせた入力欄が表示される"
     "Theo Comment Figma No.17: 1つ目は AND/OR を表示しない"
     "Quan sát từ ảnh UI (state 適格条件選択): date picker hiển thị 以降/以前"

  Quy tắc:
  - Khi cite Comment Figma → ghi "Theo Comment Figma No.X: [trích nguyên văn cột F
    Comment_VN hoặc cột E Comment_JP — ưu tiên VN nếu có]".
  - Khi cite Feature List → ghi "Theo Feature List No.X: [trích nguyên văn cụm liên quan
    từ cột G]".
  - Khi cite ảnh UI → ghi "Quan sát từ ảnh UI (state/ảnh nào): [mô tả ngắn bằng chứng]".
  - Nếu KHÔNG có nội dung gì đáng ghi → để "-". KHÔNG ghi số tham chiếu trống rỗng.

═══════════════════════════════════════════════════════════════
B. INPUT FILES (path cố định)
═══════════════════════════════════════════════════════════════

1. Output đang sửa:
   /home/sotatek/DucNguyen/ADF_Lottery_Campaign/output/[Lottery Campaign ] Screen Definition_10072026_Ver1.0.xlsx
   (nếu có bản mới hơn → dùng file mới nhất trong thư mục output/)

2. Ảnh UI gốc (thư mục):
   /home/sotatek/DucNguyen/ADF_Lottery_Campaign/inputs/screen-detail/image-screen

3. Feature List:
   /home/sotatek/DucNguyen/ADF_Lottery_Campaign/inputs/requirement/business-requirement/[Lottery Campaign] Feature_List_20260629_Mapping.xlsx
   Sheet: "Danh sách chức năng (phiên bản " (CHỈ dùng sheet này)
   Cột: A=No, B=Hệ thống con, C=Phân loại lớn, D=Phân loại trung, E=Phân loại nhỏ,
   F=Chi tiết chức năng, G=Tổng quan chức năng, H=Tài liệu tham khảo, I=Điều chỉnh phạm vi.

4. Comment Figma:
   /home/sotatek/DucNguyen/ADF_Lottery_Campaign/inputs/screen-detail/spec-note/[Lottery Campaign] _Comment Figma_Ver1.0.xlsx
   Sheet: "Comment Figma"
   Cột: A=No, B=ID Màn hình (merged cell), C=Tên màn hình_JP (merged cell),
   D=Field comment, E=Comment_JP, F=Comment_VN (dùng trực tiếp, KHÔNG tự dịch lại),
   G=Image (ảnh nằm ở inputs/screen-detail/image-note/, KHÁC thư mục ảnh UI), H=Note.

═══════════════════════════════════════════════════════════════
C. CÁC BƯỚC THỰC HIỆN (tuần tự, KHÔNG bỏ bước)
═══════════════════════════════════════════════════════════════

────────────────────────────────────────
BƯỚC 0 — KIỂM TRA FILE TỒN TẠI
────────────────────────────────────────
```python
import os
files_to_check = {
    "Output": r"/home/sotatek/DucNguyen/ADF_Lottery_Campaign/output/[Lottery Campaign ] Screen Definition_10072026_Ver1.0.xlsx",
    "Ảnh UI (thư mục)": r"/home/sotatek/DucNguyen/ADF_Lottery_Campaign/inputs/screen-detail/image-screen",
    "Feature List": r"/home/sotatek/DucNguyen/ADF_Lottery_Campaign/inputs/requirement/business-requirement/[Lottery Campaign] Feature_List_20260629_Mapping.xlsx",
    "Comment Figma": r"/home/sotatek/DucNguyen/ADF_Lottery_Campaign/inputs/screen-detail/spec-note/[Lottery Campaign] _Comment Figma_Ver1.0.xlsx",
}
missing = [name for name, path in files_to_check.items() if not os.path.exists(path)]
if missing:
    raise SystemExit(f"DỪNG — không tìm thấy: {missing}. Báo người dùng, KHÔNG tiếp tục.")
print("✓ Đủ 4 file/thư mục — tiếp tục BƯỚC 1.")
```
Nếu thiếu file: DỪNG NGAY, báo người dùng. KHÔNG chạy tiếp với dữ liệu thiếu.

────────────────────────────────────────
BƯỚC 0.5 — KÍCH HOẠT SKILL (ADF Phase ② Design)
────────────────────────────────────────
Agent: `ui-ux-designer`
Skills:
  • `ui-ux-pro-max` — dùng cho BƯỚC 1 (phân tích layout/component từ ảnh UI gốc).
  • `design-system` — chuẩn hoá Type/Validation Rule khớp taxonomy đã dùng ở các sheet
    Screen khác đã có trong file output (đọc lại các sheet cũ để giữ nhất quán).

────────────────────────────────────────
BƯỚC 1 — PHẦN A: PHÂN TÍCH ẢNH UI GỐC
────────────────────────────────────────

1a. Tìm ảnh UI cho SLC0104:
    - Đọc ws._images trong sheet hiện tại. Nếu không có ảnh → tìm file ảnh trong thư mục
      inputs/screen-detail/image-screen/ theo tên Screen Name.

1b. Phân tích TỪ ĐẦU (không neo theo bảng cũ):
    Liệt kê MỌI component nhìn thấy: label, input, button, dropdown, checkbox, radio,
    table + từng cột, breadcrumb, tab, icon action, thông báo...
    Với MỖI component: ghi bằng chứng ngắn gọn (VD "nút xanh góc dưới phải, text '保存'").
    Không mô tả được bằng chứng → KHÔNG liệt kê.

1c. Áp dụng NC3 (không gộp):
    - Mỗi ô input/output = 1 dòng riêng, tên = label chính xác trên ảnh.
    - Bảng/danh sách lặp: liệt kê TỪNG DÒNG dữ liệu thật, không tóm tắt thành header.
    - Đếm tổng số ô input trên ảnh → ghi nhớ con số này (dùng ở BƯỚC 4 verify).

────────────────────────────────────────
BƯỚC 2 — PHẦN B: ĐỐI CHIẾU FEATURE LIST + COMMENT FIGMA
────────────────────────────────────────

2a. Feature List — Lọc dòng liên quan SLC0104:
    Tìm dòng có cột D/E/F khớp ngữ nghĩa với Screen Name.
    Với mỗi dòng, đọc cột I (Điều chỉnh phạm vi):
    • Trống → dùng toàn bộ cột G.
    • "Loại khỏi phạm vi" → BỎ QUA HOÀN TOÀN.
    • "Điều chỉnh một phần phạm vi (...)" → chỉ bỏ phần trong ngoặc, phần còn lại dùng.
      Không chắc → ghi "-".
    • "※Bổ sung ..." → dùng bình thường.

    Trích xuất từ cột G:
    - Field có dấu ※ → Required="Có" (trích nguyên văn cụm "tên_field※" làm bằng chứng).
    - Field KHÔNG có ※ → Required="-" (không suy diễn).
    - Mô tả hành vi hệ thống (VD "trạng thái tự chuyển...") → đưa vào mục 4 Screen Actions,
      KHÔNG tạo field input mới cho nó.

2b. Comment Figma — Lọc dòng cho SLC0104:

    B2.1: Mở file Comment Figma, sheet "Comment Figma".
    Cột B/C là merged cell → forward-fill (lấy giá trị dòng đầu vùng merge) để xác định
    Screen ID và sub-state cho TỪNG dòng. KHÔNG bỏ qua dòng có B/C rỗng.

    B2.2: Lọc dòng có Screen ID (đã forward-fill) = "SLC0104".
    Nếu không có dòng nào, hoặc tất cả dòng đều rỗng cả 4 cột D/E/F/G → KẾT LUẬN:
    "Chưa có Comment Figma cho SLC0104" — ghi vào sheet, KHÔNG bịa nội dung.

    B2.3: Với mỗi dòng có dữ liệu thật:
    - Cột D (Field comment): "-" = ghi chú chung, KHÔNG gán cho 1 field cụ thể.
    - Cột F (Comment_VN): dùng TRỰC TIẾP, KHÔNG tự dịch lại từ cột E.
    - Cột G (Image): xác định sub-state (作成前 vs 作成後).
    - Phân loại dòng: (a) field detail, (b) validation/điều kiện kích hoạt,
      (c) hành vi hệ thống tự động, (d) business rule, (e) logic phụ thuộc tab/màn hình.
      Không rõ nhóm → ghi nguyên văn vào Remarks kèm "chưa phân loại rõ".
    - Ghi kèm "Theo Comment Figma No.X" khi trích dẫn.

────────────────────────────────────────
BƯỚC 3 — PHẦN C: TỔNG HỢP, ĐỐI CHIẾU, BỔ SUNG
────────────────────────────────────────

⚠ CẤU TRÚC SHEET THEO NC6:
  - Main screen CHỈ có: (1) Overview + (2) Layout (kèm ảnh tất cả state).
  - KHÔNG có mục 3/4 ở main — toàn bộ Input/Output + Actions nằm TRONG từng sub-screen.
  - Nếu sheet hiện tại đang có mục 3/4 ở main (dạng "union tất cả state"):
    → DI CHUYỂN nội dung vào đúng sub-screen tương ứng, rồi XOÁ mục 3/4 khỏi main.

3a. ĐỐI CHIẾU — Main screen:
    Mục 1 (Overview): business rule từ BƯỚC 2 chưa nhắc → đánh dấu bổ sung.
    Mục 2 (Layout): kiểm tra đã có đủ ảnh cho mọi state, mô tả layout tổng thể.

3b. ĐỐI CHIẾU — Từng sub-screen (mục 5):
    Với MỖI sub-screen, đối chiếu field/action từ BƯỚC 1 (ảnh UI của state đó) và
    BƯỚC 2 (Feature List + Comment Figma) với bảng (3)/(4) hiện có trong block:
    - Field từ ảnh UI chưa có dòng → đánh dấu thiếu, ghi nguồn.
    - Action chưa có → đánh dấu thiếu.
    - Required/Validation Rule sai/thiếu → đánh dấu cần sửa.

3c. KIỂM TRA NGƯỢC — chống field bịa:
    Rà MỌI dòng ĐANG CÓ trong bảng (3)/(4) của TỪNG sub-screen.
    Mỗi dòng phải có ít nhất 1 bằng chứng (a)/(b)/(c) theo NC1.
    Không có bằng chứng nào → ĐÂY LÀ FIELD BỊA → xoá hẳn.
    Nghi ngờ nhưng có khả năng đúng (ảnh mờ/khó thấy) → giữ, ghi chú.

3d. BỔ SUNG / SỬA vào sheet:

    ◆ XOÁ field bịa: xoá dòng + QUÉT TOÀN BỘ sheet tìm mọi tham chiếu còn sót
      → xoá/sửa hết. Renumber "No".

    ◆ THÊM field thiếu vào ĐÚNG sub-screen tương ứng: chèn đúng vị trí, copy style.
      Renumber "No". Ghi rõ nguồn trong Remarks theo NC9.

    ◆ SỬA Required/Validation Rule: chỉ ghi Required="Có" khi đã trích được "tên※"
      nguyên văn từ Feature List. Không trích được → Required="-".
      Giá trị hệ thống → I/O="Output", Required="-".

    ◆ CHUẨN HOÁ Error Message (NC7): quét toàn bộ cột Error Message trong MỌI sub-screen.
      Required="Có" → set 「必須項目を入力してください。」
      Ngoại lệ (lỗi format/trùng có bằng chứng riêng) → giữ nguyên.
      In ra: đã chuẩn hoá bao nhiêu dòng.

    ◆ XÂY DỰNG / SỬA SUB-SCREEN (NC6): với MỖI sub-screen kiểm tra:

      (1) Overview: có mô tả context riêng state này chưa.

      (2) Layout: PHẢI có ẢNH CHÈN TRỰC TIẾP (openpyxl add_image) ngay dưới dòng (2).
          Nguồn ảnh: file ảnh tương ứng state trong thư mục image-screen/
          (hoặc copy từ image đã chèn ở mục 2 nếu cùng ảnh).
          KHÔNG chấp nhận chỉ viết text "参照画像: mục2 ①..." — phải INSERT ảnh thật.
          Không tìm thấy ảnh → ghi "⚠ chưa có ảnh — cần bổ sung", KHÔNG bịa layout.

      (3) Input/Output: PHẢI là BẢNG đầy đủ cột — KHÔNG chấp nhận kiểu 1 dòng tóm tắt
          + "※mục3 No.X参照". Mỗi field = 1 dòng riêng với đầy đủ tất cả cột.

      (4) Actions: PHẢI là BẢNG đầy đủ cột — KHÔNG chấp nhận 1 câu mô tả chung.

      Nếu hiện tại sub-screen chỉ có dạng tóm tắt + tham chiếu:
      → PHẢI viết lại thành bảng đầy đủ, dựa trên ảnh UI + Feature List + Comment Figma
        CỦA RIÊNG state đó.
      In ra: đã xây dựng đầy đủ cho bao nhiêu sub-screen.

    ◆ Ô không xác định giá trị (NC8): ghi "-".

    ◆ Dòng mới giữ đúng style (font, border, độ rộng cột) như dòng xung quanh.

────────────────────────────────────────
BƯỚC 4 — RÀ SOÁT CUỐI (BẮT BUỘC, KHÔNG BỎ QUA)
────────────────────────────────────────

4a. BẢNG TỔNG KẾT:
    In ra: field/action đã thêm (kèm nguồn), dòng đã sửa Required/Validation Rule,
    field đã xoá (vì bịa).

4b. VERIFY KHÔNG GỘP (NC3):
    Với MỖI sub-screen: đếm số ô input trên ảnh UI của state đó (từ BƯỚC 1c).
    So sánh với số dòng input trong bảng (3) của sub-screen tương ứng.
    Không khớp → tìm nhóm field bị gộp, tách ra đủ dòng.
    In: "Sub-screen X: ảnh=N ô, bảng=M dòng — [Khớp / Đã xử lý]"

4c. VERIFY REQUIRED (NC5):
    Với MỌI field có Required="Có" + nguồn "Theo Feature List" (trong MỌI sub-screen):
    đọc lại dòng Feature List, xác nhận có dấu ※ gắn trực tiếp vào tên field trong cột G.
    Không có ※ → sửa Required="-", xoá nguồn Feature List khỏi Remarks.
    In danh sách field đã sửa lại (kỳ vọng = rỗng).

4d. VERIFY ERROR MESSAGE (NC7):
    Đếm field Required="Có" có Error Message ≠ 「必須項目を入力してください。」
    trong MỌI sub-screen, mà KHÔNG thuộc ngoại lệ → kỳ vọng = 0. Còn sót → sửa ngay.

4e. VERIFY SUB-SCREEN (NC6):
    Mỗi sub-screen trong mục 5: xác nhận:
    ✓ Có đủ 4 mục con (Overview / Layout / Input-Output / Actions).
    ✓ Mục (2) Layout có ẢNH CHÈN TRỰC TIẾP (ws._images có image anchor nằm trong vùng row
      của block sub-screen này) — KHÔNG chấp nhận chỉ có text "参照画像: mục2 ①...".
    ✓ Mục (3) Input/Output là BẢNG đầy đủ cột — KHÔNG phải 1 dòng text tóm tắt.
    ✓ Mục (4) Actions là BẢNG đầy đủ cột — KHÔNG phải 1 câu mô tả chung.
    Chưa đạt → liệt kê kèm lý do + bổ sung ngay nếu có đủ dữ liệu nguồn.
    In: "Sub-screen X: [Đạt / Chưa đạt — lý do]" cho từng state.

4f. VERIFY MAIN SCREEN KHÔNG CÒN MỤC 3/4:
    Xác nhận main screen CHỈ có (1) Overview + (2) Layout.
    Nếu vẫn còn mục 3/4 dạng "union" → đã di chuyển hết vào sub-screen chưa?
    In: "Main screen: [Chỉ có mục 1+2 / Còn sót mục 3/4 — cần xử lý]"

4g. VERIFY QUÉT SẠCH SAU XOÁ:
    Với mỗi field/button đã xoá: search tên trong toàn sheet.
    In: "Đã search '<tên>' — còn 0 chỗ sót" (phải = 0 trước khi hoàn tất).

4h. VERIFY NGƯỢC TOÀN BỘ LẦN CUỐI:
    Rà lại MỌI dòng trong bảng (3)/(4) của MỌI sub-screen → áp dụng NC1 (3 bằng chứng).
    Phát hiện thêm field bịa → xoá + quét sạch y hệt BƯỚC 3d.