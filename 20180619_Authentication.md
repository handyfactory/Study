#  Authentication

- Email과 Password를 입력했을 때
- DB에 있는 사람인지 파악
- DB에 있다면 Password 비교 해서 로그인
- 없다면 다시 시도 및 쫓아내기

---

# HTTP

- Stateless
- Hyper Text Transfer Protocol
- 로그인 과정에 sinatra의 session 이용
- HTTP는 기본적으로 무상태이기 때문에 저장 기능이 없음
- 쿠키 이용
- 정보를 저장 못하니깐 서버는 얘 컴퓨터에 '오레오'를 심어요
- 다음 요청이 들어올때부터 '오레오'를 같이 보내
- 서버는 쿠키를 보고 인증!
- 고객 2가 로그인 성공
- 서버는 또 고객2에게 '오레오'를 넣어줘
- 근데 고객 3은 쿠키를 발급 못받았어 고객 2에게 있는 쿠키를 갖고와
- 이를 써서 로그인 가능. 해킹 가능.
- 쿠키를 점점 로그인에 안쓰기 시작
- 검색기록은 남아. 쿠키로.
- 구글이나 네이버는 고객들의 쿠키 다 수집
- GDPR 이라고 규약이 바뀌었어. 그래서 최근 외국사이트에서 메일이 많이 왔을 것

---

# Sinatra Session

- 

```ruby
get '/login_session' do

   @users = User.all
   #로그인에서 날아온 정보로 DB의 정보와 비교하는 로직
   @msg = "로그인 실패 DB에 없음"
   @users.each do |u|
      if u.email == params[:email] && u.password == params[:password]
              @msg = "로그인 성공"
      end

   end
  erb :login_session
end
```

```ruby
get '/login_session' do

   @users = User.all
   #로그인에서 날아온 정보로 DB의 정보와 비교하는 로직
   @msg = "로그인 실패 DB에 없음"
   @users.each do |u|
      if u.email == params[:email] && u.password == params[:password]
          @msg = "로그인 성공"
          session[:email] = u.email #session 사용하겠다
      end

   end
  erb :login_session
end
```

