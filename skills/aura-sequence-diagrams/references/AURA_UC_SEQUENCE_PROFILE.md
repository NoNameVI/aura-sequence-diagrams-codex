# Quy trình sequence diagram AURA được chốt

**Phiên bản quy tắc:** 3.1.0. Skill điều phối: `../SKILL.md`; lịch sử phiên bản: `../CHANGELOG.md`. Tài liệu này là nguồn quy tắc duy nhất; không sao chép nội dung quy tắc sang skill. Đây là bản đóng gói để chia sẻ; các đường dẫn workspace, tên database và bước build release bên dưới chỉ áp dụng khi người dùng có dự án AURA tương ứng.

**Hiệu lực:** 30-10-2026; cập nhật quy tắc `opt`/`alt`, `ref`, khung A3 và workflow V9 đến ngày 06-11-2026. Áp dụng cho sequence diagram AURA, gồm release V9 của tám feature đã chốt; các release cũ vẫn giữ để truy vết lịch sử. Bản UC-13.3 `alt` lồng nhau đã được người dùng chốt là mẫu trình bày. Tài liệu này thay các chỉ dẫn trình bày xung đột trong bản v2/v5/v6. Đây là **quy ước dự án AURA**, không phải lời khẳng định rằng OMG bắt buộc mọi sơ đồ đều phải theo đúng một kiểu bố cục.

## Trình tự làm việc

1. Trong workspace AURA, kiểm tra `Code/AURA Shore Store/AGENTS.md`, `docs/CODEBASE_MAP.md` và độ mới của Cartographer. Đối chiếu controller, service, validator, repository, mapper, entity, DTO và template thực tế. Ghi nhận phiên bản/đường dẫn code đã dùng. Ở dự án khác, dùng source code và tài liệu UC được cung cấp để xác nhận hành vi.
2. Lập luồng nghiệp vụ chính, điều kiện, kết quả và đường lỗi của từng UC. Chỉ mô tả hành vi được code hoặc tài liệu UC xác nhận; đánh dấu chênh lệch thay vì tự bổ sung nghiệp vụ.
3. Mỗi UC có một **diagram tổng quan chính**. UC dài được phép dùng `ref` để gọi các interaction chi tiết được định nghĩa trong diagram riêng. Không dùng `break` trong bộ 19 UC này. Dùng `alt` cho từ hai đường xử lý loại trừ nhau, `opt` cho đúng một đường xử lý có thể xảy ra hoặc không xảy ra, `loop` cho lặp thực sự. Không thay `alt` bằng `break` hoặc lạm dụng `ref` chỉ để chữa bố cục.
4. Mỗi `alt` phải có thông điệp yêu cầu/kết quả hay phép xác định điều kiện **trước khi** mở hộp. Lồng `alt` khi điều kiện sau chỉ có ý nghĩa trong nhánh trước; có thể gộp khi các điều kiện cùng cấp và các đường đi vẫn rõ. Mỗi guard có ngoặc vuông. Hộp fragment có đủ **bốn cạnh**, đường phân cách operand chạm cả hai cạnh bên, không tràn canvas.
5. Đặt tên mọi thông điệp theo mục đích nghiệp vụ hoặc ý nghĩa trao đổi, ví dụ `Request publication status change`, `Find product`, `Read product record`, `Return product details`. Chỉ ghi tên nút/click khi thao tác UI là điều kiện nghiệp vụ quan trọng. Không hiển thị đoạn code, biểu thức/lệnh lập trình, endpoint/route HTTP, câu SQL, tên exception triển khai hoặc mã trạng thái kỹ thuật như `404`, `500`. **Tên method là ngoại lệ:** được phép ghi tên method hoặc lời gọi method ngắn như `findById(productId)` khi cần đối chiếu code và không làm nhãn khó đọc; không ghi kiểu dữ liệu, modifier, phần thân method hoặc cả chữ ký khai báo dài.
6. Vẽ participant có stereotype hiển thị: `«boundary»`, `«controller»`, `«service»`, `«repository»`, `«mapper»`, `«dto»` và loại liên quan khác. **Không vẽ Entity thành lifeline/participant** và không dùng stereotype `«entity»` trong sequence diagram. Request/response DTO liên quan vẫn được vẽ bằng stereotype `«dto»`. Database hiển thị đúng **`MySQL`**.
7. Chỉ vẽ self-call nếu code gọi một method trên chính participant và lời gọi đó có vai trò trong luồng. Không dùng self-call để biểu diễn phép gán, đọc thuộc tính hay câu `if` thông thường. Self-call tự nó không đồng nghĩa với `alt`; `alt` chỉ mở khi có những kết quả/đường xử lý loại trừ nhau.
8. Giữ các tương tác Non-UI khi chúng giải thích điều kiện nghiệp vụ, truy vấn, ánh xạ DTO hoặc kết quả trả về. Lược các phép tính nội bộ không ảnh hưởng cách hiểu UC. Mũi tên gọi đồng bộ là đường liền đầu kín tô đen; trả về là đường đứt đầu mở. Sử dụng activation bar cho lời gọi thực, không kéo qua các nhánh lỗi không còn chạy.
9. Giữ Arial, nhãn thông điệp dễ đọc, không đè lifeline/activation/border. Đánh số phân cấp theo thứ tự thực hiện và quy tắc đầu nhánh `alt`/`opt` bên dưới. Mọi số message và `ref` hiển thị phải có **một dấu chấm kết thúc ngay trước nội dung**, ví dụ `1. Request ...`, `1.1. Return ...`; dấu chấm phân cấp bên trong số vẫn giữ nguyên. Khi sơ đồ dài, trước hết lược chi tiết nội bộ không cần thiết và sắp xếp khoảng trống; nếu interaction vẫn quá dài hoặc có một đoạn nghiệp vụ độc lập, dùng `ref` theo quy tắc bên dưới.
10. Với release AURA V9, tạo nguồn `.puml`, master `.drawio` chỉnh sửa được và artefact `.svg` cho diagram tổng quan cùng từng interaction được tham chiếu; giữ `.mmd` hoặc metadata khi chúng hỗ trợ pipeline. V9 không sinh PNG/PNG 4K. Mở kiểm tra diagram tổng quan, bản dài nhất và mọi diagram con; soát đủ bốn cạnh frame, guard, mũi tên, stereotype, `MySQL`, liên kết `ref` và độ đọc. Sau tất cả chỉnh sửa và xuất SVG, thực hiện **cổng kiểm tra đánh số cuối cùng** theo mục bên dưới. Quy tắc chuyển sang `GitLab/aura-store` chỉ áp dụng trong workspace AURA và phải theo `AGENTS.md` tại đó. Với dự án khác, chỉ tạo những định dạng mà công cụ hiện có hỗ trợ.

