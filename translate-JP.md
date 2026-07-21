# PROMPT DỊCH NỘI DUNG SHEET: TIẾNG VIỆT → TIẾNG NHẬT
> Dùng cho file *Screen Definition* (画面定義書) của Lottery Campaign.
> Cách dùng: thay `Screen_SLC0202 口数設定` bằng tên sheet, dán toàn bộ nội dung sheet vào `{{SHEET_CONTENT}}`, rồi gửi cho AI.
> **Mỗi lần chạy 1 sheet sẽ tạo ra một file XLSX MỚI RIÊNG.** Tên file đích = **tên sheet + `_JP.xlsx`**, lưu trong folder `output`. Chạy sheet nào ra file nấy — không gộp chung, không ghi tích lũy.

---

## ▶️ MỖI LẦN CHẠY THÌ ĐỔI Ở ĐÂU?

Mỗi lần muốn dịch một sheet khác, **chỉ cần đổi đúng 1 chỗ**: giá trị `Screen_SLC0202 口数設定` (ở phần “Đầu vào” bên dưới) thành **tên sheet** bạn muốn chạy. Các phần còn lại (`SOURCE_FILE`, `OUTPUT_DIR`, quy tắc, glossary) **giữ nguyên**.

- Tên file đích được **tự động suy ra** từ `Screen_SLC0202 口数設定`: `OUTPUT_DIR / Screen_SLC0202 口数設定_JP.xlsx`.
- Ví dụ chạy sheet `Screen_SLC0101 基本設定` → file đích: `Screen_SLC0101 基本設定_JP.xlsx`.
- Ví dụ chạy sheet `Screen_SLC0102 応募データフォーマット` → file đích: `Screen_SLC0102 応募データフォーマット_JP.xlsx`.
- Lần sau chạy sheet khác → chỉ đổi lại `Screen_SLC0202 口数設定`, hệ thống tạo file `_JP.xlsx` mới tương ứng.
- Nếu dán nội dung trực tiếp thì cập nhật luôn `{{SHEET_CONTENT}}` cho khớp sheet đó. Nếu để AI/script tự đọc từ `SOURCE_FILE` thì **không cần** dán `{{SHEET_CONTENT}}`.

**Danh sách 12 sheet (copy tên dán vào `Screen_SLC0202 口数設定`) — tick ✅ khi dịch xong:**

| # | Tên sheet (`Screen_SLC0202 口数設定`) | File đích tạo ra | Trạng thái |
|---|---|---|---|
| 1 | `Screen List` | `Screen List_JP.xlsx` | ☐ |
| 2 | `Screen Transition Diagram` | `Screen Transition Diagram_JP.xlsx` | ☐ |
| 3 | `Screen_T-03 ログイン` | `Screen_T-03 ログイン_JP.xlsx` | ☐ |
| 4 | `Screen_SLC0102 応募データフォーマット` | `Screen_SLC0102 応募データフォーマット_JP.xlsx` | ☐ |
| 5 | `Screen_SLC0103 抽選枠設定` | `Screen_SLC0103 抽選枠設定_JP.xlsx` | ☐ |
| 6 | `Screen_SLC0104 重複チェック` | `Screen_SLC0104 重複チェック_JP.xlsx` | ☐ |
| 7 | `Screen_SLC0201 基本設定` | `Screen_SLC0201 基本設定_JP.xlsx` | ☐ |
| 8 | `Screen_SLC0204 抽選枠判定条件` | `Screen_SLC0204 抽選枠判定条件_JP.xlsx` | ☐ |
| 9 | `Screen_SLC0301 キャンペーン一覧` | `Screen_SLC0301 キャンペーン一覧_JP.xlsx` | ☐ |
| 10 | `Screen_SLC0401 抽選枠一覧` | `Screen_SLC0401 抽選枠一覧_JP.xlsx` | ☐ |
| 11 | `Screen_SLC0501 応募一覧` | `Screen_SLC0501 応募一覧_JP.xlsx` | ☐ |
| 12 | `Screen_SLC0601 応募詳細` | `Screen_SLC0601 応募詳細_JP.xlsx` | ☐ |

