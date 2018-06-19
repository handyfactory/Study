# Ordering your library

- Sort : 순서대로 있는 것 처럼 보이지만 페이크
- Sort! : 제대로 순서대로 나열하기

```ruby
numbers = [45,2,4,798,3]

def alphabetize(arr,rev=false)
  return arr.sort!
end

puts alphabetize(numbers)
```

