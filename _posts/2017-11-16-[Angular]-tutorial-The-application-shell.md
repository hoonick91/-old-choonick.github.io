# 소개
# application shell

Angular CLI를 설치한다.
```npm install -g @angular/cli```

new Application을 생성한다.
```ng new angular-tour-of-heroes
```
여기서 이름은 angular-tour-of-heroes 이다.

angular-tour-of-heroe 경로로 들어가서
application을 실행시킨다.
```
cd angular-tour-of-heroes
ng serve --open
```

shellㅣ은 컴포넌트에 의해 조종된다.

app.component.ts	에서 title 프로퍼티를 바꿀 수있다.
이는 appcomponent.html의

```
<h1>
    Welcome to {{title}}!
</h1>
```
의 {{title}} 부분과 연결되어 있다.

## component
app.component.ts

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'tour of heroes';
}

```

### selector : 'app-root'
이 부분은 컴포넌트의 이름이다.
<app-root></app-root>형태로 사용할 수 있다.

index.html

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>AngularTourOfHeroes</title>
  <base href="/">

  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
<body>
  <app-root></app-root>
</body>
</html>
```

### templateUrl: './app.component.html',
component가 바라보는 template의 경로를 나타낸다.

마찬가지로
styleUrls: ['./app.component.css']
template가 바라보는 css를 나타낸다.

### export class AppComponent {
  title = 'tour of heroes';
}

export는 어디서나 import할 수 있다는 것이다.