> Gợi ý: chạy tuần tự từ trên xuống. Sau khi chạy hết 12 sheet, bạn sẽ có **12 file `_JP.xlsx` riêng biệt** trong folder `output`, mỗi file là 1 sheet đã dịch.

---

## ⚙️ CẤU HÌNH (chỉnh trước khi chạy nếu cần)

- `SOURCE_FILE = "/home/sotatek/DucNguyen/ADF_Lottery_Campaign/output/[Lottery Campaign ] Screen Definition_07142026_Ver1.1.xlsx"` → File gốc (tiếng Việt).
- `OUTPUT_DIR = "/home/sotatek/DucNguyen/ADF_Lottery_Campaign/output"` → **Thư mục** chứa các file đích. Mỗi sheet dịch xong tạo 1 file mới trong thư mục này.
- `OUTPUT_FILE = OUTPUT_DIR + "/" + Screen_SLC0202 口数設定 + "_JP.xlsx"` → **Tên file đích tự suy ra từ tên sheet** (không đặt thủ công). VD `Screen_SLC0202 口数設定` = `Screen_SLC0101 基本設定` → `OUTPUT_FILE` = `.../output/Screen_SLC0101 基本設定_JP.xlsx`.
- `KEEP_ENGLISH_TECH_TOKENS = true` → Giữ nguyên các token kỹ thuật/enum tiếng Anh (`String`, `Input`, `Output`, `Text Box`, `Button`, `Label`, `onClick`, `onLoad`, `onInput`, `API`, `URL`…). *(Khuyến nghị: để `true`.)*
- `KEEP_BILINGUAL_HEADERS = true` → Giữ nguyên các tiêu đề mẫu song ngữ Anh/Nhật có sẵn (VD `Screen Overview / スクリーン概要`). Đặt `false` nếu muốn **chỉ còn tiếng Nhật** (bỏ phần tiếng Anh, giữ phần tiếng Nhật).
- Yêu cầu bắt buộc bất kể cấu hình: **KẾT QUẢ KHÔNG ĐƯỢC CÒN BẤT KỲ TIẾNG VIỆT NÀO.**

---

## 📌 PROMPT (copy phần dưới đây gửi cho AI)

Bạn là **biên dịch viên kỹ thuật chuyên tài liệu định nghĩa màn hình (画面定義書) tiếng Nhật** trong lĩnh vực phát triển phần mềm. Nhiệm vụ: dịch **toàn bộ phần tiếng Việt** trong nội dung sheet dưới đây sang **tiếng Nhật tự nhiên, chuẩn văn phong tài liệu thiết kế**.

### Đầu vào
- File gốc: **{{SOURCE_FILE}}** (mặc định `/home/sotatek/DucNguyen/ADF_Lottery_Campaign/output/VN/[Lottery Campaign ] Screen Definition_SLC0202 口数設定_07202026_Ver1.2.xlsx`)
- Thư mục đích: **{{OUTPUT_DIR}}** (mặc định `/home/sotatek/DucNguyen/ADF_Lottery_Campaign/output/JP`)
- Tên sheet cần dịch: **Screen_SLC0202 口数設定**
- File đích cần tạo (tự suy ra): **`{{OUTPUT_DIR}}/Screen_SLC0202 口数設定_JP.xlsx`**
- Nội dung sheet (nếu dán trực tiếp):
```
{{SHEET_CONTENT}}
```

### GHI RA FILE ĐÍCH (quy trình bắt buộc — MỖI SHEET LÀ MỘT FILE MỚI)

1. **Xác định tên file đích:** ghép `OUTPUT_DIR` + `/` + `Screen_SLC0202 口数設定` + `_JP.xlsx`. Giữ nguyên khoảng trắng và ký tự tiếng Nhật trong tên sheet (VD `Screen_SLC0101 基本設定_JP.xlsx`). Không đổi tên, không đổi thư mục.
2. **Tạo file đích MỚI cho mỗi lần chạy:**
   - Mở workbook gốc `SOURCE_FILE`, lấy **đúng sheet `Screen_SLC0202 口数設定`**.
   - Tạo một **workbook mới chỉ chứa 1 sheet** là sheet `Screen_SLC0202 口数設定` này, **sao chép nguyên vẹn** nội dung và định dạng: giữ đủ **merge cell, format, độ rộng cột, chiều cao dòng, font, màu, border, hình ảnh, style**. Không tạo file rỗng.
   - Ghi bản dịch tiếng Nhật vào chính sheet đó trong file mới.
