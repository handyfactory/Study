# Hashes and Symbols

- 해시는 key 와 value 의 조합이다
- key는 특별해야 하지만 value는 반복될 수 있다
- 과일바구니를 예로 들면 바나나, 사과가 동시에 맛있을 수 있다
- 바나나, 사과는 key
- 맛있다는 value
- 해시를 주로 만드는 방법은 두 가지
  - ㅇㄹ
- key는 유니크 해야 함, 그래서 심볼을 주로 사용함



---

### Symbols

- 메모리에 저장된 자료는 컴퓨터가 꺼지면 사라짐
- 자료는 메모리의 특정한 공간에 저장이 됨
- "hello".object_id 를 irb에 치면 주소가 나온다
- 또 다른 "hello".object_id를 치면 또 다른 주소가 나온다
- 그런데 변수를 지정하면 한 공간을 차지할 수 있다. greeting = "hello" 처럼
- :john 은 심볼을 표시하는 방법
- :john.object_id 계속 치면 같은 주소가 나옴. 해당 구역 할당받음
- :john.to_s 하면 String 으로 바뀜
- "john".to_sym 하면 Symbol로 바뀜
- Symbol.all_symbols.last(10) 를 치면 관리하고 있는 모든 심볼이 나와
- 심볼은 고유하고 변경이 불가능하다



---

### Class

- 세상에 있는 모든 물체는 object 다. S + V
- 세상에 있는 모든 물체는 분류 가능하다.
- 세상에 있는 모든 물체는 계층 구조를 갖고 있다.

```ruby
dh ={"name"=>"dh","age" => "27", "gender" => "male"}
hs = {:name => "hs", :age => "27", :gender => "male"}
yr = {name: "yr", age: "27", gender: "female"} 
# yr = {:name => "yerim", :age => "27", :gender => "female"}
#자동으로 내부에서 바꿔줌

puts dh["name"]
puts hs[:name]
puts yr[:name]
```

---

# Hash practice

```ruby
matz = { "First name" => "Yukihiro",
  "Last name" => "Matsumoto",
  "Age" => 47,
  "Nationality" => "Japanese",
  "Nickname" => "Matz"
}

matz.each do |key, value|
  puts key
end

```

- puts key 하면 key 가 주르륵 나온다
- puts value 하면 value 가 주르륵 나온다

---

# Symbol

- 심볼은 이름의 종류
- 심볼은 String이 아니다
- String은 같은 값이라도 할당되는 메모리의 위치는 다른데
- 심볼은 같은 값이면 할당되는 메모리 위치 같다!

```ruby
puts "string".object_id
puts "string".object_id

puts :symbol.object_id
puts :symbol.object_id

7914600
7914340
802268
802268
```

- 심볼을 만들 땐 공백을 두지 마라

