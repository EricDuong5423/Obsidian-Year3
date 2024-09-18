## Web caches:
- **Web caches** là nơi lưu trữ những truy cập của người dùng. Khi người dùng khác cần thì lấy ra luôn không cần phải gọi ra sever để tạo kết nối với sever.
- Nếu nhiều người dùng thì như thế nào ?
- Thì sẽ tạo ra một cache sever (proxy server) giúp cho việc gọi trang web thêm một lần nữa nếu người dùng khác cần gọi thì sẽ lấy từ caches ra đưa.
 - Lợi ích:
	+ Giảm thời gian phản hồi với yêu cầu của end-users.
	+ Giảm jam traffic trên các server.
- Nếu không có server cache thì phải làm gì 
	 - Ví dụ:![[Pasted image 20240917162136.png]]
	 - Giải quyết bằng cách tăng đường truyền lên 100 lần:![[Pasted image 20240917162234.png]]
		*Thế nhưng sẽ rất là mắc vì tăng tốc độ đường truyền lên sẽ đồng nghĩa tăng sức mạnh của các phần cứng lên*
	- Giải quyết bằng cài đặt web cache:![[Pasted image 20240917162420.png]]
		*Với việc cài đặt web cache sẽ tăng hiệu quả hơn cả việc tăng 100 lần tốc độ của đường truyền và còn rẻ*
## Conditional GET:
- Nếu như không có gì thay đổi từ máy chủ thì không cần phải tạo lại trang web từ phản hồi của người dùng.
- ![[Pasted image 20240917162739.png]]
	 *Như ta thấy ở đây, khi client yêu cầu lại tài nguyên web thì sẽ check thử xem trên server có thay đổi gì trên trang web không, nếu không thì sẽ lấy từ caches để đưa lại cho client cho đỡ tốn tài nguyên và thời gian*
## HTTP 2.0
### Điểm bất lợi của HTTP 1.
- Thứ tự FCFS sẽ khiến cho gặp vấn đề nếu yêu cầu trước đó nhiều quá sẽ block luôn các yêu cầu nhỏ hơn ở sau sẽ starving.
	 ![[Pasted image 20240917163448.png]]
		*Như ở hình trên dữ liệu của yêu cầu O1 nó đã chiếm hết tất cả thời gian khiến cho các O2, O3, O4*
### Giải pháp của HTTP 2
- Sử dụng cơ chế như round robin để chia các dữ liệu trả về thành từng frames nhỏ
	![[Pasted image 20240917163711.png]]
		*Như ở đây thì tất cả các dữ liệu sẽ được gửi tuần tự*
## HTTP 3.0
### Điểm bất lợi của HTTP2:
- Việc recovery các packet loss vẫn sẽ khiến cho hệ thống sẽ bị starving.
- Không có bảo mật cho kết nối TCP
### Giải pháp của HTTP 3:
- Bỏ qua các luôn việc các packet loss và thêm vào các lớp bảo mật
## E-mail:
### Ba thành phần chính của e-mail:
- User agents (UAs):
	- "mail reader"
	- Làm công việc "tổng hợp, chỉnh sửa, đọc mail".
	- Ví dụ: Outlook, Gmail.
	- Tin nhắn gửi và tới sẽ được lưu trong đây.
- Mail servers (MAs):
	- Chứa các tin nhắn gửi tới
	- ==message queue== là nơi chứa hàng đợi các mail sẽ được gửi.
- Simple mail transfer protocol (SMTP): giữa mail servers để gửi các mail
	- ==client==: gửi mail đến server
	- =="server"==: nhận mail đến serverserver
		![[Pasted image 20240917164408.png]]
- RFC (request for comments):
	- Sử dụng TCP: SMTP sử dụng giao thức TCP để đảm bảo việc truyền email từ máy chủ gửi đến máy chủ nhận qua cổng 25.
	- Chuyển tiếp trực tiếp: Máy chủ gửi email (như là một client) kết nối và truyền email trực tiếp tới máy chủ nhận.
	- Ba giai đoạn chuyển giao:
		1. **Bắt tay (handshaking)**: Hai máy chủ giao tiếp để thiết lập kết nối.
		2. **Chuyển mail**: Truyền tải các thông điệp email
		3. **Đóng kết nối**: Kết thúc quá trình giao tiếp
	- **Tương tác lệnh/ phản hồi**: Giao thức hoạt động dựa trên việc gửi lệnh (dưới dạng văn bản ASCII) và nhận phản hồi (mã trạng thái và câu trả lời), tương tự như HTTP
	- **Email phải dùng định dạng 7-bit ASCII**: Nội dung email cần tuân theo tiêu chuẩn 7-bit ASCII
- Ví dụ về gửi mail:![[Pasted image 20240917214404.png]]
	 *Ở đây ta có thể thấy là người dùng Alice gửi cho người dùng Bob một email. Email đó phải đi qua con đường: User agent -> SMTP của mail server -> kết nối TCP đến server mail của Bob -> Bob đọc được email của Alice*
