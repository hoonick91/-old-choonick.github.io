# error report
### 1. ng build 했을때 index.html이 script의 경로를 못찾을 경우
index.html에 <base href=''> 위의 형식으로 기본 url이 설정되어 있을 가능성이 높다.
provider를 이용하여 기본경로를 설정해 주어야 한다. 아래의 코드를 추가하여 기본경로를 설정한다.
#### ../app.module.ts
```
import { APP_BASE_HREF } from '@angular/common';

...

providers: [ {provide: APP_BASE_HREF, useValue: '/'}],

```