## Cổng kiểm tra đánh số bắt buộc trước bàn giao

1. Đánh số là hạng mục QA ưu tiên cao nhất của bộ sequence AURA. **Bước cuối cùng trước mọi lần bàn giao** phải là rà soát numbering trên nguồn cuối cùng và artefact đã xuất. Không được coi diagram là hoàn tất khi cổng numbering chưa đạt.
2. Kiểm tra tối thiểu: không trùng số cho hai hành vi khác nhau; không thiếu bước cha; mỗi số có đúng một dấu chấm kết thúc trước nội dung; số tăng đúng cấp; mỗi operand có đúng số đầu nhánh; các message tiếp theo kế thừa đúng tiền tố đầu nhánh; sau `alt`/`opt` trở về đúng cấp; `ref` và diagram con khớp tiền tố hoặc dùng đúng ngoại lệ interaction tái sử dụng; note không được đánh như message nếu không có mũi tên.
3. Đối chiếu số giữa `.puml`, `.mmd` nếu có, `.drawio` và SVG. Kết quả trong SVG bàn giao phải giống nguồn; không chỉ dựa vào một file trung gian hoặc báo cáo cấu trúc chung. Với release lịch sử có PNG, chỉ dùng PNG để kiểm chứng chính release đó.
4. Kiểm tra từng operand của `alt`/`opt` độc lập và kiểm tra điểm nhập lại sau `end`. Một số hợp lệ ở nhánh này không được làm cha cho message nằm trong nhánh khác hoặc ngoài fragment.
5. Sau khi cổng numbering đạt, mọi sửa đổi có thể làm thay đổi message, fragment, `ref` hoặc thứ tự luồng đều làm kết quả hết hiệu lực và bắt buộc chạy lại kiểm tra numbering. Báo cáo bàn giao phải nêu rõ cổng đã đạt; còn một lỗi numbering xác nhận thì chưa bàn giao.

