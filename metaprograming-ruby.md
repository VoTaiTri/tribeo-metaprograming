# Introduction
- Link book : [Metaprgraming Ruby pdf book](http://www.mediafire.com/view/zkkznnr1sy9n8on/the_ruby_programming_language.pdf)

- Một số thứ có thể làm với **metaprogramming** trong Ruby.
    - Khi viết 1 chương trình **Ruby** kết nối tới 1 `hệ thống bên ngoài`(có thể là `web service` hoặc 1 `chương trình Java`)
      - có thể viết 1 `wrapper` lấy bất kỳ `method` nào và `routes` nó đến `hệ thống bên ngoài`
      - nếu `hệ thống bên ngoài` được thêm các method sau đó, `Ruby wrapper` của bạn sẽ ko phải thay đổi mà `wrapper` sẽ hỗ trợ các method mới đó ngay vào **App** của bạn

    - Có thể loại bỏ trùng lặp code mà Java khó có thể làm được `=>` định nghĩa cho các method giống nhau

    - Có thể chỉ dùng **Ruby** để `uốn` cú pháp cho đến khi gần giống 1 ngôn ngữ cụ thể nào đó cho vấn đề của bạn

    - .v.v..

#### *M* Word
Có một số định nghĩa cần nhớ trong **Metaprograming**
##### - `Metaprogramming is writing code that writes code`
  - => dùng code để sinh ra code

##### - `Với Ruby, runtime giống như 1 busy marketplace`
  - `=>` hầu hết các cấu trúc ngôn ngữ vẫn còn sau khi biên dịch xong `job` (không giống như C++)

##### - `Metaprogramming is writing code that manipulates language constructs at runtime`
  - Không viết các `method` `accessor` cho từng thuộc tính của `class`
  - Viết code định nghĩa các `method` trong thời gian chạy cho bất kỳ `class` nào kế thừa `ActiveRecord::Base`

***

# Phần 1 Metaprogramming Ruby

## Chương 1. The object model

##### - `all these constructs live together in a system called the object model`
  - `object model` là nơi bạn có thể tìm thấy câu trả lời cho câu hỏi "những method này đến từ đâu?"và "chuyện gì sẽ xảy ra nếu như tôi *include* module này?"

###Inside Class Definitions

- Ruby ko thực sự phân biệt giữa `code` định nghĩa 1 `class` và `code` của bất kỳ loại nào khác
  - có thể `code` tùy ý trong định nghĩa `class`.

- Ruby thực thi `code` trong `class` giống như là bất kỳ `code` khác.
- vd1:

```ruby
  3.times do
    class C
      puts "Hello"
    end
  end
```

=> `Không phải định nghĩa 3 class với tên giống nhau`

- vd2: định nghĩa 2 `class` cùng tên sau

```ruby
class D                                 class D
  def x; `x` ; end                        def y; `y`; end
end                                     end
```
```
obj = D.new
obj.x # => "x"
obj.y # => "y"
```

=> khi `mention` đến `class D` lần đầu tiên thì chưa có `class` với tên `D` tồn tại lúc này => Ruby cần định nghĩa class với method `x`

=> Lần thứ 2 `mention` `D` thì `class` này đã tồn tại => Ruby ko cần định nghĩa lại mà chỉ cần mở lại class đã tồn tại và định nghĩa thêm method mới `y`

- Trong cảm nhận, class trong Ruby gần giống với toán tử `scope` hơn là `declaration class`


- kỹ thuật `Open Class` => luôn có thể mở lại các `class` hiện có (thậm chí là các thư viện chuẩn như `String`, `Array`...) và chỉnh sửa nó `on the fly`

=> Bạn có định nghĩa 1 `class` mới trùng tên với các `class` sẵn có.

```ruby
class MyClass
  def my_method
    @v = 1
  end
end


obj = MyClass.new
obj.class # => MyClass
```

#### 1. Instance variables

- `objects` chứa `instance variables`
  - `Object#instance_variables()`

```ruby
obj.instance_variables() # => [:@v]
```

- Có thể hiểu `tên` và `giá trị` của `instance variables` giống như là `key` và `value` của 1 `HASH`.

=> cả `tên` và `giá trị` có thể khác nhau với mỗi `object`

#### 2. Methods