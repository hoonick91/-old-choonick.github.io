# 데이터 바인딩 - post
post를 요청하기위해 html과 바인딩을 하겠다.

먼저 ts 파일에 바인딩할 객체를 만들어 준다.

#### ../post.component.ts
```
export class PostComponent implements OnInit {

  post: {name: string, date: string, money: string, reason: string} = {
    name: '',
    date: '',
    money: '',
    reason: '선택'
  };
  subm...
```

그리고 html에 [(ngModel)]을 이용하여 바인딩
#### ../post.component.html
```
<div class="container">
  <div class="well well-lg">

    <div class="input-group">
      <span class="input-group-addon">이름</span>
      <input id="name" type="text" class="form-control" name="name" placeholder="Additional Info" [(ngModel)]="post.name"> // 바인딩
    </div>

    <div class="input-group">
      <span class="input-group-addon">날짜</span>
      <input id="date" type="text" class="form-control" name="date" placeholder="Additional Info" [(ngModel)]="post.date"> // 바인딩
    </div>

    <div class="input-group">
      <span class="input-group-addon">벌금</span>
      <input id="gold" type="text" class="form-control" name="gold" placeholder="Additional Info" [(ngModel)]="post.money"> // 바인딩
    </div>

    <div class="input-group">
      <span class="input-group-addon" >사유</span>
      <select class="form-control" id="sel1" [(ngModel)]="post.reason"> // 바인딩
        <option disabled>선택</option> // 처음 보여주는 선택 상자
        <option>지각</option>
        <option>안 품</option>
        <option>결석</option>
      </select>
    </div>

  </div>



  <div class="submit">
    <!--<a [routerLink]="['/list']">명단 보기</a>-->
    <button (click)="submit()">명단 제출</button>
  </div>

</div>

```

그리고 (click)를 이용하여 객체에 값이 잘 저장됬는지 확인한다.

#### ../post.component.ts
```
submit(): void {
    console.log(this.post);
  }
```