## Quy tắc đã chốt cho validation, `opt` và `alt`

1. Chỉ dùng self-call `Validate ...` khi participant thực sự gọi một method của chính nó để kiểm tra input và bước đó đáng thể hiện. Nếu Spring MVC, Bean Validation, validator/request object hoặc participant khác thực hiện validation thì vẽ đúng participant đó; không gán giả thành self-call của controller/service.
2. Có thể dùng `opt [Input is invalid]` cho một nhánh lỗi ngắn chỉ làm nhiệm vụ trả field errors/kết quả lỗi về Boundary và hiển thị cho Actor. Luồng hợp lệ tiếp tục bên ngoài hộp để giảm độ dài và độ lồng của diagram.
3. Vì UML `opt` chỉ có nghĩa operand được thực hiện hoặc bị bỏ qua, nó **không tự mang nghĩa dừng phần còn lại của interaction**. Khi dùng mẫu trên, nhánh lỗi phải thể hiện rõ điểm kết thúc: trả kết quả lỗi về caller, Boundary hiển thị lỗi, đóng các activation thuộc request lỗi và không để call/return treo. Không đặt thông điệp ghi dữ liệu của nhánh lỗi phía dưới `opt` theo cách khiến người đọc hiểu chúng vẫn chạy sau lỗi.
4. Nếu việc tiếp tục hay dừng sau lỗi vẫn có thể bị hiểu sai, phải dùng `alt [Input is invalid] / [Input is valid]`. Nhánh hợp lệ chứa phần xử lý tiếp theo trong operand của nó. Ưu tiên tính chính xác của trace hơn việc làm diagram ngắn.
5. Dùng `alt` khi cả hai hoặc nhiều kết quả đều có chuỗi xử lý riêng cần nhìn thấy, ví dụ `[Entity not found] / [Entity found]`, `[Reference inactive] / [Reference active]`, hoặc các trạng thái dẫn đến những repository call/state change khác nhau. Không bắt buộc hai operand có độ dài tương đương.
6. Mỗi `opt`/`alt` phải xuất hiện sau bước sinh hoặc đánh giá điều kiện. Guard mô tả trạng thái, không mô tả thao tác. Ví dụ đúng: `[Input is invalid]`; tránh `[Return validation error]`.

### Đánh số message bên trong `alt` và `opt`

1. Message ngay trước fragment, là bước sinh hoặc đánh giá điều kiện, được dùng làm **số neo** `P`. Khi thoát khỏi fragment, luồng ngoài tiếp tục bằng số kế tiếp cùng cấp của `P`: `3.` → `4.`; `5.1.` → `5.2.`; `3.2.4.` → `3.2.5.`.
2. Với `alt`, mỗi operand nhận một số đầu nhánh riêng theo thứ tự từ trên xuống: operand thứ nhất `P.1`, operand thứ hai `P.2`, operand thứ ba `P.3`... Số đầu nhánh phải gắn với **message có mũi tên đầu tiên** của operand, không gắn riêng cho guard hoặc tên operand.
3. Sau message đầu nhánh, các message còn lại trong cùng operand kế thừa toàn bộ số đầu nhánh và thêm một thành phần tăng dần: nhánh `P.1` có `P.1.1`, `P.1.2`...; nhánh `P.2` có `P.2.1`, `P.2.2`... Không dùng message của operand này làm cha cho message của operand khác.
4. Với `opt`, operand duy nhất bắt đầu bằng message `P.1`; các message tiếp theo trong operand là `P.1.1`, `P.1.2`... Nếu operand chỉ có một message thì chỉ dùng `P.1`.
5. Fragment lồng áp dụng đệ quy. Nếu message `P.1.2` sinh điều kiện cho một `alt` con, message đầu của hai operand con lần lượt là `P.1.2.1` và `P.1.2.2`; các message tiếp theo của operand thứ nhất là `P.1.2.1.1`... và của operand thứ hai là `P.1.2.2.1`... Sau fragment con, interaction trở lại cấp chứa bước neo.
6. Guard, nhãn `alt`/`opt`, đường phân cách operand, activation và note không có mũi tên không được nhận số message. Không tạo một số đầu nhánh chỉ để đặt lên guard.

