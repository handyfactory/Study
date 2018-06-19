# Render와 Redirect의 차이점

- 때때로, `redirect_to`를 일종의 `goto` 명령어와 같은 것이라고 이해하고 있는 초급 개발자들을 볼 수 있습니다. Rails 코드의 실행위치를 어떤 장소에서 다른 장소로 옮기는 명령이라고 생각하고 있다는 것인데, 이것은 *올바르지 않은* 생각입니다. `redirect_to`를 실행한 뒤, 코드는 거기서 종료되며, 브라우저에게서 다른 요청을 기다립니다(평소의 요청 대기 상태). 그 직후에 `redirect_to`로 브라우저에 전송된 HTTP 상태 코드 302에 따라서, 다른 URL 요청이 서버로 전송되고 서버는 이 요청을 처리합니다. 그 이외의 처리는 하지 않습니다. 

```ruby
def index
  @books = Book.all
end
 
def show
  @book = Book.find_by(id: params[:id])
  if @book.nil?
    render action: "index"
  end
end
```

- 위의 코드에서는 `@book` 인스턴스 변수가 `nil`일 경우에 문제가 발생할 가능성이 있습니다. `render :action`은 대상이 되는 액션의 코드를 실행하지 않는다는 점을 상기해주세요. 따라서 `index` 뷰에서 필요로 할 `@books` 인스턴스 변수에는 아무것도 설정되지 않고, 아무 것도 없는 서적 목록이 표시되게 됩니다. 이것을 해결하는 방법 중 하나는 render를 redirect로 변경하는 것입니다. 

```ruby

def index
  @books = Book.all
end
 
def show
  @book = Book.find_by(id: params[:id])
  if @book.nil?
    redirect_to action: :index
  end
end
```

- 이 코드라면, 브라우저에서 index 페이지를 달라는 요청이 새로 전송되기 때문에 `index` 액션의 코드가 정상적으로 실행됩니다.

  이 코드에서 한가지 아쉬운 점이 있다면, 브라우저와의 통신을 한번 더 해야한다는 점입니다. 브라우저의 `/books/1` 요청에 대해서 show 액션이 호출되고 책이 하나도 없다는 것을 확인한 뒤, 컨트롤러는 브라우저에 대해서 `/books/`를 요청하라는 상태 코드 302(리다이렉트)를 돌려줍니다. 브라우저는 이 지시를 받고, 이 컨트롤러의 `index` 액션을 호출하기 위한 요청을 전송합니다. 그러면 컨트롤러는 이 요청을 받아서 데이터베이스에 존재하는 모든 서적 목록을 가져온 뒤 index 템플릿을 랜더링하여 결과를 브라우저에게 전송하고, 브라우저는 서적 목록을 보여주게 됩니다.

  이 반복된 통신에 의한 지연은 소규모 애플리케이션이라면 별 문제가 없습니다만, 지연이 문제가 되기 시작하게 되면 이 부분을 고쳐야할 필요가 있을 수도 있습니다. 브라우저와의 통신 횟수를 늘리지 않기 위해 개선한 예제는 아래와 같습니다.

```ruby
def index
  @books = Book.all
end
 
def show
  @book = Book.find_by(id: params[:id])
  if @book.nil?
    @books = Book.all
    flash.now[:alert] = "Your book was not found"
    render "index"
  end
end
```

- 이 코드의 동작은 다음과 같습니다. 지정된 id를 가지는 책이 발견되지 않은 경우에는, 모델에 있는 모든 서적 목록을 `@books` 인스턴스 변수에 보존합니다. 이어서 flash를 이용해 경고 메시지를 추가하고, 마지막으로 `index.html.erb` 템플릿을 랜더링하도록 지시합니다. 

