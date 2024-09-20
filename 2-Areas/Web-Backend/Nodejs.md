- Nodejs là môi trường giúp cho chúng ta có thể chạy các file javascript giống như là g++ của C++. Nó có thể thêm nhiều thư viện vào trong đó.
- Muốn sử dụng Nodejs thì cần cài node về máy và check bằng npm.
- Muốn sử dụng Nodejs thì bấm lệnh `node {file javascript muốn chạy}`
## Sử dụng `require('fs')` để đọc và ghi file trong hệ thống:
- `fs.readFile()` dùng để đọc với parameter đầu tiên là đường dẫn file trong hệ thống, tiếp theo là định dạng kiểu kí tự trong file. Nó có một version khác là `fs.readFileSync()` giúp cho việc đọc và ghi file sync không bị tranh chấp.
- `fs.writeFile()` dùng để ghi file với parameter đầu tiên là đường dẫn file trong hệ thống, tiếp theo là buffer (kí tự muốn ghi vào file) và cuối cùng là định dạng chữ của file. 
## Sử dụng `require('http')` để tạo một server:
- Ta cần khởi tạo một server bằng cách `const server = http.createServer((req, res) => {})` và 
`sever.listen('{port}', '{hostname}')`.
- Giải thích: server sẽ được tạo bằng lệnh createServer sau đó sẽ yêu cầu server listen trên ==port== và ==hostname== tương ứng. Sau đó server sẽ thực hiện lệnh trong function của createServer().
## Sử dụng `require('url')` để routing một server:
- Khi sử dụng routing ta sẽ cần có một biến để chứa URL hiện giờ của path đó như ví dụ: ![[Pasted image 20240920212323.png]]
- Sau đó ta sẽ kiểm tra đường link bằng *if else* thế nhưng trong phép so sánh thì trước tên đường dẫn phải có dấu ==/== .