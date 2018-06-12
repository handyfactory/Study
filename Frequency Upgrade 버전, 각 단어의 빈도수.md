# Frequency Upgrade 버전, 각 단어의 빈도수

문자에 있는 각 단어의 빈도수를 출력해야

---

text = "It was the best of times, it was the worst of times, it was the age of wisdom, it was the age of foolishness, it was the epoch of belief, it was the epoch of incredulity, it was the season of Light, it was the season of Darkness, it was the spring of hope, it was the winter of despair, we had everything before us, we had nothing before us, we were all going direct to Heaven, we were all going direct the other way--in short, the period was so far like the present period, that some of its noisiest authorities insisted on its being received, for good or for evil, in the superlative degree of comparison only.
"
count = 0

words = text.split(" ")

words.each do |word|
    word.downcase!
end

# arr = Array.new(10) #10개가 들어있는 어레이를 만들겠다 arr = []
# h = Hash.new("hello")
# h["banjang"]

# puts arr
# puts h

# puts h[6]

wf = Hash.new(0)
words.each do |w|
    wf[w] += 1
end

puts wf[w]