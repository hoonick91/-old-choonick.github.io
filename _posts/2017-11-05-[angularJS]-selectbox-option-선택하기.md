---
layout: post
title:  AngularJS_selectbox option 선택값 가져오기
---

> html

```
<select id="branch" class="form-control" style="width: 170px;height: 35px" ng-model="Content.dept"
                          ng-change="add_branch(Content.dept)">

	<option value="" disabled style="background-color: yellow">#분과</option>
	<option ng-repeat="dept in cate.dept" ng-value="dept">{{dept}}</option>
	<option style="color: grey">##분과 추가하기</option>

</select>
```


>js

```
var sel = document.getElementById('branch');
var val = sel.options[sel.selectedIndex].text;
```