- **So sánh với HTTP**:
	- HTTP là giao thức pull (lấy dữ liệu theo yêu cầu), còn SMTP là push (gửi dữ liệu từ client đến server)
	- Cả HTTP và SMTP đều có tương tác lệnh/phản hồi qua ASCII và sử dụng mã trạng thái.
	- **HTTP**: Mỗi đối tượng được đóng gói trong thông điệp phản hồi riêng lẻ.
	- **SMTP**: Nhiều đối tượng được gửi trong một thông điệp dạng multipart.
- **SMTP** sử dụng kết nối lâu dài (persistent connections).
- **SMTP** yêu cầu thông điệp (phần header và body) phải ở định dạng 7-bit ASCII.
- **SMTP server** sử dụng cặp ký tự **CRLF.CRLF** để xác định kết thúc của thông điệp.
- Format của mail:![[Pasted image 20240917222032.png]]
## DNS: Domain Name System:
- **Định danh của host và router trên Internet**:
	- **Địa chỉ IP** (32-bit): Dùng để định địa chỉ gói dữ liệu.
	- **Tên miền** (ví dụ: hcmut.edu.vn): Được sử dụng bởi con người.
- **Hệ thống DNS**:
	- **Cơ sở dữ liệu phân tán**: Được triển khai theo dạng phân cấp của nhiều máy chủ tên (name servers).
	- **Giao thức tầng ứng dụng**: Các máy chủ và hosts giao tiếp để giải quyết tên miền (dịch tên miền sang địa chỉ IP và ngược lại).
	- **Chức năng cốt lõi của Internet**: DNS là một phần của tầng của ứng dụng, giúp Internet hoạt động.
	- **Độ phức tạp**: Được tập trung tại rìa của mạng.
## Streaming multimedia: DASH
- **DASH**: Dynamic Adaptive Straming trên HTTP
- Ở hướng server:
	- Chia files video thành các *chunks*
	- Mỗi *chunk* chứa các dữ liệu và được encode với tốc độ khác nhau 
	- **MANIFEST FILE**: cung cấp URLs cho các chunk khác nhau
		![[Pasted image 20240918071451.png]]
- Ở hướng client:
	- Thường xuyên đo băng thông từ server-client.
	- Yêu cầu mỗi chunk mỗi lần.
		- Chọn tốc độ băng thông tối đa mà nó ổn định nhất có thể.
		- Có thể cho phép chọn tốc độ băng thông khác nhau (nếu có thể trong khả năng băng thông hiện tại)
- Mọi việc xử lý "thông minh" đều được xử lý ở client, thế nên client sẽ quyết định:
	- **==Khi nào==** yêu cầu một chunk (để tránh tình trang starving và overflow)
	- **==Bao nhiêu==** tốc độ encoding khi yêu cầu (cao nhất có thể).
	- **==Chỗ nào==** để yêu cầu chunk (có thể yêu cầu từ URL server mà *đóng* với client hoặc có băng thông cao)
- $=>$ ==Streaming video = encoding + DASH + playout buffering==
## CDNs (Content distribution networks):
- Ví dụ: Nếu muốn ==stream== một nội dung từ hàng ngàn hàng triệu người dùng ==liên tục== thì nó sẽ như nào ?
- Cách giải quyết 1: tạo một server cực lớn.
	- *Thế nhưng sẽ tốn rất rất nhiều tiền và không có hiệu quả kinh tế*
- Cách giải quyết 2: Lưu trữ và phục vụ các nội dung ==stream== ở các khu vực địa lý khác nhau (CDNs)
- ==CDN==: sẽ lưu trữ các copy của nội dung và ở các CDN nodes
- ==Người dùng==: sẽ yêu cầu nội dung từ CDN.
	- Có thể lấy trực tiếp từ nguồn có copy của nội dung đó gần nhất.
	- Nếu không được thì sẽ đi tìm một node của CDN khác.
	![[Pasted image 20240918073520.png]]
## IPTV:
- Tương tự như thế bên CDNs thì truyền hình cáp cũng hoạt động tương tự như thế. 
	- ![[Pasted image 20240918073711.png]]
		*Đối với IPTV thì sẽ nếu local distribution center nào có đống tiền thì sẽ được bộ giải mã của bên nhà đài để mã hóa thông tin được push từ các ==CDN== của đài truyền hình, nếu không có thì những tin hiệu đó vẫn đi qua mà không coi được thôi*
## Cái nhìn tổng quát hơn về trường hợp CDNs của NetFlix:
		![[Pasted image 20240918074124.png]]
1. Đầu tiên Bob sẽ đi tìm film và yêu cầu video từ account của mình.
2. Khi tìm xong Bob sẽ yêu cầu cho ==Manifest files==
3. ==Manifest files== sẽ gửi những bản copy cho các CDNs.
4. Ở CDNs gần Bob nhất (hoặc có băng thông cao nhất) sẽ truyền một bản copy của nội dung video mà Bob đã yêu cầu từ *Dash server* sau khi nó đã chọn và liên lạc tới máy client.
## Lập trình socket với UDP và TCP:
- Socket là  