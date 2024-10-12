
## GRID Container:
	![[Screenshot 2024-10-12 at 09.50.56.png]]
## GRID Items:
	![[Screenshot 2024-10-12 at 09.53.09.png]]
## Đơn vị độ dài của GRID:
- ==Fr==: một fr nghĩa là nó sẽ chiếm bao nhiêu phần bị dư ra của container làm GRID.
> [!NOTE] Lưu ý: đơn vị fr này không giống bên flexbox nếu ==grid-template-columns: 2fr 1fr== nghĩa là sẽ có 3 collumns thế nhưng collumns đầu tiên sẽ lấy 2 phần trong 3 collumn mà grid tạo ra và độ dài nó sẽ gấp đôi collumn có độ dài bằng 1fr.
```
Có một function để giúp viết các độ dài một cách dễ hơn là: repeat({số lượng hàng/cột}, {chiều dài}).
```