3. **Nếu file đích đã tồn tại từ lần chạy trước:** **ghi đè (overwrite)** file đó bằng bản dịch mới. Mỗi file chỉ tương ứng 1 sheet, nên không cần gộp hay giữ sheet khác.
4. **Cách ghi vào từng ô:** chỉ **thay giá trị chữ (text) của các ô có tiếng Việt** bằng bản dịch tiếng Nhật; **giữ nguyên** vị trí ô, merge cell, font, màu, border, số/ngày/công thức và mọi ô không đổi. Không chèn/xóa dòng, cột.
5. **Mỗi lần chạy độc lập:** KHÔNG mở, KHÔNG sửa, KHÔNG gộp vào các file `_JP.xlsx` của sheet khác. Chạy sheet nào chỉ đụng đúng file của sheet đó.

### ⚠️ GIỮ NGUYÊN FORMAT — TUYỆT ĐỐI (bắt buộc, ưu tiên cao nhất)

Sheet output **phải giống hệt** sheet đang dịch về mọi mặt định dạng. **CHỈ được đổi phần chữ (text) tiếng Việt → tiếng Nhật**, ngoài ra **KHÔNG được tự ý thay đổi bất cứ thứ gì khác**. Cụ thể phải giữ nguyên 100%:

- **Kích thước ô / độ rộng cột (column width) / chiều cao dòng (row height)** — không co giãn, không auto-fit lại.
- **Merge cell (ô gộp)** — giữ đúng phạm vi gộp, không tách, không gộp thêm.
- **Vị trí ô** — chữ nào ở ô nào giữ đúng ô đó; không dời sang ô khác, không chèn/xóa dòng, cột.
- **Font** (tên font, cỡ chữ, đậm/nghiêng/gạch chân), **màu chữ**, **màu nền (fill)**, **border** (kiểu, màu, độ dày).
- **Canh lề (alignment)**: canh ngang/dọc, **wrap text (xuống dòng trong ô)**, indent, xoay chữ.
- **Định dạng số/ngày (number format)**, công thức, và mọi ô không chứa tiếng Việt → **để nguyên không đụng vào**.
- **Hình ảnh, shape, icon, freeze panes, độ zoom, ẩn/hiện dòng-cột** — giữ y nguyên.

**Nguyên tắc thực hiện:** thao tác bằng cách **sao chép nguyên workbook/sheet gốc rồi chỉ set lại `.value` (text) cho những ô có tiếng Việt**. KHÔNG dựng lại sheet từ đầu, KHÔNG ghi kiểu "tạo mới rồi tự định dạng lại" (sẽ làm mất format). Nếu công cụ có nguy cơ làm mất style khi ghi, phải chọn cách ghi giữ nguyên style của ô.

**Tự kiểm tra format trước khi lưu:** so sánh nhanh sheet output với sheet gốc — độ rộng cột, chiều cao dòng, các vùng merge, border và màu phải khớp. Nếu lệch, sửa lại cho khớp rồi mới lưu.

### QUY TẮC DỊCH (bắt buộc tuân thủ)

**1. Phạm vi dịch**
- Dịch **mọi** câu, cụm từ, ghi chú, thông báo lỗi… đang viết bằng tiếng Việt sang tiếng Nhật.
- Với câu **lẫn lộn Việt + Nhật** (VD: `Hiển thị khi người dùng chọn tab 「応募データフォーマット」`), dịch phần tiếng Việt và ghép thành **một câu tiếng Nhật hoàn chỉnh, trôi chảy**. Không để sót từ tiếng Việt nào.
- **KHÔNG được bỏ sót, tóm tắt hay rút gọn** nội dung. Dịch đủ ý 1–1.

