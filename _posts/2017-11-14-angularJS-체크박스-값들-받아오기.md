## angularjs 체크박스 값들 받아오기


```
var chk = document.getElementsByName('chartChk[]');
      var len = chk.length;
      var chartIds = [];
      var chartTitles = [];
      $scope.chartList = [];


      for (var i = 0; i < len; i++) {
        if (chk[i].checked === true) {
          // 차트명
          chartIds.push(chk[i].value.split(',')[0]);
          // 차트아이디
          chartTitles.push(chk[i].value.split(',')[1]);

        }
      }

      $scope.chartList = chartTitles;
```