Ví dụ `alt` được chấp nhận:

```text
3. Validator --> Controller: Return validation result
alt [Input is valid]
    3.1. Controller -> Service: create(request)
    3.1.1. Service -> Repository: Save product
    3.1.2. Repository --> Service: Return saved product
else [Input is invalid]
    3.2. Controller --> View: Return field errors
    3.2.1. View --> Actor: Display validation errors
end
4. Controller --> View: Return operation outcome
```

Ví dụ `opt` được chấp nhận:

```text
3. Validator --> Controller: Return validation result
opt [Input is invalid]
    3.1. Controller --> View: Return field errors
    3.1.1. View --> Actor: Display validation errors
end
4. Controller -> Service: create(request)
```

Ví dụ AURA rút gọn được chấp nhận:

```text
1. Controller -> Validator: Validate request
2. Validator --> Controller: Return validation result
opt [Input is invalid]
    2.1. Controller --> View: Return field errors
    2.1.1. View --> Actor: Display validation errors
end
[Khi input hợp lệ, luồng chính tiếp tục]
3. Controller -> Service: create(request)
```

Ví dụ trên là quy ước đọc rút gọn của AURA. Nếu bản vẽ không thể làm rõ rằng request lỗi kết thúc tại `Display validation errors`, chuyển sang `alt` đầy đủ.

## Quy tắc đã chốt cho `ref`

1. `ref` là một InteractionUse gọi interaction được định nghĩa riêng, không phải một khung cắt hình tùy ý. Diagram chính vẫn phải cho thấy mục tiêu UC, các quyết định nghiệp vụ quan trọng và kết quả cuối cho Actor.
2. Chỉ tách `ref` khi đoạn được tách có tên nghiệp vụ rõ ràng, nhiều thông điệp nội bộ, đầu vào/kết quả xác định, hoặc được tái sử dụng. Không tạo `ref` cho một truy vấn, một phép gán hay một validation ngắn chỉ để giảm chiều cao.
3. Nội dung hiển thị trong khung `ref` chỉ gồm **một mô tả nghiệp vụ ngắn và đủ nghĩa**, thường dùng động từ + đối tượng/mục tiêu, ví dụ `Validate publication eligibility`, `Add product variant` hoặc `Build product response`. Không hiển thị mã UC/Part trong khung; không liệt kê dài tham số, kiểu trả về hoặc chi tiết từng bước con. Tránh tên chung chung như `Process data`, `Handle request`, `Validate` hoặc `Save` khi chúng không giúp người đọc phân biệt interaction. Đầu vào, kết quả và mã diagram con vẫn được lưu trong nguồn/metadata hoặc tài liệu ánh xạ để truy vết và QA.
4. Khung `ref` phải phủ đúng các lifeline tham gia tại điểm gọi. Khi `ref` nằm trong một operand `alt`, `opt`, `loop` hoặc fragment khác, toàn bộ bốn cạnh và tab `ref` phải nằm trong biên operand cha với khoảng đệm nhìn thấy; không dùng chung cạnh, chạm biên hoặc đè lên tab/guard/divider của frame cha. Diagram con khai báo đủ participant thực sự trao đổi thông điệp và phải đọc được độc lập; không dựa vào biến, activation hoặc điều kiện chưa được giới thiệu.
5. Diagram chính xem `ref` như một lời gọi hoàn chỉnh. Không kéo activation nội bộ của diagram con xuyên qua hai file. Sau `ref`, ghi rõ kết quả nếu kết quả đó mở `alt`, `opt` hoặc quyết định bước tiếp theo.
6. Ưu tiên `ref` trả kết quả rồi đặt `alt` ở diagram chính khi quyết định là trọng tâm của UC. Có thể đặt `ref` bên trong một operand `alt` khi mỗi nhánh gọi một interaction riêng. Không giấu nhánh nghiệp vụ cốt lõi trong diagram con nếu việc đó khiến diagram chính không còn giải thích được UC.
7. Diagram chính đánh số bước `ref` như một bước cấp cao. Diagram con dùng số con của bước đó, ví dụ bước `4. ref ...` có `4.1.`, `4.2.`... Nếu interaction được tái sử dụng bởi nhiều UC, diagram con dùng mã interaction và số nội bộ riêng; không gắn cố định số của một UC.
8. Mỗi interaction được tham chiếu có một nguồn chính duy nhất và tên hiển thị ánh xạ rõ tới tên file/mã interaction. Không sao chép cùng một luồng thành nhiều diagram con độc lập dễ lệch nhau.
9. Bộ xuất phải chứa diagram tổng quan và toàn bộ diagram được `ref` gọi tới. QA kiểm tra không có `ref` mồ côi, tên/hợp đồng khớp, participant hợp lệ, numbering liên tục và đường quay lại luồng chính rõ ràng.
10. Một UC dùng tối đa khoảng **1–3 `ref`** ở diagram tổng quan. Mặc định chỉ tách hai cấp: diagram chính → diagram con. Không tạo chuỗi `ref` lồng nhiều tầng; diagram con chỉ được gọi thêm một interaction dùng chung khi có bằng chứng tái sử dụng thực sự và việc đó không làm mất khả năng theo dõi luồng.
11. Tên định danh kỹ thuật của diagram con dùng `UC-<mã UC>-Part-<n>_<Mô_tả_chức_năng>`, ví dụ `UC-13.2-Part-2_Add_Product_Variant`. Phần mô tả bắt đầu bằng động từ, nêu rõ đối tượng hoặc mục tiêu và dùng cùng ý nghĩa với caption hiển thị. Không dùng tham số, kiểu trả về, HTTP route, SQL, mã trạng thái, tên exception hoặc tên mơ hồ như `Process_Data`, `Handle_Request`, `Validate` hay `Save`. Diagram UC chính giữ tên UC hiện có, không thêm `Part`. Toàn bộ nguồn và artefact của interaction dùng cùng tên gốc; mã Part và mô tả phải được ánh xạ trong manifest, metadata và liên kết SDS. **Không hiển thị mã UC/Part trong caption khung `ref`**. Caption có dạng `<số bước>. <mô tả nghiệp vụ ngắn, đủ nghĩa>`, ví dụ `5. Add product variant`. Số Part là định danh tra cứu, không mặc nhiên là thứ tự chạy khi interaction dùng chung hoặc có nhánh `alt`.