**2. Giữ nguyên (KHÔNG dịch, KHÔNG đổi)**
- Văn bản **đã là tiếng Nhật** → giữ y nguyên.
- Tên UI / nhãn hệ thống trong 「」 (VD `「応募データフォーマット」`, `「キャンペーン一覧」`), tên trường: `氏名`, `郵便番号`, `保存ボタン`…
- Ký tự cột: `A列`, `B列`… ; thuật ngữ `列番号`, `半角英数`, `固定項目`, `個別検索項目`.
- Mã định danh & tham chiếu: `キャンペーンID`, `URL`, đường dẫn (`/campaigns/{キャンペーンID}/format`), `NC0.1`/`NC0.2`/`NC0.5`, `Comment Figma No.x`, `Function List No.x`, `Final_Screen List`.
- Số, ngày tháng, ID, mã lỗi, tên API, tên sự kiện (`onClick`, `onLoad`, `onInput`, `onChange`).
- Token kỹ thuật/enum tiếng Anh (nếu `KEEP_ENGLISH_TECH_TOKENS = true`): `String`, `Text Box`, `Button`, `Label`, `Input`, `Output`, `Badge`, `Icon Button`, `Link`…

**3. Giữ nguyên cấu trúc & định dạng**
- Giữ đúng **số thứ tự, bố cục dòng/ô, dấu xuống dòng (`\n`), bullet (`•`), ngoặc 「」（）**, thứ tự các mục.
- Không thêm/bớt ô, không đổi vị trí, không thêm bình luận của người dịch.
- Nếu đầu vào theo dạng `Ô | Giá trị`, giữ nguyên mã ô, chỉ dịch phần giá trị.

**4. Văn phong tiếng Nhật**
- Phần mô tả nội bộ (Screen Overview, Validation Rule, Processing Details, Remarks…): dùng **thể thường/thể định nghĩa** (常体・体言止め・「〜する」), ngắn gọn, mang tính kỹ thuật.
- **Thông báo hiển thị cho người dùng cuối** (Error Message, hộp thoại xác nhận): dùng **thể lịch sự** đúng chuẩn (VD `必須項目を入力してください。`). Nếu bản gốc đã có sẵn câu tiếng Nhật cho message thì **ưu tiên dùng đúng câu đó**.
- Thuật ngữ phải **nhất quán toàn bộ** theo bảng thuật ngữ bên dưới.

**5. Tiêu đề mẫu song ngữ**
- Nếu `KEEP_BILINGUAL_HEADERS = true`: giữ nguyên (VD `Screen Overview / スクリーン概要`).
- Nếu `false`: chỉ giữ phần tiếng Nhật, bỏ phần tiếng Anh.

### BẢNG THUẬT NGỮ CHUẨN (Việt → Nhật) — dùng để dịch nhất quán

| Tiếng Việt | Tiếng Nhật |
|---|---|
| màn hình | 画面 |
| ứng tuyển / đăng ký dự thưởng | 応募 |
| thông tin ứng tuyển / dữ liệu đăng ký | 応募データ／応募情報 |
| chiến dịch | キャンペーン |
| bốc thăm /抽選 | 抽選 |
| khung/suất bốc thăm (抽選枠) | 抽選枠 |
| mục / hạng mục | 項目 |
| mục bắt buộc | 必須項目 |
| mục cố định (固定項目) | 固定項目 |
| số cột | 列番号 |
| nút | ボタン |
| lưu | 保存 |
| hiển thị | 表示 |
| điều kiện hiển thị | 表示条件 |
| hiển thị ban đầu / khởi tạo | 初期表示 |
| người dùng | ユーザー |
| đăng nhập | ログイン |
| đăng xuất | ログアウト |
| ký tự nửa chiều chữ-số | 半角英数 |
| văn bản gợi ý / placeholder | プレースホルダー |
| điều hướng / chuyển (màn hình/tab) | 遷移 |
| chuyển tab | タブ切り替え |
| trạng thái | 状態／ステータス |
| kích hoạt (enable) / vô hiệu (disable) | 活性化（enable）／非活性（disable） |
| điều kiện | 条件 |
| ánh xạ (mapping) | マッピング |
| hợp lệ / kiểm tra hợp lệ | バリデーション／入力チェック |
| thông báo | メッセージ／通知 |
| hộp thoại xác nhận | 確認ダイアログ／確認ポップアップ |
| cảnh báo | 警告 |
| tải / tải lên / tải xuống | 取得／アップロード／ダウンロード |
| gọi API | API呼び出し |
| hệ thống gán sẵn | システムが割り当てる |
| không cho chỉnh sửa | 編集不可 |
| căn giữa dưới cùng | 最下部中央に配置 |
| theo chiều dọc | 縦方向 |
| thanh trên cùng | ヘッダー（最上部バー） |
| menu trái | 左メニュー |

