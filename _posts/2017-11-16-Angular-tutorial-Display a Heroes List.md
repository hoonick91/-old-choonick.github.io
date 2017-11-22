# Display a Heroes List
### 목차
- 리스트 생성하기
- *ngFor
- hero detail 만들기
- click event 추가
- *ngIf
- [class.selected]

여기선 hero리스트를 선택하고 그 상세정보를 보여주는 것을 할 것이다.


## Create mock heroes
여러개의 heroes를 보여주기 위해 mock-heroes.ts를 만든다.
#### src/app/mock-heroes.ts

```
import { Hero } from './hero';

export const HEROES: Hero[] = [
  { id: 11, name: 'Mr. Nice' },
  { id: 12, name: 'Narco' },
  { id: 13, name: 'Bombasto' },
  { id: 14, name: 'Celeritas' },
  { id: 15, name: 'Magneta' },
  { id: 16, name: 'RubberMan' },
  { id: 17, name: 'Dynama' },
  { id: 18, name: 'Dr IQ' },
  { id: 19, name: 'Magma' },
  { id: 20, name: 'Tornado' }
];
```

## Displaying heroes
hero component에 방금 만든 HEROES를 추가해준다.

#### ../heroes.component.ts

```
import { Component, OnInit } from '@angular/core';
// import { Hero } from '../hero';
import { HEROES } from '../mock-heroes'; // 추가된 항목

@Component({
  selector: 'app-heroes',
  templateUrl: './heroes.component.html',
  styleUrls: ['./heroes.component.css']
})
export class HeroesComponent implements OnInit {

  // hero: Hero = {
  //   id : 1,
  //   name : 'Windstorm'
  // };
  heroes = HEROES; //추가된 항목
  constructor() { }

  ngOnInit() {
  }

}

```

### List heroes with *ngFor
HEROES의 값을들 반복문으로 뿌려줄 수 있다.

#### ../heroes.component.html

```
<h2>My Heroes</h2>
<ul class="heroes">
  <li *ngFor="let hero of heroes">
    <span class="badge">{{hero.id}}</span> {{hero.name}}
  </li>
</ul>
```

이제 여기에 css를 입혀보자
#### ../heroes.component.css

```
/* HeroesComponent's private CSS styles */
.selected {
  background-color: #CFD8DC !important;
  color: white;
}
.heroes {
  margin: 0 0 2em 0;
  list-style-type: none;
  padding: 0;
  width: 15em;
}
.heroes li {
  cursor: pointer;
  position: relative;
  left: 0;
  background-color: #EEE;
  margin: .5em;
  padding: .3em 0;
  height: 1.6em;
  border-radius: 4px;
}
.heroes li.selected:hover {
  background-color: #BBD8DC !important;
  color: white;
}
.heroes li:hover {
  color: #607D8B;
  background-color: #DDD;
  left: .1em;
}
.heroes .text {
  position: relative;
  top: -3px;
}
.heroes .badge {
  display: inline-block;
  font-size: small;
  color: white;
  padding: 0.8em 0.7em 0 0.7em;
  background-color: #607D8B;
  line-height: 1em;
  position: relative;
  left: -1px;
  top: -4px;
  height: 1.8em;
  margin-right: .8em;
  border-radius: 4px 0 0 4px;
}
```

## Master/Detail
hero를 클릭했을때 그 정보를 보는 것을 할 것이다.

### Add a click event binding
li 태그에 다음을 추가하자

#### heroes.component.html

``` <li *ngFor="let hero of heroes" (click)="onSelect(hero)">```

여기서 onSelect는 HeroesComponent의 method이다.

### Add the click event handler
click이벤트 핸들러를 추가해보자

#### ../heroes.component.ts
```
import { Component, OnInit } from '@angular/core';
import { Hero } from '../hero';
import { HEROES } from '../mock-heroes';

@Component({
  selector: 'app-heroes',
  templateUrl: './heroes.component.html',
  styleUrls: ['./heroes.component.css']
})
export class HeroesComponent implements OnInit {
// 추가된 부분
  selectedHero: Hero;
  heroes = HEROES;

// 추가된 부분
  onSelect(hero: Hero): void {
    this.selectedHero = hero;
  }
  constructor() { }

  ngOnInit() {
  }

}

```

### Update the details template
hero template에 hero detail을 표시할 부분을 추가한다.
#### ../heroes.component.html
```
<h2>{{ selectedHero.name | uppercase }} Details</h2>
<div><span>id: </span>{{selectedHero.id}}</div>
<div>
  <label>name:
    <input [(ngModel)]="selectedHero.name" placeholder="name">
  </label>
</div>
```

### Hide empty details with *ngIf

하지만 실행 브라우저의 console에 보면 다음과 같은 오류가 표시된다.
> HeroesComponent.html:3 ERROR TypeError: Cannot read property 'name' of undefined

아직 hero가 클릭되지 않았기 때문에 selectHero.name이 undefine이기 때문이다. 그래서
클릭되기 전에는 hero detail	부분을 숨겨주어야 한다.

#### ../heroes.component.html (*ngIf)

```
<div *ngIf="selectedHero">

  <h2>{{ selectedHero.name | uppercase }} Details</h2>
  <div><span>id: </span>{{selectedHero.id}}</div>
  <div>
    <label>name:
      <input [(ngModel)]="selectedHero.name" placeholder="name">
    </label>
  </div>

</div>```

### Style the selected hero
선택되었을 때 heroes 목록에 선택되었다는 css가 적용되지 않는다. 그래서 적용하기 위해
``` [class.selected]="hero === selectedHero"```를 추가한다.

hero === selectedHero 가 성립할때 즉, 클릭했을 때 
class.selected를 적용시킨다.
여기서 class = heroes

#### ../heroes.component.html

```
<li *ngFor="let hero of heroes"
  [class.selected]="hero === selectedHero"
  (click)="onSelect(hero)">
  <span class="badge">{{hero.id}}</span> {{hero.name}}
</li>
```



<a href="https://angular.io/tutorial/toh-pt2"> 참고 사이트 </a>

