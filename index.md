<html>
  <head>
    <!-- Google Tag Manager -->
    <script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
    new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
    j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
    'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
    })(window,document,'script','dataLayer','GTM-WW62FCM');</script>
    <!-- End Google Tag Manager -->
    <!-- JQ for listener convenience -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
    <!-- End JQ -->
    <!-- mP web SDK -->
    <script type="text/javascript">
    window.mParticle = {
      config: {
        isDevelopmentMode: true //switch to false (or remove) for production
      }
    };

    (
      function(t){window.mParticle=window.mParticle||{};mParticle.EventType={Unknown:0,Navigation:1,Location:2,Search:3,Transaction:4,UserContent:5,UserPreference:6,Social:7,Other:8};window.mParticle.eCommerce={Cart:{}};window.mParticle.Identity={};window.mParticle.config=window.mParticle.config||{};window.mParticle.config.rq=[];window.mParticle.config.snippetVersion=2.1;window.mParticle.ready=function(t){window.mParticle.config.rq.push(t)};function e(e,o){return function(){if(o){e=o+"."+e}var t=Array.prototype.slice.call(arguments);t.unshift(e);window.mParticle.config.rq.push(t)}}var o=["endSession","logError","logEvent","logForm","logLink","logPageView","setSessionAttribute","setAppName","setAppVersion","setOptOut","setPosition","startNewSession","startTrackingLocation","stopTrackingLocation"];var n=["setCurrencyCode","logCheckout"];var i=["identify","login","logout","modify"];o.forEach(function(t){window.mParticle[t]=e(t)});n.forEach(function(t){window.mParticle.eCommerce[t]=e(t,"eCommerce")});i.forEach(function(t){window.mParticle.Identity[t]=e(t,"Identity")});var r=document.createElement("script");r.type="text/javascript";r.async=true;r.src=("https:"==document.location.protocol?"https://jssdkcdns":"http://jssdkcdn")+".mparticle.com/js/v2/"+t+"/mparticle.js";var c=document.getElementsByTagName("script")[0];c.parentNode.insertBefore(r,c);}
    )("us1-8343aa0c8f16e74b9176320270fc92da");
  </script>
    <!-- End mP web SDK -->
    <!-- listeners to forward button clicks to mP events -->
    <script>
      // initial page view event when snippet loads
      window.mParticle.ready(
        function() {
          console.log('in mP ready');
        }   
      );

      // event button handler
      jQuery(document).on('click','.button',function() {
        console.log('clicked id:' + jQuery(this).attr('id'));
      });

      // login form
      jQuery(document).on('click','#login input[type="submit"]',function() {
          var loginRequest = {
            userIdentities: {
              email: jQuery('#login .email').val()
            }
          };
          var loginCallback = function(result) { 
            if (result.getUser()) { 
              result.getUser().setUserAttribute('$FirstName', jQuery('#login .first_name').val());
              result.getUser().setUserAttribute('$LastName', jQuery('#login .last_name').val());
              result.getUser().setUserAttribute('$Age', jQuery('#login .age').val());
              result.getUser().setUserAttribute('$Gender', jQuery('#login input[name="gender"]:checked').val());
              result.getUser().setUserAttribute('Nickname', jQuery('#login .nickname').val());
            } 
          };
          mParticle.Identity.login(loginRequest, loginCallback);
      });
      // userinfo form
      jQuery(document).on('click','#userinfo input[type="submit"]',function() {
          var modifyRequest = {
            userIdentities: {}
          };
          var modifyCallback = function(result) { 
            if (result.getUser()) { 
              result.getUser().setUserAttribute('$FirstName', jQuery('#userinfo .first_name').val());
              result.getUser().setUserAttribute('$LastName', jQuery('#userinfo .last_name').val());
              result.getUser().setUserAttribute('$Age', jQuery('#userinfo .age').val());
              result.getUser().setUserAttribute('$Gender', jQuery('#userinfo input[name="gender"]:checked').val());
              result.getUser().setUserAttribute('Nickname', jQuery('#userinfo .nickname').val());
            } 
          };
          mParticle.Identity.modify(modifyRequest, modifyCallback);
      });
    </script> 
    <!-- End mP forwarding -->
  </head>
  <body>
    <!-- Google Tag Manager (noscript) -->
    <noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-WW62FCM"
    height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
    <!-- End Google Tag Manager (noscript) -->
    <div style="float:left">
      <h3>Login</h3>
      <form id="login" style="background-color: #ccc">
        <input class="email" placeholder="email@test.com"><br>
        <input class="first_name" placeholder="John"><br>
        <input class="last_name" placeholder="Smith"><br>
        <input class="age" placeholder="27"><br>
        <input class="nickname" placeholder="Young Febreezy"><br>
        <input type="radio" class="gender-m" name="gender" value="male" checked>
        <label for="gender">Male</label><br>
        <input type="radio" class="gender-f" name="gender" value="female">
        <label for="gender">Female</label><br>
        <input type="submit" value="Login">
      </form>
    </div>
    <div style="float:right">
      <h3>Update Info</h3>
      <form id="userinfo" style="background-color: #ccc">
        <input class="first_name" placeholder="John"><br>
        <input class="last_name" placeholder="Smith"><br>
        <input class="age" placeholder="27"><br>
        <input class="nickname" placeholder="Young Febreezy"><br>
        <input type="radio" class="gender-m" name="gender" value="male" checked>
        <label for="gender">Male</label><br>
        <input type="radio" class="gender-f" name="gender" value="female">
        <label for="gender">Female</label><br>
        <input type="submit" value="Update">
    </form>
    </div>
    <br>
    <div id="add-to-cart" class="button">Add-to-cart event</div>
    <div id="purchase-button" class="button">purchase event</div>
    <div id="remove-from-cart" class="button">remove-from-cart event</div>
    <div id="checkout" class="button">checkout event</div>
  </body>
</html>
