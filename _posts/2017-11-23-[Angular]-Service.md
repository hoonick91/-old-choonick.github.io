# Service
## 1. 왜 service 인가
컴포넌트는 직접적으로 데이터를 저장할 수 없으므로 어디서나 저장하고 불러올 수 있는 서비스를 만들어 데이터를 관리한다.
### 2. service를 생성한다.
```
ng generate service hero --module=app

```
그리고 생성한 파일에 다음을 추가한다.
#### ../hero.service.ts
```
import { Injectable } from '@angular/core';
import { Hero } from './hero';
import { HEROES } from './mock-heroes';


@Injectable()
export class HeroService {

  getHeroes(): Hero[] {
    return HEROES;
  }

  constructor() { }

}

```

### 3. provider에 service를 추가 


```
ng generate service hero --module=app

```
이미 파일을 만들었다면 다음과 같이 수기로 추가해준다.

#### ../src/app/app.module.ts (providers)

```
providers: [ HeroService ],

```
여기에 추가함으로써 다른 클래스가 요청하면 inject할 수 있게 된다.
그렇게 되면 이전에 만든 mock-hero는 필요없게 된다. 그래서 

#### ../hero.service.ts
에서 생성한 here를 추가해준다.

### 4. heroes.component를 바꾸기
#### ../src/app/heroes/heroes.component.ts (import HeroService)

```
import { Component, OnInit } from '@angular/core';
import { Hero } from '../hero';
// import { HEROES } from '../mock-heroes';
import { HeroService } from '../hero.service'; //추가된 부분

@Component({
  selector: 'app-heroes',
  templateUrl: './heroes.component.html',
  styleUrls: ['./heroes.component.css']
})
export class HeroesComponent implements OnInit {
  selectedHero: Hero;
  // heroes = HEROES;
  heroes: Hero[]; //추가된 부분

  onSelect(hero: Hero): void {
    this.selectedHero = hero;
  }

  getHeroes(): void {
    this.heroes = this.heroService.getHeroes();
  }
  constructor(private heroService: HeroService) { } //추가된 부분

  // component가 생성되자마자 호출하게된다 여기다 넣어두면
  ngOnInit() {
    this.getHeroes();//추가된 부분
  }

}

```

**설명**

서비스를 import해준다. 그리고 이제는 mock-heroes를 사용하지 않느니 주석처리를 해준다.

```
import { HeroService } from '../hero.service';
// import { HEROES } from '../mock-heroes';

```


마찬가지로 mock-heroes를 사용하지 않으니 주석처리해주고, 새로운 heroes: Hero[]를 추가해준다.

```
export class HeroesComponent implements OnInit {
  selectedHero: Hero;
  // heroes = HEROES;
  heroes: Hero[];

  onS...
```

생성자에 heroService를 추가해준다.

```
constructor(private heroService: HeroService) { } //추가된 부분
```

ngOnit에 함수를 추가하여 component가 생성되자마자 함수를 호출해 준다.

```
ngOnInit() {
   this.getHeroes();//추가된 부분
}
```

### Observable HeroService(공부 중)
obsevable을 왜 사용하는지 아직 모르겟지만 이걸 사용하려면 다음을 바꾸어야 한다.
#### ../hero.service.ts
기존의 getHeroes(): 를 주석처리한다. 그리고 observable를 반환하는 함수를 추가해준다.(아마 왠지 템플릿?)

```
import { Injectable } from '@angular/core';
import { Hero } from './hero';
import { HEROES } from './mock-heroes';
import {Observable} from "rxjs/Observable";
import {of} from "rxjs/observable/of";


@Injectable()
export class HeroService {

  // getHeroes(): Hero[] {
  //   return HEROES;
  // }


  getHeroes(): Observable<Hero[]> {
    return of(HEROES);
  }

  constructor() { }

}
```

이렇게 되면 component에서 getHeroes를 불러서 반환되는 값이 `Hero[]`가 아닌` Observable<Hero[]> `형태가 나오게 된다. 그래서 component의 함수도 바꾸어 주어야 한다.

#### ../hero.component.ts

```
getHeroes(): void {
	this.heroService.getHeroes()
  		.subscribe(heroes => this.heroes = heroes);
}
```

## show message

### 1. message component 생성

```
ng generate component messages

```
app.component에 방금 추가한 컴포넌트를 넣어준다.
#### ../src/app/app.component.html

```
<h1>{{title}}</h1>
<app-heroes></app-heroes>
<app-messages></app-messages> //추가된 부분
```

### 2. message service를 만들고 module에 추가한다. 
위의 과정을 한번에 하려면 다음 코드를 따른다.

```
ng generate service message --module=app

```

다음 코드를 추가
#### ../src/app/message.service.ts

```
import { Injectable } from '@angular/core';
 
@Injectable()
export class MessageService {
  messages: string[] = [];
 
  add(message: string) {
    this.messages.push(message);
  }
 
  clear() {
    this.messages = [];
  }
}
```
### 3. message Service를 hero Service에 추가한다.
그리고, getHeroes() 함수에 string을 push하는 명령어를 한줄 추가
#### ../src/app/hero.service.ts (import MessageService)

```
import { Injectable } from '@angular/core';
import { Hero } from './hero';
import { HEROES } from './mock-heroes';
import {Observable} from "rxjs/Observable";
import {of} from "rxjs/observable/of";
import {MessageService} from "./message.service"; //추가된 부분


@Injectable()
export class HeroService {

  // getHeroes(): Hero[] {
  //   return HEROES;
  // }

  getHeroes(): Observable<Hero[]> {
    this.messageService.add('HeroService: fetched heroes'); //추가된 부분
    return of(HEROES);
  }

  constructor(private messageService: MessageService) { } //추가된 부분

}

```
### 4. message componet의 ts을 조작한다.
#### ../messages.component.ts (import MessageService)

```
import { Component, OnInit } from '@angular/core';
import {MessageService} from "../message.service"; //추가된 부분

@Component({
  selector: 'app-messages',
  templateUrl: './messages.component.html',
  styleUrls: ['./messages.component.css']
})
export class MessagesComponent implements OnInit {

  constructor(public messageService: MessageService) { } //추가된 부분

  ngOnInit() {
  }

}
```

### 5. message.ts와 html을 바인딩 해준다.
#### src/app/messages/messages.component.html

```
<div *ngIf="messageService.messages.length">

  <h2>Messages</h2>
  <button class="clear"
          (click)="messageService.clear()">clear</button>
  <div *ngFor='let message of messageService.messages'> {{message}} </div>

</div>
```





