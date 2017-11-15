---
layout: post
title:  AngularJS_facebook login 연동하기
---
> 매우 쉽고 간단하다


	<script>
	  function statusChangeCallback(response) {
	
	    console.log('statusChangeCallback');
	    console.log(response);
	
	    if (response.status === 'connected') {
	      // Logged into your app and Facebook.
	      testAPI();
	    } else {
	      // The person is not logged into your app or we are unable to tell.
	      document.getElementById('status').innerHTML = 'Please log ' +
	        'into this app.';
	    }
	  }
<br>
	
	function checkLoginState() {
	    FB.getLoginStatus(function (response) {
	      statusChangeCallback(response);
	    });
	  }
	
	  window.fbAsyncInit = function () {
	    FB.init({
	      appId: '355566331536659',
	      cookie: true,  // enable cookies to allow the server to access
	                     // the session
	      xfbml: true,  // parse social plugins on this page
	      version: 'v2.8' // use graph api version 2.8
	    });
	
	
	    FB.getLoginStatus(function (response) {
	      statusChangeCallback(response);
	    });
	
	  };

<br>	

	  // Load the SDK asynchronously
	  (function (d, s, id) {
	    var js, fjs = d.getElementsByTagName(s)[0];
	    if (d.getElementById(id)) return;
	    js = d.createElement(s);
	    js.id = id;
	    js.src = "//connect.facebook.net/ko_KR/sdk.js";
	    fjs.parentNode.insertBefore(js, fjs);
	  }(document, 'script', 'facebook-jssdk'));
	
	
	  function testAPI() {
	    console.log('Welcome!  Fetching your information.... ');
	    FB.api('/me', function (response) {
	
	      console.log(response);
	
	      console.log('Successful login for: ' + response.name);
	      document.getElementById('status').innerHTML =
	        'Thanks for logging in, ' + response.name + '!';
	    });
	
	  }
	
	  function logout() {
	    FB.logout(function () {
	
	    });
	
	
	  }
	</script>
	
	
<br>
	
 	<fb:login-button scope="public_profile,email" onlogin="checkLoginState();">
    </fb:login-button>

	<div
    	class="fb-like"
    	data-share="true"
    	data-width="450"
    	data-show-faces="true">	
   	</div>

	<div id="status"></div>