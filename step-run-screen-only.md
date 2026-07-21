╔══════════════════════════════════════════════════════════════════════════════╗
║  PROMPT HOÀN CHỈNH — CHẠY CHO ĐÚNG 1 MÀN HÌNH                                   ║
║  Thay SLC0701 (VD SLC0104) và Screen_SLC0701 システムログ参照 (VD "Screen_SLC0104      ║
║  重複チェック") ở mọi nơi trước khi chạy.                                        ║
║                                                                                ║
║  Prompt gồm 3 GIAI ĐOẠN TUẦN TỰ — KHÔNG đảo thứ tự:                             ║
║    GIAI ĐOẠN I  — DỰNG / HOÀN THIỆN SHEET (cấu trúc 4 mục + sub-screen + ảnh)   ║
║    GIAI ĐOẠN II — ĐỐI CHIẾU & BỔ SUNG NỘI DUNG (NC1–NC9, chống bịa/gộp)         ║
║    GIAI ĐOẠN III— DỊCH SANG TIẾNG VIỆT (giữ nhãn Display Item Name tiếng Nhật)  ║
║                                                                                ║
║  ⚠ Việc DỊCH luôn để CUỐI CÙNG. Giai đoạn I & II làm việc trên nội dung gốc     ║
║    (tiếng Nhật) vì phải cite nguyên văn Function List / Comment Figma.           ║
╚══════════════════════════════════════════════════════════════════════════════╝


═══════════════════════════════════════════════════════════════════════════════
GIAI ĐOẠN I — DỰNG / HOÀN THIỆN SHEET CHO SLC0701
═══════════════════════════════════════════════════════════════════════════════

Nhiệm vụ: TẠO MỚI 1 file output xlsx RIÊNG cho ĐÚNG 1 màn hình có Screen ID = SLC0701, file
này CHỈ CHỨA 1 sheet DUY NHẤT là sheet của màn hình đang chạy (KHÔNG chứa "Screen List",
KHÔNG chứa "Screen Transition Diagram", KHÔNG chứa bất kỳ màn hình nào khác). Mỗi lần chạy 1
màn hình = 1 file output riêng.

⚠ QUY TẮC TÊN FILE OUTPUT (BẮT BUỘC — dùng thống nhất cho toàn bộ prompt):
  [Lottery Campaign ] Screen Definition_{Sheet_Name}_Ver1.1.xlsx
  trong đó {Sheet_Name} = ĐÚNG tên sheet của màn hình = "Screen_<ID> <Screen Name_JP>".
  VD màn hình Screen_SLC0701 システムログ参照 → tên sheet = "Screen_SLC0701 システムログ参照"
  → tên file = "[Lottery Campaign ] Screen Definition_Screen_SLC0701 システムログ参照_Ver1.1.xlsx".
  (VD khác: Screen_SLC0102 応募データフォーマット → "[Lottery Campaign ] Screen Definition_
  Screen_SLC0102 応募データフォーマット_Ver1.1.xlsx".)
  File được lưu trong thư mục output/ (xem B.1). Giữ dấu cách sau chữ "Campaign" đúng như mẫu.

CÁCH DỰNG: tạo workbook mới, thêm 1 sheet có tên = {Sheet_Name} rồi hoàn thiện sheet đó theo
cấu trúc chuẩn dưới đây. Nếu file output cùng tên đã tồn tại (chạy lại màn hình này) → MỞ và
hoàn thiện chính file đó, KHÔNG tạo file trùng, KHÔNG tạo sheet trùng.
⚠ Tên sheet Excel giới hạn 31 ký tự: nếu "Screen_<ID> <Screen Name_JP>" vượt 31 ký tự thì
  RÚT GỌN TÊN SHEET cho ≤31 ký tự (ưu tiên giữ "Screen_<ID>"), nhưng TÊN FILE vẫn dùng chuỗi
  {Sheet_Name} đầy đủ như trên.

──────────────────────────────────────────────
I.-1 — Xác định nguồn sub-screen cho SLC0701
──────────────────────────────────────────────
NGUỒN CHÍNH: sheet "Final_Screen List" trong file
  inputs/screen-detail/screen-list/Screen_List.xlsx
Cột: A=ページ内容 (tên màn hình + cấp bậc — dòng con thụt đầu bằng ký tự　U+3000), B=ID
(Screen ID, VD SLC0102; dòng state con để B trống/None), C=Title, D=パンクズ (breadcrumb),
E=URL, F=備考, G=Figma mapping (tên các state/ảnh của màn hình — mỗi dòng 1 state, ngăn bởi
xuống dòng), H=Sub function (Figma mapping) (các sub-screen/state con — mỗi dòng 1 sub).

CÁCH XÁC ĐỊNH SUB-SCREEN cho SLC0701 (đọc động từ file, KHÔNG hardcode):
1. Tìm dòng có cột B = SLC0701. Lấy Title (C), URL (E), breadcrumb (D), 備考 (F).
2. State/sub-screen = hợp của:
   • Các dòng trong cột G (Figma mapping) của chính dòng đó — mỗi dòng là 1 state.
   • Các dòng trong cột H (Sub function) của dòng đó VÀ các dòng NGAY DƯỚI có cột B trống
     (None) cho tới trước Screen ID kế tiếp — mỗi dòng H là 1 sub-screen.
3. Đặt tên ảnh state theo đúng chuỗi trong G/H (VD "#2_キャンペーン設定_重複チェックキャンペーン
   追加前") để MAP tới file ảnh trong inputs/screen-detail/image-screen/.
4. Gán Screen ID hiển thị cho từng sub-screen dạng "SLC0701.<số thứ tự>" theo đúng
   thứ tự xuất hiện trong G rồi H (VD 3 state của SLC0104 → SLC0104.1/.2/.3).

BẢNG THAM CHIẾU NHANH (chốt từ Final_Screen List — VẪN đối chiếu lại file khi chạy, ưu tiên
dữ liệu file nếu có sai lệch):

  | SLC0701 | Title / màn hình | State & sub-screen (theo cột G / H) |
  |---|---|---|
  | T-03 (ID="-") | ログイン | 1 màn (GMOトラストログイン); không có state con |
  | SLC0101 | 基本設定 (キャンペーン設定) | 2 state: 作成前, 作成後 |
  | SLC0102 | 応募データフォーマット | 1 state; không có con |
  | SLC0103 | 抽選枠設定 | 2 state: 抽選枠追加前, 抽選枠追加後 |
  | SLC0104 | 重複チェック | 3 state: キャンペーン追加前, キャンペーン追加後, 同一応募者チェックを外した場合 |
  | SLC0105 | 適格条件 | 6 state: 追加前, 追加後, 選択, 条件グループ追加後, 条件グループ追加後条件選択, 条件入力例 |
  | SLC0201 | 基本設定 (抽選枠設定) | 1 state; không có con |
  | SLC0202 | 口数設定 | 3 state: 口数設定, 口数設定チェック後, 口数設定条件追加後 |
  | SLC0203 | 等数設定 | 3 state: 等数設定, 等数設定チェック後, 等数設定等数入力後 |
  | SLC0204 | 抽選枠判定条件 | 3 state: 抽選枠判定条件, 抽選枠判定条件チェック後, 抽選枠判定条件条件追加後 |
  | SLC0205 | 適格条件 (抽選枠設定) | 1 state; không có con |
  | SLC0206 | 倍率設定 | 3 state: 倍率設定, 倍率設定チェック後, 倍率設定条件入力後 |
  | SLC0301 | キャンペーン一覧 | sub: 絞り込みOPEN |
  | SLC0401 | 抽選枠一覧 | sub: 応募取り込み, 応募取り込み中, 応募取り込み後 |
  | SLC0501 | 応募一覧 | sub: 選択中, 適格チェック中, 適格チェック後, 適格チェック後絞り込みモーダル, 適格チェック後絞り込みOPEN |
  | SLC0601 | 応募詳細 | sub: レシート情報, 応募情報, 画像拡大モーダル, 画像にレシートが複数枚の場合 |
  | SLC0701 | システムログ参照 | 備考 G="※未作成" → chưa có ảnh; chỉ Overview + "⚠ chưa có ảnh/breakdown" |

⚠ Bảng trên là ảnh chụp tại thời điểm soạn prompt. Khi chạy, LUÔN đọc lại Final_Screen List
để lấy danh sách state/sub mới nhất (cột G/H có thể được bổ sung). Nếu file khác bảng → theo
file. Với màn hình có 備考/G = "※未作成" hoặc trống → đánh dấu "⚠ chưa có ảnh", KHÔNG bịa state.

──────────────────────────────────────────────
I.0 — Kích hoạt skill (ADF Phase ② Design)
──────────────────────────────────────────────
Agent: `ui-ux-designer`
- `ui-ux-pro-max`  — phân tích ảnh trong inputs/screen-detail/image-screen/ khớp với
  SLC0701 và sub-screen của nó (theo mapping I.-1); trích component/state/hành vi,
  xác định path ảnh để CHÈN ẢNH THẬT.
- `design-system`  — chuẩn hoá "Type" component theo taxonomy sheet "Settings" của file
  inputs/translated_【基本設計書】....xlsx; PHẢI nhất quán với các màn hình đã tạo trước đó
  (đọc lại các file output per-screen khác trong thư mục output/ nếu có — mỗi file 1 màn hình).
- `web-design-guidelines` — checklist thuật ngữ UX pattern cho mục Layout.
- (Tuỳ chọn) `design-mockup-create` nếu cần bản visual layout riêng ngoài ảnh chèn thật.

──────────────────────────────────────────────
I.1 — Đọc format chuẩn
──────────────────────────────────────────────
Đọc sheet "Screen Name" của file inputs/translated_【基本設計書】....xlsx để lấy đúng cấu trúc
4 mục + Supplement, style/font/độ rộng cột.

──────────────────────────────────────────────
I.2 — Dựng nội dung, tiêu đề đầu sheet = "SLC0701 <Screen Name>"
──────────────────────────────────────────────
(Ở GIAI ĐOẠN I nội dung viết bằng tiếng Nhật/gốc — dịch để dành GIAI ĐOẠN III.)

  1. Screen Overview Description — Overview / Display Conditions / Initial Display Behavior.

  2. Screen Layout — mô tả bố cục bám sát ảnh thật. BẮT BUỘC chèn ảnh thật bằng openpyxl
     (`from openpyxl.drawing.image import Image as XLImage`), resize giữ tỷ lệ (~500-600px
     chiều rộng), tăng row height đủ chỗ TRƯỚC khi chèn để không đè nội dung mục 3/4.
     Không có ảnh → để "⚠ Chưa có ảnh tham chiếu", KHÔNG chèn placeholder giả.

  3. Detailed Screen Input/Output Item List —
     No | Display Item Name | Type | Required | I/O | Data Type | Max Length |
     Default Value | Validation Rule | Error Message | Remarks.

  4. Screen Actions (Detailed Processing Flow) —
     No | Action Name | Event | Input Information | Output Information/Destination |
     Processing Details (Step-by-Step) | Error Handling.

  5. Sub Screens (画面内訳) — theo cây map ở I.-1, mỗi sub-screen 1 block (đủ 4 mục trên,
     chỉ mô tả PHẦN THAY ĐỔI nếu là state/modal khác của cha), CHÈN ẢNH THẬT riêng cho từng
     sub-screen có ảnh; không có ảnh → đánh dấu "⚠", KHÔNG chèn ảnh giả.

  ⚠ Lưu ý cấu trúc main vs sub-screen: xem NC6 ở GIAI ĐOẠN II — nếu SLC0701 có
    nhiều state, MAIN chỉ giữ mục (1)+(2); toàn bộ Input/Output + Actions nằm trong từng
    sub-screen. Áp dụng NC6 khi hoàn thiện.

──────────────────────────────────────────────
I.3 — Rà soát dựng sheet
──────────────────────────────────────────────
Không ô trống không giải thích (phải "TBD"/"⚠"); không bịa validation rule/API nếu không có
căn cứ; đếm số ảnh đã chèn khớp số Screen ID có ảnh; không ảnh nào đè lên nội dung/block kế
tiếp; in tổng kết cover được bao nhiêu sub-screen, còn thiếu gì.


═══════════════════════════════════════════════════════════════════════════════
GIAI ĐOẠN II — ĐỐI CHIẾU & BỔ SUNG NỘI DUNG (NC1–NC9) cho SLC0701
═══════════════════════════════════════════════════════════════════════════════

Nhiệm vụ: ĐỐI CHIẾU và BỔ SUNG (KHÔNG tạo sheet mới) cho sheet Screen_SLC0701 システムログ参照 — nguồn chính là
ẢNH UI, bổ sung bằng Function List + Comment Figma. Ở giai đoạn này giữ nguyên tiếng Nhật khi
cite.

───────────────────────────────────────────────────────────────
A. NGUYÊN TẮC CỐT LÕI (đọc hết trước khi làm bất kỳ bước nào)
───────────────────────────────────────────────────────────────

【NC0 — QUY TẮC COMMON (áp dụng cho MỌI màn hình, MỌI sub-screen)】
Đây là 7 chuẩn hành vi UI/UX toàn cục. Chúng LÀ ngoại lệ hợp lệ của NC1: được coi như đã có
"bằng chứng chuẩn dự án", KHÔNG cần trích ảnh/Function List/Comment Figma. Khi áp dụng, ghi
nguồn trong Remarks/Error Handling là "Theo quy tắc common NC0.<số>".
⚠ Chỉ áp dụng khi màn hình THỰC SỰ có thành phần tương ứng (VD chỉ áp NC0.7 khi màn hình có
nút Xóa; NC0.1 khi có nút Lưu + trường bắt buộc). KHÔNG bịa ra nút/tab/thao tác không tồn tại
chỉ để gắn quy tắc. Nếu ảnh/nguồn cho thấy màn hình có hành vi KHÁC chuẩn common → ưu tiên
nguồn thực tế và ghi chú rõ điểm khác biệt.

  NC0.1 — Điều kiện kích hoạt nút Lưu: nút [Lưu/Save] mặc định `disabled`; chỉ chuyển
    `enabled` khi TẤT CẢ trường bắt buộc (required) đã điền đủ. → Ghi vào mục 4 Actions (Event
    của nút Lưu) và/hoặc Remarks của nút Lưu.
  NC0.2 — Kiểm soát định dạng nhập liệu: chặn nhập trực tiếp (hard-block) ngay khi sai định
    dạng (VD trường chỉ cho chữ Alphabet/Text-only → bỏ qua/không nhận phím số). → Ghi vào
    Validation Rule của trường tương ứng.
  NC0.3 — Cảnh báo mất dữ liệu khi chuyển tab: nếu dữ liệu đã đổi (dirty) mà chưa [Lưu] và
    người dùng chuyển tab → hiện Confirmation Dialog/Browser Alert.
    Nội dung: 「入力した情報はまだ保存されていません。この画面を閉じてもよろしいでしょうか。」
    (VN: "Thông tin đã nhập chưa được lưu. Bạn có chắc chắn muốn đóng màn hình này không?").
    → Ghi vào mục 4 Actions (Error Handling / Processing Details).
  NC0.4 — Thông báo lỗi bắt buộc dùng chung 1 message: 「必須項目を入力してください。」
    (VN: "Vui lòng nhập các mục bắt buộc.") cho MỌI trường required. Trùng & thay thế NC7.
  NC0.5 — Cơ chế hiển thị lỗi (2 dạng):
    • Inline Message (lỗi validate: sai định dạng / thiếu required) → text đỏ ngay dưới trường
      (input-level).
    • Toast Message (lỗi hệ thống/API sau khi click: 4xx/5xx, lỗi logic backend) → thông báo
      nổi góc trên bên phải.
    → Ghi vào Error Handling của Actions và/hoặc Error Message của trường.
  NC0.6 — Tải lại trang: khi click các button chỉ định [tên button cụ thể của màn hình], hệ
    thống Hard Reload (window.location reload) để cập nhật dữ liệu mới nhất. → Ghi vào
    Processing Details của action tương ứng (chỉ khi màn hình có button như vậy).
  NC0.7 — Xác nhận thao tác xóa: khi click [Xóa], KHÔNG xóa trực tiếp mà hiện Popup
    Confirmation. Nội dung: 「削除してもよろしいでしょうか。」 (VN: "Bạn có chắc chắn muốn
    xóa không?"). → Ghi vào mục 4 Actions (Error Handling / Processing Details của nút Xóa).

⚠ Ở GIAI ĐOẠN II giữ nguyên chuỗi tiếng Nhật của NC0.3/NC0.4/NC0.7; GIAI ĐOẠN III sẽ dịch
  sang tiếng Việt theo D4 (xem quy tắc dịch message ở GIAI ĐOẠN III).

【NC1 — KHÔNG SUY DIỄN】
Mọi field/button/action/business rule đưa vào sheet PHẢI có ít nhất 1 trong 3 bằng chứng:
  (a) Nhìn thấy trực tiếp trong ảnh UI — mô tả được vị trí/hình dạng/text.
  (b) Trích dẫn nguyên văn từ Function List (cột G) — ghi rõ Function List No.
  (c) Trích dẫn nguyên văn từ Comment Figma (cột E/F) — ghi rõ Comment Figma No.
Chỉ cần 1 trong 3 là đủ. Bằng chứng (a) một mình đã đủ mạnh, không cần (b)/(c) bổ trợ.
NGOẠI LỆ: 7 quy tắc common NC0 được áp dụng như bằng chứng chuẩn dự án (không cần a/b/c),
nhưng CHỈ khi màn hình thực sự có thành phần tương ứng — không được dùng NC0 để bịa
nút/tab/field không có trên màn hình.
KHÔNG có bằng chứng nào (và không thuộc NC0) → KHÔNG đưa vào. Ghi "-" thay vì đoán.
CẤM suy diễn theo "pattern UI phổ biến" / "form thường có nút X" / "theo thông lệ thiết kế".
Áp dụng cho MỌI nơi trong sheet: bảng mục 3/4, text tự do mục 1/2, block sub-screen mục 5.

【NC2 — THỨ TỰ ƯU TIÊN NGUỒN】
(1) Ảnh UI gốc = NGUỒN CHÍNH. Field nhìn thấy trên ảnh PHẢI vào sheet, kể cả khi Feature
    List / Comment Figma không nhắc.
(2) Function List + Comment Figma = BỔ SUNG (Required, Validation Rule, logic ẩn). Không được
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
Chỉ ghi Required="Có" khi Function List cột G có dấu ※ gắn TRỰC TIẾP vào tên field đó
(VD "CPID※"). Phải trích nguyên văn cụm từ có ※ trước khi gán.
Giá trị hệ thống tự tính (status, số tự sinh, kết quả tính toán) → I/O="Output",
Required="-", Validation Rule = mô tả logic tự tính.

【NC6 — CẤU TRÚC MAIN SCREEN + SUB-SCREEN】
Nếu Screen ID có nhiều state (VD 6 state của SLC0104, 2 state 作成前/作成後 của SLC0101...):

▸ MAIN SCREEN chỉ giữ 2 mục (tránh trùng lặp với sub-screen):
  (1) Screen Overview — mô tả tổng quan chung cho toàn bộ Screen ID (context, mục đích,
      URL, display conditions, initial behavior, business rules chung).
  (2) Screen Layout — mô tả layout tổng thể + CHÈN ẢNH UI của TẤT CẢ state (mỗi state 1 ảnh
      kèm label, người đọc thấy toàn cảnh các state).
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
      Liệt kê CHỈ các field THUỘC RIÊNG state này. Mỗi field = 1 dòng riêng đủ tất cả cột.
  (4) Screen Actions — BẢNG ĐẦY ĐỦ CÁC CỘT giống hệt cấu trúc bảng chuẩn:
      No | Action Name | Event | Input Information | Output/Destination |
      Processing Details | Error Handling
      Liệt kê CHỈ các action THUỘC RIÊNG state này.
  Breadcrumb, button đặc thù từng state phải nằm đúng block tương ứng.
  ⚠ TUYỆT ĐỐI KHÔNG viết kiểu tóm tắt 1 dòng như:
     "(3) Input/Output: 条件を選択(Dropdown)、この条件を削除(Link)。※mục3 No.4,21参照。"
  PHẢI viết thành BẢNG có đầy đủ cột, mỗi field 1 dòng riêng.

【NC7 — ERROR MESSAGE CHUẨN HOÁ】 (chi tiết hoá của NC0.4)
Mọi field Required="Có" dùng CHUNG: 「必須項目を入力してください。」 (theo NC0.4).
Ngoại lệ: ảnh UI/Comment Figma hiển thị rõ message khác (lỗi format, trùng lặp) → giữ riêng.
Cơ chế hiển thị lỗi tuân theo NC0.5 (Inline cho lỗi validate, Toast cho lỗi hệ thống/API).
(Ở GIAI ĐOẠN II giữ nguyên chuỗi Nhật này để chuẩn hoá nhất quán; GIAI ĐOẠN III sẽ dịch toàn
bộ Error Message sang tiếng Việt theo D4 — chuỗi chuẩn → "Vui lòng nhập các mục bắt buộc.")

【NC8 — GIÁ TRỊ MẶC ĐỊNH CHO Ô KHÔNG XÁC ĐỊNH】
Khi không có đủ thông tin cho 1 cột (Required, Validation Rule, Error Message, Remarks...)
và không trích dẫn được nguồn → ghi "-" (KHÔNG ghi "TBD - cần xác nhận", KHÔNG tự đoán).

【NC9 — REMARKS PHẢI CÓ NỘI DUNG THẬT, KHÔNG GHI SỐ SUÔNG】
Cột Remarks (và Error Handling) PHẢI ghi NỘI DUNG CỤ THỂ, không chỉ ghi số tham chiếu.
  ❌ SAI: "Comment Figma No.19,29。" / "画像/Comment Figma。" / "- (Comment Figma No.16)"
  ✅ ĐÚNG:
     "Theo Comment Figma No.19: 条件を選択すると、それに合わせた入力欄が表示される"
     "Theo Comment Figma No.17: 1つ目は AND/OR を表示しない"
     "Quan sát từ ảnh UI (state 適格条件選択): date picker hiển thị 以降/以前"
  Quy tắc:
  - Cite Comment Figma → "Theo Comment Figma No.X: [nguyên văn cột F Comment_VN nếu có; nếu
    F trống thì dịch cột E Comment_JP sang tiếng Việt; cả hai trống thì không cite]".
  - Cite Function List → "Theo Function List No.X: [nguyên văn cụm liên quan từ cột G]".
  - Cite ảnh UI → "Quan sát từ ảnh UI (state/ảnh nào): [mô tả ngắn bằng chứng]".
  - Không có nội dung đáng ghi → để "-". KHÔNG ghi số tham chiếu trống rỗng.

───────────────────────────────────────────────────────────────
B. INPUT FILES (path cố định)
───────────────────────────────────────────────────────────────
1. Output đang sửa = FILE PER-SCREEN do GIAI ĐOẠN I tạo cho ĐÚNG màn hình này (chỉ 1 sheet):
   /home/sotatek/DucNguyen/ADF_Lottery_Campaign/output/[Lottery Campaign ] Screen Definition_{Sheet_Name}_Ver1.1.xlsx
   VD: /home/sotatek/DucNguyen/ADF_Lottery_Campaign/output/[Lottery Campaign ] Screen Definition_Screen_SLC0701 システムログ参照_Ver1.1.xlsx
   ⚠ KHÔNG mở/sửa file output của màn hình khác. Toàn bộ GIAI ĐOẠN II & III chỉ thao tác trên
   đúng file per-screen này (chứa duy nhất sheet của màn hình đang chạy).
2. Ảnh UI gốc (thư mục):
   /home/sotatek/DucNguyen/ADF_Lottery_Campaign/inputs/screen-detail/image-screen
3. Function List (danh sách tính năng — ĐÃ dịch sẵn tiếng Việt đầy đủ):
   /home/sotatek/DucNguyen/ADF_Lottery_Campaign/inputs/requirement/business-requirement/Function_List_v1.1.xlsx
   Sheet: "Danh sách tính năng" (CHỈ dùng sheet này)
   Cột: A=# (No), B=Hệ thống con, C=Phân loại lớn, D=Phân loại trung, E=Phân loại nhỏ,
   F=Chi tiết tính năng, G=Tổng quan tính năng, H=Tài liệu tham khảo, I=Điều chỉnh phạm vi.
   ⚠ File đã ở tiếng Việt → khi cite lấy NGUYÊN VĂN tiếng Việt từ cột G, KHÔNG cần dịch lại.
   ⚠ Dòng "NGOÀI PHẠM VI": dòng có cột I = "Ngoài phạm vi" (và được BÔI XÁM nền FFD9D9D9)
   → BỎ QUA HOÀN TOÀN, không lấy field/action/rule từ dòng đó. Phát hiện bằng 1 trong 2:
   (a) text cột I chứa "Ngoài phạm vi", hoặc (b) fill.fgColor.rgb == "FFD9D9D9" ở cột G/I.
4. Comment Figma:
   /home/sotatek/DucNguyen/ADF_Lottery_Campaign/inputs/screen-detail/spec-note/List_Comment_Figma_Ver1.1.xlsx
   Sheet: "Comment Figma"
   Cột: A=No, B=ID Màn hình (merged cell), C=Tên màn hình_JP (merged cell),
   D=Field comment, E=Comment_JP, F=Comment_VN, G=Image (ảnh ở
   inputs/screen-detail/image-note/, KHÁC thư mục ảnh UI), H=Note.
   ⚠ Quy tắc dùng comment: nếu cột F (Comment_VN) CÓ nội dung → dùng TRỰC TIẾP, KHÔNG tự dịch
   lại. Nếu F TRỐNG nhưng cột E (Comment_JP) CÓ → tự DỊCH E sang tiếng Việt rồi dùng trực
   tiếp. Nếu cả E và F đều trống → BỎ QUA dòng đó (không có comment).

───────────────────────────────────────────────────────────────
C. CÁC BƯỚC THỰC HIỆN (tuần tự, KHÔNG bỏ bước)
───────────────────────────────────────────────────────────────

── BƯỚC 0 — KIỂM TRA FILE TỒN TẠI ──
```python
import os
OUTPUT_DIR = r"/home/sotatek/DucNguyen/ADF_Lottery_Campaign/output"
SHEET_NAME = r"Screen_SLC0701 システムログ参照"   # đổi theo màn hình đang chạy
OUTPUT_FILE = os.path.join(OUTPUT_DIR, f"[Lottery Campaign ] Screen Definition_{SHEET_NAME}_Ver1.1.xlsx")

# Output per-screen do GIAI ĐOẠN I tạo phải tồn tại trước khi vào GIAI ĐOẠN II.
files_to_check = {
    "Output per-screen (Giai đoạn I tạo)": OUTPUT_FILE,
    "Ảnh UI (thư mục)": r"/home/sotatek/DucNguyen/ADF_Lottery_Campaign/inputs/screen-detail/image-screen",
    "Screen List": r"/home/sotatek/DucNguyen/ADF_Lottery_Campaign/inputs/screen-detail/screen-list/Screen_List.xlsx",
    "Function List": r"/home/sotatek/DucNguyen/ADF_Lottery_Campaign/inputs/requirement/business-requirement/Function_List_v1.1.xlsx",
    "Comment Figma": r"/home/sotatek/DucNguyen/ADF_Lottery_Campaign/inputs/screen-detail/spec-note/List_Comment_Figma_Ver1.1.xlsx",
}
missing = [name for name, path in files_to_check.items() if not os.path.exists(path)]
if missing:
    raise SystemExit(f"DỪNG — không tìm thấy: {missing}. Báo người dùng, KHÔNG tiếp tục.")
print(f"✓ Đủ file/thư mục — output per-screen: {os.path.basename(OUTPUT_FILE)} — tiếp tục BƯỚC 1.")
```
⚠ THỐNG NHẤT PATH: dùng đúng 1 path output ở mục B.1 cho toàn bộ prompt (không dùng lẫn tên
file khác). Nếu thiếu file: DỪNG NGAY, báo người dùng. KHÔNG chạy tiếp với dữ liệu thiếu.

── BƯỚC 1 — PHẦN A: PHÂN TÍCH ẢNH UI GỐC ──
1a. Tìm ảnh UI cho SLC0701: đọc ws._images trong sheet hiện tại; nếu không có →
    tìm file ảnh trong inputs/screen-detail/image-screen/ theo tên Screen Name (mapping I.-1).
1b. Phân tích TỪ ĐẦU (không neo theo bảng cũ): liệt kê MỌI component nhìn thấy (label, input,
    button, dropdown, checkbox, radio, table + từng cột, breadcrumb, tab, icon action,
    thông báo...). Mỗi component ghi bằng chứng ngắn (VD "nút xanh góc dưới phải, text '保存'").
    Không mô tả được bằng chứng → KHÔNG liệt kê.
1c. Áp dụng NC3 (không gộp): mỗi ô input/output = 1 dòng, tên = label chính xác; bảng/danh
    sách lặp liệt kê từng dòng thật; ĐẾM tổng số ô input trên ảnh (dùng verify BƯỚC 4).

── BƯỚC 2 — PHẦN B: ĐỐI CHIẾU FUNCTION LIST + COMMENT FIGMA ──
2a. Function List — lọc dòng liên quan SLC0701 (cột D/E/F khớp ngữ nghĩa Screen
    Name). File đã ở tiếng Việt → dùng nguyên văn tiếng Việt, KHÔNG dịch lại. Đọc cột I
    (Điều chỉnh phạm vi):
    • Trống → dùng toàn bộ cột G.
    • "Ngoài phạm vi" (dòng bôi xám nền FFD9D9D9) → BỎ QUA HOÀN TOÀN (không lấy gì từ dòng).
    • "Điều chỉnh một phần phạm vi (...)" → chỉ bỏ phần trong ngoặc; không chắc → ghi "-".
    • "※Bổ sung ..." → dùng bình thường.
    Trích từ cột G: field có ※ → Required="Có" (trích nguyên văn "tên_field※"); field không
    ※ → Required="-"; mô tả hành vi hệ thống → đưa vào mục 4 Actions, KHÔNG tạo field input.
2b. Comment Figma — lọc dòng cho SLC0701:
    B2.1: Mở sheet "Comment Figma". Cột B/C merged → forward-fill để xác định Screen ID và
          sub-state cho TỪNG dòng. KHÔNG bỏ dòng có B/C rỗng.
    B2.2: Lọc dòng có Screen ID (đã fill) = "SLC0701". Nếu không có dòng nào hoặc
          tất cả rỗng D/E/F/G → ghi "Chưa có Comment Figma cho SLC0701", KHÔNG bịa.
    B2.3: Mỗi dòng có dữ liệu thật: cột D "-" = ghi chú chung (không gán 1 field); comment
          lấy theo quy tắc B.4 (F có → dùng trực tiếp; F trống & E có → dịch E; cả hai trống
          → bỏ dòng); cột G xác định sub-state; phân loại (a) field
          detail (b) validation/điều kiện kích hoạt (c) hành vi hệ thống tự động (d) business
          rule (e) logic phụ thuộc tab/màn hình; không rõ → ghi nguyên văn + "chưa phân loại
          rõ". Ghi kèm "Theo Comment Figma No.X".

── BƯỚC 3 — PHẦN C: TỔNG HỢP, ĐỐI CHIẾU, BỔ SUNG ──
⚠ CẤU TRÚC SHEET THEO NC6: main chỉ (1)+(2); Input/Output + Actions nằm trong từng sub-screen.
  Nếu sheet hiện có mục 3/4 ở main (union) → DI CHUYỂN vào đúng sub-screen, rồi XOÁ khỏi main.
3a. Main screen: mục 1 bổ sung business rule còn thiếu; mục 2 đủ ảnh mọi state + mô tả layout.
3b. Từng sub-screen: đối chiếu field/action từ BƯỚC 1 (ảnh state đó) + BƯỚC 2 với bảng (3)/(4)
    hiện có → đánh dấu field/action thiếu (ghi nguồn), Required/Validation sai/thiếu.
3c. KIỂM TRA NGƯỢC chống field bịa: mọi dòng đang có phải có ≥1 bằng chứng (NC1). Không có →
    xoá hẳn. Nghi ngờ nhưng có thể đúng (ảnh mờ) → giữ + ghi chú.
3d. BỔ SUNG / SỬA:
    ◆ Xoá field bịa: xoá dòng + QUÉT TOÀN BỘ sheet xoá/sửa mọi tham chiếu còn sót. Renumber No.
    ◆ Thêm field thiếu vào đúng sub-screen: chèn đúng vị trí, copy style, renumber, nguồn (NC9).
    ◆ Sửa Required/Validation: Required="Có" chỉ khi trích được "tên※" từ Function List; không
      → "-". Giá trị hệ thống → I/O="Output", Required="-".
    ◆ Chuẩn hoá Error Message (NC7): Required="Có" → 「必須項目を入力してください。」; ngoại lệ
      giữ nguyên. In số dòng đã chuẩn hoá.
    ◆ Xây/sửa sub-screen (NC6): mỗi sub-screen đủ (1) Overview (2) Layout CÓ ẢNH CHÈN THẬT
      (3) Input/Output là BẢNG đủ cột (4) Actions là BẢNG đủ cột. Dạng tóm tắt + tham chiếu →
      viết lại thành bảng đầy đủ. In số sub-screen đã xây đủ.
    ◆ Ô không xác định (NC8): ghi "-". Dòng mới giữ đúng style dòng xung quanh.
    ◆ Áp quy tắc common (NC0): với mỗi màn hình/sub-screen, chủ động thêm NC0.1–NC0.7 vào
      đúng cột (Validation Rule / Error Message / Actions Processing Details / Error Handling)
      cho các thành phần thực có (nút Lưu, trường giới hạn định dạng, tab form, nút Xóa, button
      reload...). Ghi nguồn "Theo quy tắc common NC0.<số>". KHÔNG áp cho thành phần không có.

── BƯỚC 4 — RÀ SOÁT CUỐI (BẮT BUỘC) ──
4a. Bảng tổng kết: field/action đã thêm (kèm nguồn), dòng sửa Required/Validation, field đã xoá.
4b. Verify không gộp (NC3): mỗi sub-screen so số ô input trên ảnh vs số dòng bảng (3). Không
    khớp → tách. In "Sub-screen X: ảnh=N ô, bảng=M dòng — [Khớp / Đã xử lý]".
4c. Verify Required (NC5): mọi Required="Có" nguồn Function List → xác nhận có ※ trong cột G;
    không có → sửa "-" + xoá nguồn. In danh sách đã sửa (kỳ vọng rỗng).
    Đồng thời xác nhận KHÔNG có field/action/rule nào lấy từ dòng "Ngoài phạm vi" (cột I =
    "Ngoài phạm vi" hoặc nền FFD9D9D9). Có → xoá + quét sạch. In danh sách (kỳ vọng rỗng).
4d. Verify Error Message (NC7): đếm Required="Có" có Error ≠ chuẩn & không ngoại lệ → kỳ vọng 0.
4e. Verify sub-screen (NC6): mỗi sub-screen đủ 4 mục; (2) có ảnh chèn thật (ws._images anchor
    trong vùng row block); (3)(4) là bảng đủ cột. In "Sub-screen X: [Đạt / Chưa đạt — lý do]".
4f. Verify main không còn mục 3/4: in "Main screen: [Chỉ có mục 1+2 / Còn sót — cần xử lý]".
4g. Verify quét sạch sau xoá: mỗi field/button đã xoá → search toàn sheet, in "còn 0 chỗ sót".
4h. Verify ngược lần cuối: rà mọi dòng (3)/(4) mọi sub-screen theo NC1; phát hiện bịa → xoá +
    quét sạch như 3d.
4i. Verify quy tắc common (NC0): với MỖI màn hình/sub-screen, rà từng NC0.1–NC0.7 và đối chiếu
    với thành phần thực có trên màn hình:
    • Có nút Lưu + trường bắt buộc → phải có NC0.1 (disabled/enabled) + NC0.4 (message required).
    • Có trường giới hạn định dạng → phải có NC0.2 trong Validation Rule.
    • Có form nhập trên tab → phải có NC0.3 (cảnh báo chuyển tab khi dirty).
    • Mọi màn hình có lỗi → cơ chế hiển thị NC0.5 (Inline vs Toast) được nêu.
    • Có button cần reload → NC0.6. Có nút Xóa → NC0.7 (popup xác nhận).
    Thành phần có mà thiếu quy tắc → bổ sung (ghi nguồn "Theo quy tắc common NC0.<số>").
    Áp NC0 cho thành phần KHÔNG tồn tại → xoá (vi phạm NC1). In "NC0: đã áp N quy tắc, đã bổ
    sung M, đã gỡ K áp sai".


═══════════════════════════════════════════════════════════════════════════════
GIAI ĐOẠN III — DỊCH SANG TIẾNG VIỆT cho sheet Screen_SLC0701 システムログ参照
═══════════════════════════════════════════════════════════════════════════════

Sử dụng skill `xlsx`. CHỈ xử lý sheet Screen_SLC0701 システムログ参照, KHÔNG đụng sheet khác, giữ nguyên tên sheet.
Chỉ chạy sau khi GIAI ĐOẠN I & II hoàn tất và các verify đạt.

Mục tiêu: chuyển toàn bộ nội dung sheet sang CHỈ CÒN TIẾNG VIỆT, xóa sạch tiếng Nhật/Anh xen
lẫn, NGOẠI TRỪ các nhãn tên trường ("Display Item Name") và chuỗi Error Message chuẩn hoá.

Quy tắc:
D1. Mọi ô văn bản (Overview, Display Conditions, Initial Display Behavior, Layout Description,
    Remarks, Error Handling, Validation Rule, Processing Details, ghi chú/instruction, block
    sub-screen...): song ngữ Nhật–Việt → giữ tiếng Việt, xoá tiếng Nhật; chỉ tiếng Nhật/Anh
    → dịch sang tiếng Việt và thay thế.
D2. Rà tiếng Nhật/Anh NẰM LẪN trong câu tiếng Việt và dịch/loại bỏ (tiêu đề Anh như "Layout
    Description", "state"; cụm Nhật mô tả). Sau xử lý, ô mô tả KHÔNG còn Hiragana/Katakana/
    Kanji, TRỪ nhãn tên trường (D3) và Error Message chuẩn (D4).
D3. NGOẠI LỆ — giữ nguyên tiếng Nhật cho nhãn tên trường ("Display Item Name") ở MỌI vị trí:
    - Cột Display Item Name (表示項目名) trong mọi bảng Input/Output của mọi sub-screen: giữ
      nguyên nhãn Nhật gốc (VD 氏名, ふりがな, 保存ボタン, 住所（都道府県）), KHÔNG thêm bản dịch
      song ngữ — nếu ô đang song ngữ chỉ giữ phần tiếng Nhật.
    - Nhãn tên trường TRÍCH DẪN trong câu tiếng Việt ở ô mô tả (VD Layout "Row 1: 氏名 |
      ふりがな | 郵便番号", hoặc nhãn「氏名」): giữ nguyên tên trường tiếng Nhật, chỉ dịch phần
      diễn giải xung quanh.
D4. Trong bảng Item List: cột kỹ thuật (Type, Required, I/O, Data Type, Max Length, Default
    Value) giữ nguyên. Cột mô tả (Validation Rule, Error Message, Remarks) dịch theo D1–D2
    (chỉ giữ tiếng Nhật ở phần là trích dẫn nhãn tên trường).
    ⚠ Error Message và mọi message hệ thống (kể cả các message common NC0) DỊCH LUÔN sang
    tiếng Việt, dùng đúng các bản dịch chuẩn sau (thống nhất toàn bộ tài liệu):
      • 「必須項目を入力してください。」 → "Vui lòng nhập các mục bắt buộc." (NC0.4 / NC7 —
        cho mọi field Required="Có").
      • 「入力した情報はまだ保存されていません。この画面を閉じてもよろしいでしょうか。」 →
        "Thông tin đã nhập chưa được lưu. Bạn có chắc chắn muốn đóng màn hình này không?" (NC0.3).
      • 「削除してもよろしいでしょうか。」 → "Bạn có chắc chắn muốn xóa không?" (NC0.7).
      Các Error Message ngoại lệ khác (lỗi format/trùng lặp...) cũng dịch sang tiếng Việt,
      diễn đạt sát nghĩa gốc.
D5. Giữ nguyên định dạng: layout, merge cells, độ rộng cột/dòng, style, màu, ẢNH ĐÃ CHÈN, và
    header hệ thống (Asset Name / Author / Creation Date / Updated By / Update Date). Cập nhật
    Update Date (và Updated By nếu phù hợp).

Thuật ngữ nghiệp vụ (dữ liệu đăng ký dự thưởng, mapping cột CSV, chiến dịch, required mark,
session/JWT, breadcrumb...) dịch sát ngữ cảnh hệ thống, diễn đạt tự nhiên trong tài liệu đặc
tả màn hình.


═══════════════════════════════════════════════════════════════════════════════
LƯU & TỰ KIỂM TRA CUỐI CÙNG
═══════════════════════════════════════════════════════════════════════════════
L1. LƯU vào chính file output per-screen ở B.1 (tên theo QUY TẮC TÊN FILE OUTPUT — GIAI ĐOẠN I),
    KHÔNG đổi tên, KHÔNG tạo thêm file khác. File này CHỈ chứa DUY NHẤT 1 sheet Screen_SLC0701 システムログ参照
    (không có "Screen List"/"Screen Transition Diagram"/màn hình khác). Trước khi ghi, đọc lại
    file đảm bảo không mất định dạng/ảnh; sau khi ghi, xác nhận file mở được và có đúng 1 sheet.
L2. SELF-CHECK NGÔN NGỮ: quét sheet Screen_SLC0701 システムログ参照, liệt kê mọi ô còn ký tự tiếng Nhật và xác
    nhận chúng CHỈ là nhãn tên trường (cột Display Item Name hoặc trích dẫn như tên trường
    trong ô mô tả). Error Message KHÔNG được còn tiếng Nhật (đã dịch hết theo D4). Nếu còn
    tiếng Nhật/Anh ngoài nhãn tên trường → sửa rồi lưu lại.
L3. IN TÓM TẮT CUỐI: (a) kết quả verify GIAI ĐOẠN II (NC), (b) số ô đã dịch GIAI ĐOẠN III,
    (c) danh sách ô còn tiếng Nhật kèm lý do hợp lệ, (d) số ảnh đã chèn, (e) sub-screen đã cover.