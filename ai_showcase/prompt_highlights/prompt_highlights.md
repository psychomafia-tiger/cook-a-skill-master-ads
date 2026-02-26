# Prompt Highlights

> This file is a compilation of the key prompts that owner Tiger used to create this SKILL.

---

# Giai đoạn 1: ( Brainstorm - viết spec.md )
1. T đang cần cook một cái skill cho ai agents liên quan đến ads marketing. Theo b t nên dùng : Openclaw, Antigravity? Cái nào sẽ tối ưu hơn? Bạn cần brainstorm với tôi những điểm nào để có thể bắt đầu viết spec.md ngay? Cấu trúc cụ thể và chi tiết chuẩn của 1 SKILL? Tham khảo 2 file tôi gửi nhé. (Sonnet-4.6) 

=> Brainstorm ý tưởng khi nhận được đề bài, hiểu ngay cấu trúc chuẩn của SKILL.md, quyết định build trên openclaw vì tiềm năng go to market cao hơn/ phù hợp với bất kì ai. 

2. Yêu cầu của tôi: Kịch bản ads phải cực kì chi tiết vì output ra cho team cùng triển khai => Phải có sự rõ ràng để đảm bảo flow trôi chảy. Về TA Setting: Phải nêu rõ được lí do vì sao gợi ý chọn setting đó, giải thích theo góc độ insight/tâm lí học hành vi/phù hợp với use case của sản phẩm/phù hợp văn hoá của địa điểm target/phù hợp lối sống của đối tượng mục tiêu. Về budget, nên hỏi mức budget có thể chi trả của users sử dụng skill, rồi mới gợi ý mức budget phù hợp/hiệu quả. Không dài dòng lan man, phải có 1 vài câu hỏi để nắm rõ các thông tin của sản phẩm, rồi đối chiếu với những điều kiện cần để có thể setting 1 campaign đẳng cấp => mới cho ra output. Giờ bắt đầu từ việc viết spec.md để brainstorm trước khi bắt tay vào build SKILL(Sonnet-4.6)

=> Thêm một số ràng buộc và kinh nghiệm cá nhân thực tế trong công việc để AI có thể hiểu rõ hơn về yêu cầu của tôi, từ đó đưa ra output hợp lí, vẫn để khoảng trống cho AI lấp những thứ mình có thể chưa biết. Đây gần như là prompt core nhất để tạo nền móng cho SKILL này. 

3. Giờ tôi sẽ mang cái draft này sang antigravity IDE để tinh chỉnh file .md bằng claude opus 4.6, hãy giúp tôi viết một prompt để Claude Opus bên đó có thể hiểu và tự làm nốt phần còn lại, yêu cầu nó chỉ ra lỗ hổng hoặc chỗ nào bất khả thi khi sử dụng với openclaw, phản biện spec hiện tại đề xuất phương án tối ưu hơn trước khi chỉnh sửa, chờ đợi tôi ra lệnh mới chỉnh sửa.(Sonnet-4.6)

=> Chuyển môi trường làm việc lần đầu, cho AI tự viết prompt cho bao quát và chuẩn chỉ.

# Giai đoạn 2 ( Building )

1. spec.md Với các công dụng trên, nếu được thêm một điều gì đó khác biệt, đột phá, làm user phải nghĩ rằng : "Wow, AI đã có thể mạnh đến mức này rồi ư?" hoặc "Thật sự đột phá, không thể tin nổi", bạn sẽ đề xuất là thêm tính năng gì? trao đổi với tôi ngay tại box trò chuyện này nhé.

=> Từ prompt này , chọn được Post-Playbook cho output.

2. Từ spec.md, lập 1 plan tạo SKILL.md for OpenClaw "Meta Ads Script & TA Generator" (Opus4.6) 

3. Plan: Create SKILL.md for Meta Ads Script & TA Generator
  Context
  The spec.md (design spec, supervisor-approved) needs to be converted into a SKILL.md — the runtime instruction file that an AI agent reads when executing the skill. The SKILL.md must be self-contained, use natural language only
  ... Verify business rules match spec Section 10
  Thấy Plan này thế nào hả Gemini? Có phản biện đi xem còn chỗ nào chưa được hoặc có thể cải thiện điều gì không?

=> Sau khi Opus gửi Plan, copy sang Gemini để mở rộng và tìm kẽ hở. ( Lí do: Gemini có nguồn Google, cực mạnh trong việc đọc kĩ các context dài lên tới 2M tokens)

Giai đoạn này liên tục cho các models phối hợp với nhau để kiểm tra chéo giữa Opus, Gemini. Đa số chỉ hướng tư duy cùng agents, đôi khi việc viết prompt yêu cầu agents khác kiểm tra cũng là AI tự làm luôn.