## Khung trang và tỷ lệ đã chốt

1. Thiết kế mỗi diagram để đặt vừa một trang A3 ngang. Khung mục tiêu là **4:3** (`1.333:1`); có thể mở linh hoạt đến tỷ lệ A3 ngang (`420:297`, xấp xỉ `1.414:1`) khi số participant hoặc độ dài nhãn cần thêm chiều ngang.
2. Khoảng tỷ lệ khuyến nghị của canvas là `1.30:1` đến `1.42:1`. Đây là mục tiêu bố cục, không phải lý do để kéo giãn hình hoặc làm sai hình học UML.
3. SVG và Draw.io giữ cùng viewBox/canvas ratio: `4:3` hoặc A3 ngang theo phạm vi cho phép. Từ V9, SVG là hình bàn giao chuẩn và không bắt buộc sinh PNG/PNG 4K. Các release lịch sử có thể giữ PNG đã sinh nhưng không dùng chúng làm nguồn để chỉnh sửa hoặc làm chuẩn QA cho V9.
4. Không bóp/kéo ảnh khi chèn vào SDS, Word hoặc PDF. Giữ tỷ lệ gốc và căn giữa trong vùng in; phần dư của trang dành cho tiêu đề, mã UC, caption và lề an toàn.
5. Không giảm font, khoảng cách thông điệp, activation hoặc fragment đến mức khó đọc chỉ để đạt tỷ lệ. Khi nội dung vượt khung, xử lý theo thứ tự: lược chi tiết nội bộ không cần thiết, rút gọn nhãn nhưng giữ nghĩa, sắp xếp lại participant, rồi tách interaction bằng `ref`.
6. QA phải kiểm tra cả canvas và bản đặt trên trang A3: không cắt bốn cạnh fragment, không đè chữ, guard và numbering đọc được ở kích thước in dự kiến, và không có vùng trắng bất thường do ép tỷ lệ.
7. Tính đúng của interaction và khả năng đọc luôn ưu tiên hơn tỷ lệ trang. Nếu không thể đồng thời giữ đầy đủ luồng đúng và đạt khung 4:3/A3, cho phép lệch khỏi khoảng tỷ lệ khuyến nghị; ghi nhận lý do trong QA thay vì xóa nhánh nghiệp vụ, bóp hình hoặc làm chữ khó đọc.

