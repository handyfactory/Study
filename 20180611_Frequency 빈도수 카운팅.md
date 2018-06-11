# Frequency 빈도수 카운팅

글 안에 있는 특정 단어를 카운팅 합니다.

---

text = "It was the best of times, it was the worst of times, it was the age of wisdom, it was the age of foolishness, it was the epoch of belief, it was the epoch of incredulity, it was the season of Light, it was the season of Darkness, it was the spring of hope, it was the winter of despair, we had everything before us, we had nothing before us, we were all going direct to Heaven, we were all going direct the other way--in short, the period was so far like the present period, that some of its noisiest authorities insisted on its being received, for good or for evil, in the superlative degree of comparison only.
"
count = 0

words = text.split(" ")

words.each do |word|
    word.downcase!

    if word == "it"
        count += 1
    end

end

puts count

---

- count++ 가 적용 안되는 듯
- split 이란 method로 쪼개준다, " " 공간을 중심으로
- |word| 처럼 명확한 단어로 하는 습관