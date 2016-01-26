# Ruby-Coding-Convention
Source Code Layout

Mọi người đều nghĩ rằng tất cả style trừ của họ đều thật là khó đọc. Bỏ đi ba chữ ‘trừ  của họ’ và họ có lẽ đúng …

Encode các file của project bằng
```
UTF-8
```

- Sử dụng 2 dấu cách (soft tabs) cho mỗi thụt đầu dòng thay vì dùng tab thông thường (hard tabs – 4 spaces)
```
# bad - four spaces
def some_method
    do_something
end

# good
def some_method
  do_something
end
```

- Sử dụng Unix-style
```
 $ git config --global core.autocrlf true
```

- Không sử dụng ; để phân cách các câu lệnh. Mỗi câu lệnh viết thành một dòng không có dấu ;
- Không viết các function một dòng
```
# bad
  def too_much; something; something_else; end
# good
  def some_method
    body
  end
```
- Có dấu cách trước va sau các phép toán, sau dấu , trước và sau { và truớc }. Ngoại trừ toán tử lũy thừa **
```
sum = 1 + 2
a, b = 1, 2
1 == 2 ? true : false; puts 'Hi'
[1, 2, 3].each { |e| puts e }
e = M * c**2
```
- Không có dấu cách sau ( và [ hay trước ], )
```
some(arg).other
[1, 2, 3].size

```
- Không có dấu cách sau !
```
# good
!something
```
- Trong lệnh when ... case, when cần được thụt dòng ngang với case. Có thể một số người không đồng tình với quan điểm này, nhưng đó cũng là style trong 2 cuốn sách ‘The Ruby Programming Language’ và ‘Programming Ruby’
```
 # bad
  case
    when song.name == 'Misty'
      puts 'Not again!'
    when song.duration == 120
      puts 'Too long!'
    when Time.now.hour == 21
      puts "It's too late"
    else
      song.play
  end

  # good
  case
  when song.name == 'Misty'
    puts 'Not again!'
  when song.duration == 120
    puts 'Too long!'
  when Time.now.hour == 21
    puts "It's too late"
  else
    song.play
  end
```

- Khi gán biến theo một câu lệnh if ... else ... end hay case ... when ... else ... end, hãy chú ý để các nhánh được thẳng
```
# bad - pretty convoluted
kind = case year
when 1850..1889 then 'Blues'
when 1890..1909 then 'Ragtime'
when 1910..1929 then 'New Orleans Jazz'
when 1930..1939 then 'Swing'
when 1940..1950 then 'Bebop'
else 'Jazz'
end

result = if some_cond
  calc_something
else
  calc_something_else
end

# good - it's apparent what's going on
kind = case year
       when 1850..1889 then 'Blues'
       when 1890..1909 then 'Ragtime'
       when 1910..1929 then 'New Orleans Jazz'
       when 1930..1939 then 'Swing'
       when 1940..1950 then 'Bebop'
       else 'Jazz'
       end

result = if some_cond
           calc_something
         else
           calc_something_else
         end
```
- Tránh sử dụng kí tự xuống dòng trong Ruby \ nếu không cần thiết, ngoại trừ nối các string
- Khi các hàm được gọi nối tiếp, hãy đặt dấu . ở dòng thứ 2
```
       # bad - K hiểu đc dòng thứ 2
one.two.three.
  four

# good - chúng ta thấy rõ ràng dòng thứ 2 được gọi từ dòng trên
one.two.three
  .four
```
- Đối với những hàm mà tham biến của nó quá nhiều, chúng ta nên xuống dòng từng tham biến theo một trong hai cách sau
```
 # good
  def send_mail(source)
    Mailer.deliver(to: 'bob@example.com',
                   from: 'us@example.com',
                   subject: 'Important message',
                   body: source.text)
  end

  # good (normal indent)
  def send_mail(source)
    Mailer.deliver(
      to: 'bob@example.com',
      from: 'us@example.com',
      subject: 'Important message',
      body: source.text
    )
  end
```

- Dóng thẳng các phần tử khi khai báo mảng nếu mảng quá nhiều. Ví dụ như sau:
```
# bad - single indent
menu_item = ["Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam",
  "Baked beans", "Spam", "Spam", "Spam", "Spam", "Spam"]

# good
menu_item = [
  "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam",
  "Baked beans", "Spam", "Spam", "Spam", "Spam", "Spam"
]
```

- Thêm gạch dưới đối với những số lớn để dễ đọc
```
# bad - how many 0s are there?
num = 1000000

# good - much easier to parse for the human brain
num = 1_000_000
```

- Mỗi dòng chỉ nên tối đa 80 kí tự
Không sử dụng dấu cách ở cuối dòng lệnh
Không sử dụng kiểu comment cả một block. Kiểu comment này không đặt được dấu cách trước nó và khó nhận ra đó là những comment như bình thường
```
# bad
== begin
comment line
another comment line
== end

# good
# comment line
# another comment line
```
###Syntax

