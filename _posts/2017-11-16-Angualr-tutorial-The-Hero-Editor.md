# The Hero Editor

### 목차

- HeroesComponent 생성
- HeroesComponentFMF AppComponent shell에 추가(view에 추가)
- UppercasePipe
- two-way data binding - ngModel을 사용하여
- AppModule
- FormsModule를 추가하여 ngModel directive를 적용
- AppModule 선언의 중요성


## Create the heroes component

component를 직접 만들어 본다.

```
ng generate component heroes

```
새로운 HeroesComponent라는 폴더가 생긴다.

#### ../heroes.components.ts

- 클래스안에 hero = 'Windstorm' 추가



```
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-heroes',
  templateUrl: './heroes.component.html',
  styleUrls: ['./heroes.component.css']
})
export class HeroesComponent implements OnInit {

  hero = 'Windstorm'; // 추가한 부분
  constructor() { }

  ngOnInit() {
  }

}
```

#### heroes.component.html
- {{hero}}를 입력( data binding )

heroes component를 사용하기 위해 app.component.html selector를 추가

#### ../ app.component.html

```<app-heroes></app-heroes>``` 추가









## Create a Hero class
hero 클래스를 추가해보자

#### src/app/hero.ts

```
export class Hero {
  id: number;
  name: string;
}
```

HeroesComponent로 돌아와서 방금 만든 Hero클래스를 import

#### ../heroes.component.ts

```
import { Component, OnInit } from '@angular/core';
import { Hero } from '../hero';
```

그러면 Hero클래스를 다음과 같이 사용할 수 있다.

```
@Component({
  selector: 'app-heroes',
  templateUrl: './heroes.component.html',
  styleUrls: ['./heroes.component.css']
})
export class HeroesComponent implements OnInit {
  hero: Hero = {
    id: 1,
    name: 'Windstorm'
  };

  constructor() { }

  ngOnInit() {
  }

}
```
template에 적용시킨다.

#### ../heroes.componet.html

```
<h2>{{ hero.name }} Details</h2>
<div><span>id: </span>{{hero.id}}</div>
<div><span>name: </span>{{hero.name}}</div>

```

pipe를 이용할 수도 있다.

```
<h2>{{ hero.name | uppercase }} Details</h2>
```


## Edit the hero

### Two-way binding

input box를 이용하여 양방향 data binding를 할 수 있다.

양방향 data binding이란?<br>
클래스 에서 변경하는것 뿐만아니라 html에서 input box를 이용하여 클래스의 프로퍼티 값을 변경 할 수 있다.

#### ../heroes.component.html

```
<div>
    <label>name:
      <input [(ngModel)]="hero.name" placeholder="name">
    </label>
</div>
```

### The missing FormsModule
하지만 이는 오류가 나온다.

> Template parse errors:
> Can't bind to 'ngModel' since it isn't a known property of 'input'.

ngModel은 Angular의 directive인데 기본으로 이용할 수 없다. 그래서 모듈을 추가해주어야 한다.

#### ../app.module.ts

``` 
import { FormsModule } from '@angular/forms'; // <-- NgModel lives here 

imports: [
  BrowserModule,
  FormsModule
],

```

### Declare HeroesComponent
모든 component는 NgModule로 선언된다.

우리가 만든 HeroesComponent는

#### ../app.module.ts

```
import { HeroesComponent } from './heroes/heroes.component';

```

이렇게 추가되어 있고,

```
@NgModule({
  declarations: [
    AppComponent,
    HeroesComponent
  ],
  imports: [
    BrowserModule,
    FormsMo...
```
decalaations에 선언되어 있다.