## Quy tắc chọn mức chi tiết và participant

1. Actor của từng UC phải lấy nguyên tập vai trò được đánh dấu trong sheet `Authorization` của `AURA_Backlog.xlsx`; không tự tạo vai trò tổng quát như `Catalog manager`, `Catalog reader`, `Authorized staff` hoặc `Signed-in account holder`. Khi hiển thị, bỏ khoảng trắng trong tên từng vai trò và phân cách các vai trò bằng `/`, ví dụ `Sale&CustomerServiceStaff/WarehouseStaff`. Bộ dựng hình xuống dòng tại mỗi `/` để mỗi vai trò nằm trên một dòng khi nhãn có nhiều actor; dấu `/` vẫn được giữ ở cuối dòng trước để thể hiện tập vai trò.
2. Không chuyển mọi câu `if` trong code thành `alt`/`opt`. Chỉ tạo combined fragment khi điều kiện làm thay đổi chuỗi tương tác giữa participant, kết quả nghiệp vụ hoặc phản hồi cho Actor. Phép kiểm tra nội bộ không làm đổi luồng có thể được lược hoặc gộp vào một operation có tên rõ.
3. Không đưa Entity vào diagram như một lifeline, kể cả khi code đọc thuộc tính, thay đổi trạng thái hoặc tạo Entity. Gộp hành vi đó vào message có nghĩa trên Service/Repository/Mapper, hoặc thể hiện qua DTO/kết quả trả về khi cần hiểu UC. Tên Entity có thể xuất hiện như tên dữ liệu trong nhãn method hoặc kết quả, nhưng không phải participant riêng.
4. Request DTO và response DTO có liên quan trực tiếp đến UC phải được vẽ thành lifeline với stereotype `«dto»`, kể cả khi chúng chủ yếu mang dữ liệu. Chỉ đưa DTO thuộc phạm vi interaction; không thêm DTO không xuất hiện trong luồng code. Message tới/từ DTO phải phản ánh validation, mapping, construction hoặc truyền kết quả có thật, không sáng tác hành vi miền cho một data carrier. Khi cần chọn giữa Entity và DTO để trình bày dữ liệu, dùng DTO.
5. Dùng mức chi tiết thống nhất theo tầng và diễn đạt bằng ngôn ngữ nghiệp vụ/kỹ thuật dễ hiểu, không chép ký hiệu triển khai:
   - Actor → Boundary: mục đích nghiệp vụ; chỉ ghi tên nút/click khi thao tác UI là điều kiện quan trọng.
   - Boundary → Controller: yêu cầu hoặc lệnh nghiệp vụ được gửi; không ghi HTTP method/URL.
   - Controller → Service: ưu tiên hành động ứng dụng/nghiệp vụ; được dùng tên method hoặc lời gọi method ngắn khi cần truy vết.
   - Service → Repository: ưu tiên mục đích truy xuất/lưu dữ liệu; được dùng tên method repository hoặc lời gọi ngắn khi nó giúp đối chiếu code.
   - Repository → MySQL: thao tác dữ liệu ở mức `Read`, `Create`, `Update`, `Delete` cùng đối tượng; không ghi câu SQL, từ khóa SQL hay tên bảng/cột nếu chúng chỉ là chi tiết triển khai.
   - MySQL self-call: chỉ cho xử lý database ảnh hưởng kết quả nghiệp vụ; mô tả ý nghĩa, không ghi mã trigger/stored procedure hoặc câu lệnh.