- Khi định nghĩa function, nếu có tham biến truyền, sử dụng các dấu (). Nếu không có tham biến, bạn không nên có nó
```
   # bad
   def some_method()
     # body omitted
   end

   # good
   def some_method
     # body omitted
   end

   # bad
   def some_method_with_arguments arg1, arg2
     # body omitted
   end

   # good
   def some_method_with_arguments(arg1, arg2)
     # body omitted
   end
```
- Sử dụng ?: thay vì dùng if/then/else/end nếu điều kiện đơn giản. Nhưng nếu có 2 câu lệnh lồng nhau, thì nên đan xen 2 kiểu đó như ví dụ ở dưới
```
 # bad
  result = if some_condition then something else something_else end

  # good
  result = some_condition ? something : something_else

 # bad
  some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

  # good
  if some_condition
    nested_condition ? nested_something : nested_something_else
  else
    something_else
  end
```
- Sử dụng ! thay cho not, && thay cho and, || thay cho or
Không nên sử dụng if/unless .. end, while/until ... end nếu statement chỉ có một dòng. Ví dụ
```
 # bad
  if some_condition
    do_something
  end

  # good
  do_something if some_condition
 # bad
  while some_condition
    do_something
  end

  # good
  do_something while some_condition
```
- Sử dụng unless thay cho if not
Không sử dụng unless ... else ... end. Hãy viết lại thành câu lệnh if ... else ... end
Hạn chế sử dụng () trong câu lệnh if/unless/while/until
```
 # bad
if (x &gt; 10)
  # body omitted
end

# good
if x &gt; 10
  # body omitted
end
```
- sử dụng until thay cho while với câu lệnh dạng phủ định
```
# bad
do_something while !some_condition

# good
do_something until some_condition
```
- Bỏ các dấu {} ngoài cùng của hash
```
# bad
user.set({ name: 'John', age: 45, permissions: { read: true } })

# good
user.set(name: 'John', age: 45, permissions: { read: true })
```
- Khi gọi method không có arguments đi dùng, hãy bỏ các dấu ngoặc
```
# bad
Kernel.exit!()
2.even?()
fork()
'test'.upcase()

# good
Kernel.exit!
2.even?
fork
'test'.upcase
```
- Đối với những đoạn code chỉ đơn giản, chỉ gồm 1 dòng, hãy sử dụng {...} do ... end
```
  # bad
  names.each do |name|
    puts name
  end

  # good
  names.each { |name| puts name }
```
- Không phải lúc nào cũng cần sử dụng return. Hạn chế sử dụng nếu flow của source code không cần thiết nó
```
# bad
def some_method(some_arr)
  return some_arr.size
end

# good
def some_method(some_arr)
  some_arr.size
end
```
- Tránh sử dụng self nếu không cần thiết. Nó chỉ cần sử dụng nếu bạn muốn ghi dữ liệu
```
# bad
def ready?
  if self.last_reviewed_at &gt; self.last_updated_at
    self.worker.update(self.content, self.options)
    self.status = :in_progress
  end
  self.status == :verified
end

# good
def ready?
  if last_reviewed_at &gt; last_updated_at
    worker.update(content, options)
    self.status = :in_progress
  end
  status == :verified
end
```
- Không gán biến trong câu lệnh if ... else ... end
```
# bad (+ a warning)
  if v = array.grep(/foo/)
    do_something(v)
    ...
  end

  # good
  v = array.grep(/foo/)
  if v
    do_something(v)
    ...
  end
```
- Khai báo biến bẳng kí hiệu ||=. Tuy nhiên, không gán theo cách này với biến boolean
```
# gán giá trị  Bozhidar cho biến name nếu biến này là nil hay false
name ||= 'Bozhidar'

# bad
enabled ||= true

# good
enabled = true if enabled.nil?
```

- Sử dụng &&= để xử lý biến nếu cần điều kiện khi biến tồn tại. Việc sử dụng kí tự này sẽ không cần kiểm tra xem biến có tồn tại hay k
```
# bad
if something
  something = something.downcase
end

# good
something &amp;&amp;= something.downcase
```
- Không được có dấu cách sau tên hàm và trước dấu (
```
# bad
f (3 + 2) + 1

# good
f(3 + 2) + 1
```
- Sử dụng -w để trình biên dịch Ruby nhắc bạn nếu bạn quên đi những qui tắc ở trên
Các sử dụng lambda
```
# good
  l = -&gt;(a, b) { a + b }
  l.call(1, 2)

  l = lambda do |a, b|
    tmp = a * 7
    tmp * b / 50
  end
```
- Sử dụng proc thay cho Proc.new, proc.call() thay cho proc[] hay proc.()
Sử dụng kí tự _ đối với những biến không sử dụng trong block
```
# bad
result = hash.map { |k, v| v + 1 }

# good
result = hash.map { |_, v| v + 1 }
```
- Sử dụng between hoặc include thay vì sử kiểm tra toán tử login thông thường
```
# bad
do_something if x &gt;= 1000 &amp;&amp; x &lt;= 2000

# good
do_something if (1000..2000).include?(x)

# good
do_something if x.between?(1000, 2000)
```
- Sử dung những phương thức đã được Ruby định nghĩa sẵn thay vì sử dụng ==
```
  # bad
  if x % 2 == 0
  end

  if x % 2 == 1
  end

  if x == nil
  end

  # good
  if x.even?
  end

  if x.odd?
  end

  if x.nil?
  end

  if x.zero?
  end

  if x == 0
  end
```
- Hạn chế sử dụng các câu lệnh điều kiện lồng nhau. Việc đó làm cho login của source code rất khó theo dõi. Thay vào đó, bạn có thể sử dụng return khi có thể để giảm số lớp câu điều kiện
```
# bad
    def compute_thing(thing)
      if thing[:foo]
        update_with_bar(thing)
        if thing[:foo][:bar]
          partial_compute(thing)
        else
          re_compute(thing)
        end
      end
    end

  # good
    def compute_thing(thing)
      return unless thing[:foo]
      update_with_bar(thing[:foo])
      return re_compute(thing) unless thing[:foo][:bar]
      partial_compute(thing)
    end
```
