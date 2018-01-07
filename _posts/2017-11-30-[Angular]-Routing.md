# Routing
### 1. 라우팅모듈을 생성한다.

```
ng generate module app-routing --flat --module=app

```
만들어진 ts파일에 내용을 추가

#### ../src/app/app-routing.module.ts (v1)
```
import { NgModule }             from '@angular/core';
import { RouterModule, Routes } from '@angular/router';

@NgModule({
  exports: [ RouterModule ]
})
export class AppRoutingModule {}
```
그리고 이어서 route를 추가해준다.

```
import { HeroesComponent }      from './heroes/heroes.component';

const routes: Routes = [
  { path: 'heroes', component: HeroesComponent }
];
```
이어서  import 모듈을 추가( 왜 하는지는 모르겠다. )

```
imports: [ RouterModule.forRoot(routes) ],

```

### 2. 뷰에 router-outlet를 추가

#### ../src/app/app.component.html (router-outlet)
router-outlet 부분에 뷰가 나오게 된다.

```
<h1>{{title}}</h1>
<router-outlet></router-outlet> 
<app-messages></app-messages>
```

### 3. 뷰에 이어서 navigation link를 추가
```
<h1>{{title}}</h1>
<nav>
  <a routerLink="/heroes">Heroes</a> // 추가된 부분
</nav>
<router-outlet></router-outlet>
<app-messages></app-messages>
```

### 4. dashboard component를 추가한다.
```
ng generate component dashboard

```

#### ../dashboard.component.html
```
<h3>Top Heroes</h3>
<div class="grid grid-pad">
  <a *ngFor="let hero of heroes" class="col-1-4">
    <div class="module hero">
      <h4>{{hero.name}}</h4>
    </div>
  </a>
</div>
```
#### ../dashboard.component.ts
```
import { Component, OnInit } from '@angular/core';
import { Hero } from '../hero';
import { HeroService } from '../hero.service';
 
@Component({
  selector: 'app-dashboard',
  templateUrl: './dashboard.component.html',
  styleUrls: [ './dashboard.component.css' ]
})
export class DashboardComponent implements OnInit {
  heroes: Hero[] = [];
 
  constructor(private heroService: HeroService) { }
 
  ngOnInit() {
    this.getHeroes();
  }
 
  getHeroes(): void {
    this.heroService.getHeroes()
      .subscribe(heroes => this.heroes = heroes.slice(1, 5));
  }
}
```

dashboard route를 ../app-routing.module.ts에 추가한다. 이어서 _route_도 추가 해준다.
#### ../src/app/app-routing.module.ts

```
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HeroesComponent } from './heroes/heroes.component';
import { DashboardComponent } from './dashboard/dashboard.component'; // 추가된 부분

const routes: Routes = [
  { path: '', redirectTo: '/dashboard', pathMatch: 'full' }, // 추가된 부분
  { path: 'dashboard', component: DashboardComponent }, // route 추가된 부분
];

@NgModule({
  imports: [ RouterModule.forRoot(routes) ], // 추가된 부분
  exports: [
    RouterModule
  ],
})
export class AppRoutingModule { }

```

app.componenty.html에 dashboard의 링크도 추가 해준다.
#### ../src/app/app.component.html

```
<h1>{{title}}</h1>
<nav>
  <a routerLink="/dashboard">Dashboard</a> // 추가된 부분
  <a routerLink="/heroes">Heroes</a>
</nav>
<router-outlet></router-outlet>
<app-messages></app-messages>
```

### 5. hero details로 이동하기

- 기존에 만든 herescomponent의 herodetail을 지운다.
- ../heroes.component.html ```<app-hero-detail>``` 를 지워준다.
- 아래의 코드를 추가

#### ../app-routing.module.ts	

```
import { HeroDetailComponent }  from './hero-detail/hero-detail.component'
 ...
const routes: Routes = [
  { path: '', redirectTo: '/dashboard', pathMatch: 'full' },
  { path: 'dashboard', component: DashboardComponent },
  { path: 'detail/:id', component: HeroDetailComponent },
  { path: 'heroes', component: HeroesComponent }
];
```

dashboard의 hero link를 걸어준다. 아래 코드를 추가
#### ../src/app/dashboard/dashboard.component.html
```
<a *ngFor="let hero of heroes" class="col-1-4"
    routerLink="/detail/{{hero.id}}">
```

기존에 onSelect()로 된 herocomponent.html의 부분을 아래와 같이 수정한다.
#### ../src/app/heroes/heroes.component.html
```
<ul class="heroes">
  <li *ngFor="let hero of heroes">
    <a routerLink="/detail/{{hero.id}}">
      <span class="badge">{{hero.id}}</span> {{hero.name}}
    </a>
  </li>
</ul>
```

hero.component.ts의 사용하지 않는 코드를 지운다.
#### ../src/app/heroes/heroes.component.ts
```
import { Component, OnInit } from '@angular/core';
import { Hero } from '../hero';
import { HEROES } from '../mock-heroes';
import { HeroService } from '../hero.service';




@Component({
  selector: 'app-heroes',
  templateUrl: './heroes.component.html',
  styleUrls: ['./heroes.component.css']
})
export class HeroesComponent implements OnInit {
  heroes: Hero[];

  getHeroes(): void {
    this.heroService.getHeroes()
      .subscribe(heroes => this.heroes = heroes);
  }

  constructor(private heroService: HeroService) { }

  // component가 생성되자마자 호출하게된다 여기다 넣어두면
  ngOnInit() {
    this.getHeroes();
    // this.getTest();
  }

}

```

### 6. 라우팅할 수있는 heroDetailComponent

새로 함수를 작성하고 필요한 모듈을 import 한다.

#### ../src/app/hero-detail/hero-detail.component.ts
```
import { Component, OnInit, Input } from '@angular/core';
import {Hero} from '../hero';
import { ActivatedRoute } from '@angular/router'; // 추가된 부분
import { Location } from '@angular/common'; // 추가된 부분
import { HeroService } from '../hero.service';

@Component({
  selector: 'app-hero-detail',
  templateUrl: './hero-detail.component.html',
  styleUrls: ['./hero-detail.component.css']
})
export class HeroDetailComponent implements OnInit {

  @Input() hero: Hero;
  constructor(private route: ActivatedRoute, // 추가된 부분
              private heroService: HeroService, // 추가된 부분
              private location: Location) { } // 추가된 부분

  getHero(): void { // 추가된 부분
    const id = +this.route.snapshot.paramMap.get('id');
    this.heroService.getHero(id)
      .subscribe(hero => this.hero = hero);
  }

  goBack(): void { // 추가된 부분
    this.location.back(); 
  }
  ngOnInit() {
    this.getHero();
    }

}

```

hero.service에 새로운 getHero를 정의 한다.

#### ../src/app/hero.service.ts (getHero)
```
getHero(id: number): Observable<Hero> {
  // Todo: send the message _after_ fetching the hero
  this.messageService.add(`HeroService: fetched hero id=${id}`);
  return of(HEROES.find(hero => hero.id === id));
}
```

뷰에 backbutton을 추가한다.
#### ../src/app/hero-detail/hero-detail.component.html (back button)

```
src/app/hero-detail/hero-detail.component.html (back button)
```