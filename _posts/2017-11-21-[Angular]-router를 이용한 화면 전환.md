### angular router를 이용한 화면 전환

1. 필요한 컴포넌트를 만든다.
2. app.routing.ts를 만든다.
3. app.module.ts에서 모듈을 추가한다.



#### 1. 필요한 컴포넌트를 만든다.
```
$ ng generate component home
$ ng generate component post
```
#### 2. app.routing.ts를 만든다.
##### ../app/app.routing.ts
```
import { Routes, RouterModule } from '@angular/router';
import { HomeComponent } from './home/home.component';
import  {PostComponent } from './post/post.component';

const routes: Routes = [
  {path: '', component: HomeComponent},
  {path: 'post', component: PostComponent}
];

export const routing = RouterModule.forRoot(routes);

```

routes의 path를 설정해준다.


routing을 export로 선언해준다. 
위에서 선언한 routing을 module에 추가해주어야 한다.
#### 3. app.module.ts에서 모듈을 추가한다.
```
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';


import { AppComponent } from './app.component';
import { PostComponent } from './post/post.component';
import { HomeComponent } from './home/home.component';
import {routing} from './app.routing'; //추가된 부분


@NgModule({
  declarations: [
    AppComponent,
    PostComponent,
    HomeComponent
  ],
  imports: [
    BrowserModule,
    routing // 추가된 부분
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }


```

### 4. 마지막으로 html에 링크를 걸어준다.
#### ../app/app.component.html
```
<!--The content below is only a placeholder and can be replaced.-->
<div style="text-align:center">
  <h1>
    {{title}}
  </h1>
  <a [routerLink]="['/']">Home</a>
  <a [routerLink]="['/post']">post</a>
  <router-outlet></router-outlet>
</div>

```

??질문사항

```
  <a [routerLink]="['/']">Home</a>
  <a href="/">testhome</a> 
```



#### 현재 위의 방법은 하나의 페이지안에 뷰를 바꾸는 것이다.