6. Chỉ thể hiện transaction, khóa dữ liệu hoặc guard đồng thời khi chúng giải thích bất biến nghiệp vụ, thứ tự bắt buộc, rollback, chống trùng hoặc chống cập nhật cạnh tranh. Nhãn mô tả ý nghĩa như `Acquire catalog update lock`; không ghi cú pháp SQL như `FOR UPDATE`. Không thêm participant/message transaction như trang trí cho mọi service call.
7. Không dùng guard chung chung `[Error]` khi nguồn lỗi quyết định cách hiểu UC. Ưu tiên trạng thái cụ thể như `[Input is invalid]`, `[Product not found]`, `[Slug already exists]`, `[Reference is inactive]`. Chỉ tách thành nhiều fragment khi nguồn lỗi hoặc đường xử lý khác nhau; nếu nhiều kiểm tra cùng trả một kết quả và chi tiết không phải trọng tâm, có thể gom trong một interaction validation có tên rõ.
8. Return lỗi phải mô tả kết quả nghiệp vụ hoặc phản hồi cho caller, ví dụ `Return publication rejection`, `Return field errors` hoặc `Return product not found`. Không hiển thị tên lớp exception, stack trace hay mã HTTP. Không dùng return để mô tả một call mới và không tạo Exception thành lifeline riêng.

## Quy tắc activation và bước duyệt mẫu

1. Mọi synchronous call thực được vẽ phải mở activation trên lifeline nhận; call lồng hoặc self-call mở activation lồng. Activation bắt đầu khi call chuyển quyền điều khiển và kết thúc tại return hoặc điểm kết thúc operation tương ứng. Không được bỏ activation chỉ vì participant chỉ xuất hiện trong một message. Với `alt`/`opt`, phải kiểm tra riêng từng operand: nhánh đã trả lỗi hoặc kết thúc request không được để activation của Boundary, Controller, Service, Repository, Mapper, DTO hay Database kéo tiếp xuống luồng không còn chạy.
2. Không dùng một activation liên tục để che hai nhánh có thời điểm kết thúc khác nhau. Activation lồng phải đóng đúng call đã mở; sau `ref`, diagram chính chỉ tiếp tục activation phù hợp với hợp đồng trả về của interaction con.
3. QA activation là kiểm tra bắt buộc, độc lập với kiểm tra frame/mũi tên: mỗi synchronous call có activation nhận tương ứng; mỗi return đóng đúng activation; không có activation treo, activation xuyên nhánh lỗi, return không có call tương ứng, hoặc nested activation nhập thành một thanh khó phân biệt. `ref` trong diagram chính không kéo activation nội bộ của diagram con ra ngoài frame; diagram con tự thể hiện đầy đủ activation của interaction được tham chiếu.
4. Trước khi cập nhật đồng loạt 19 UC, chọn một UC dài làm **diagram mẫu phê duyệt**. Mẫu phải có validation bằng `opt` hoặc `alt`, ít nhất một nhánh nghiệp vụ `alt`, một `ref`, request/response DTO, MySQL/trigger nếu code có, activation đầy đủ và khung 4:3/A3; mẫu không có lifeline Entity.
5. Chỉ áp dụng hàng loạt sau khi người dùng duyệt nội dung, mức chi tiết, participant, numbering, `ref`, activation và bố cục của mẫu. Nếu quy tắc thay đổi trong lúc duyệt mẫu, cập nhật tài liệu quy tắc và mẫu trước khi sinh các UC còn lại.

## Nguồn đối chiếu

- OMG UML 2.5.1, chương 17: ngữ nghĩa Interaction, Lifeline, Message, CombinedFragment và InteractionOperand. Tài liệu OMG định nghĩa `alt`, `opt`, `loop`, `break`, `ref`; profile AURA hiện dùng `ref` theo hợp đồng interaction đã nêu ở trên và không dùng `break` trong bộ quy ước hiện tại.
- Visual Paradigm, hướng dẫn Sequence Diagram và Combined Fragment: minh họa ký pháp thông điệp, return, activation và guard. Xem `SOURCES.md` để tìm bản PDF/URL đã lưu.
- Code hiện tại trong `Code/AURA Shore Store` là nguồn xác nhận lớp, method và thứ tự xử lý; tài liệu UC/SDS và bảng quyền xác nhận phạm vi nghiệp vụ và actor.