### CÂU MẪU CHUẨN (translation memory — dịch giống hệt khi gặp lại)

- `Giá trị cố định do hệ thống gán, không cho chỉnh sửa.`
  → `システムが割り当てる固定値であり、編集不可。`
- `Chỉ nhập ký tự nửa chiều chữ-số (半角英数); chặn nhập trực tiếp khi sai định dạng (Theo quy tắc common NC0.2).`
  → `半角英数のみ入力可。フォーマット不正の場合は直接入力をブロックする（共通ルール NC0.2に従う）。`
- `Giá trị nhập là số cột (列番号) tương ứng của mục này trong file Excel dữ liệu ứng tuyển.`
  → `入力値は、応募データのExcelファイルにおける当該項目の列番号とする。`
- `Theo Comment Figma No.9: không gắn mark bắt buộc; dữ liệu ứng tuyển có thể không chứa thông tin cá nhân.`
  → `Figmaコメント No.9に従う：必須マークは付与しない。応募データには個人情報が含まれない場合があるため。`
- `Lỗi hệ thống/API → Toast (Theo quy tắc common NC0.5).`
  → `システム／APIエラー → トースト表示（共通ルール NC0.5に従う）。`
- `Vui lòng nhập các mục bắt buộc.`
  → `必須項目を入力してください。`
- `Không được phép nhập trùng mã cột.`
  → `列番号を重複して入力しないでください。`
- `Thông tin ứng tuyển (dữ liệu đăng ký).`
  → `応募情報（応募データ）。`
- `Thông tin đọc từ hóa đơn bằng OCR (Theo Function List No.39).`
  → `OCRでレシートから読み取った情報（Function List No.39に従う）。`
- `Thao tác click`
  → `クリック操作`
- `Theo quy tắc common NC0.x` → `共通ルール NC0.xに従う`
- `Theo Function List No.x` → `Function List No.xに従う`

### YÊU CẦU ĐẦU RA
- **Tạo file mới `{{OUTPUT_DIR}}/Screen_SLC0202 口数設定_JP.xlsx`** chứa đúng 1 sheet `Screen_SLC0202 口数設定` đã dịch, theo đúng quy trình mục **“GHI RA FILE ĐÍCH”** ở trên. Mỗi lần chạy = 1 file mới độc lập.
- Nội dung sheet sau khi ghi: **giữ nguyên 100% format của sheet gốc** (kích thước ô, độ rộng cột, chiều cao dòng, merge cell, font, màu, border, canh lề, wrap text, number format, hình ảnh…) theo đúng mục **“⚠️ GIỮ NGUYÊN FORMAT — TUYỆT ĐỐI”**. Chỉ đổi phần chữ tiếng Việt sang **tiếng Nhật** (cộng các token kỹ thuật được phép giữ theo cấu hình). Không tự ý thay đổi bất kỳ định dạng nào.
- **Tự kiểm tra trước khi lưu:** rà lại sheet vừa dịch, đảm bảo **không còn một ký tự tiếng Việt nào** (không còn `ă â đ ê ô ơ ư` và dấu thanh). Nếu còn, dịch nốt rồi mới lưu.
- Sau khi lưu, báo lại ngắn gọn: **tên file đích vừa tạo** (`Screen_SLC0202 口数設定_JP.xlsx`), **sheet đã ghi**, và **đường dẫn đầy đủ** của file.

--- HẾT PROMPT ---