4. Sonnet ơi Gemini cứ đọc các file cũ đã xoá khỏi folder từ lâu rồi kìa, giờ tôi cần 1 cái changelog thôi, bạn tự review lại cái plan changelog trước đó ( không phải cái gemini viết ở ngay trên đâu nhé ) và đề xuất phương án cuối cùng cho tôi

=> thi thoảng Gemini ngáo :D

5. Tạo thêm 1 file testlog.md đi, rồi sau khi test mỗi bước thì ghi lại kết quả vào đấy, hợp lí không? với lại lấy cái input-sample đấy để test cũng được, quan trọng là nó phải chạy được đã. Bạn có đề xuất gì trước khi làm không?

=> Luôn cho AI đề xuất trước khi bắt đầu 1 bước nào đó, để tránh những trường hợp có những cách xử lí mà mình không biết/chưa nghĩ đến

# Giai đoạn 3 ( test - debug )

6. fix ngay BUG-1 cho tôi nhé, xong thì báo cáo rõ ràng lại giúp tôi là bạn đã fix như thế nào và vì sao lại fix như vậy

=> Câu này đơn giản nhưng lại là 1 trong những câu prompt quan trọng nhất đối với tôi trong quá trình debug, giúp không bị trôi hoặc không biết mình đang làm gì

7. chạy 3 batch lần lượt theo thứ tự, sau mỗi batch, dừng lại, ghi vào debug_log và báo cáo với tôi trước khi làm tiếp, khi nào tôi ra lệnh thì tiếp tục làm batch tiếp theo nhé, bạn đã nắm rõ chưa? Xác nhận trước khi làm

=> Lí do luôn yêu cầu chia nhỏ bước ra để thực hiện vì trải nghiệm thực tế những kết quả AI làm một nhiệm vụ dài thường hay lú, chia nhỏ task ra làm thì tỉ lệ 1 phát ăn ngay cao với những model thông minh như Opus 4.6.

8. [feedback của anh Lucas] Tạo 1 file feedback.md rồi đưa nội dung trên vào cho tôi, sau đó thêm file feedback.md này vào .gitignore, yêu cầu phản biện lại những gì chưa hợp lí và những gì đồng ý là phải sửa ngay, những gì có thể sửa sau. 

=> Opus gửi lại review. 

9. Đọc skill-card.md xem nó đã chuẩn định dạng skill card chưa? Có dài dòng quá không? Nếu chấm điểm thì được mấy điểm trên thang điểm 10?

10. Làm thế nào để lên thành 10/10 ? Hãy khắt khe và khó tính hơn xem nào

11. Nghiên cứu file SKILL để tìm kiếm các khả năng sinh ra lỗi ẩn, các khả năng chưa được đề cập đến, các trường hợp vẫn chưa được tính tới, rồi báo cáo lại cho tôi, đề xuất phương án tối ưu, tuyệt đối không tự động sửa lỗi.  (Codex 5.3)

=> Sau khi hỏi Opus kêu không còn lỗi ẩn nào thì tự nhiên đa nghi nghĩ không thể nào dễ dàng như thế được, gửi sang cho Codex dò lỗi, và đúng là Codex tìm ra được 1 vài lỗi ẩn thật. Qua session làm việc này mới lên nghiên cứu thì cộng đồng mạng đánh giá khá cao khả năng truy tìm và dò bug ẩn của Codex.

# Tổng kết
## Trên đây là 1 số prompt tiêu biểu trong quá trình làm việc với AI để xây dựng nên skill này, rút ra khá nhiều bài học cụ thể: 
- Làm việc với AI luôn phải rõ ràng, rành mạch, chỉ nên tập trung cụ thể vào 1 2 đầu việc, input xịn thì output mới xịn được

- Coi AI như 1 người cộng sự cùng nhau tư duy, tốc độ công việc có thể rút ngắn đến 10 lần so với làm thủ công

- Việc lựa chọn model nào làm tác vụ nào cũng là cực kì quan trọng, mỗi người sau khi đủ thời gian trải nghiệm sẽ có khẩu vị riêng để lựa chọn model phù hợp với công việc của mình. Cái này sau khi nói chuyện với bạn bè và đồng nghiệp thì nghiệm ra :D Ví dụ như mình cực thích dùng Perplexity cho 1 vài tác vụ còn nhiều ae thì k thích dùng lắm.

- Luôn bắt AI trình bày trước khi làm, sử dụng cùng 1 câu hỏi với các model khác nhau, bạn sẽ biết ngay phải dùng model nào, tránh trường hợp làm rồi lại sửa mất thời gian.

- Kĩ năng điều phối và quản lí thực sự quan trọng trong thời đại AI Agents, nếu không thể điều phối và quản lí tốt thì sẽ rất dễ bị AI nó dẫn dắt ngược lại, làm cho mất thời gian và không đạt được kết quả mong muốn. 

- Cần sử dụng đúng chỗ cho 2 việc : Gò AI vào những giới hạn được phép - Để khoảng trống cho nó sáng tạo.