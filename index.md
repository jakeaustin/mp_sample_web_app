<html>
  <head>
    <!-- JQ for listener convenience -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
    <!-- End JQ -->

<!-- OneTrust Cookies Consent Notice start for jakeaust.in -->
<script src="https://cdn.cookielaw.org/scripttemplates/otSDKStub.js"  type="text/javascript" charset="UTF-8" data-domain-script="4a2d6a35-9135-4b66-975a-206e6bcd2bb3-test" ></script>
<script type="text/javascript">
function OptanonWrapper() { }
</script>
<!-- OneTrust Cookies Consent Notice end for jakeaust.in -->
<!-- OneTrust Cookies Settings button start -->
<button id="ot-sdk-btn" class="ot-sdk-show-settings">Cookie Settings</button>
<!-- OneTrust Cookies Settings button end -->
<!-- OneTrust Cookies List start -->
<div id="ot-sdk-cookie-policy"></div>
<!-- OneTrust Cookies List end -->


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
    // event button handler
    jQuery(document).on('click','.button',function() {
      var doubleRoom = mParticle.eCommerce.createProduct(
          'Double Room - Econ Rate',
          'econ-1', 
          100.00, 
          4
      );
      // Get the cart
      var cart = mParticle.Identity.getCurrentUser().getCart();
      switch (jQuery(this).attr('id')) {
        case 'add-to-cart':
          cart.add(doubleRoom, true);
          break;
        case 'remove-from-cart':
          cart.remove(doubleRoom, true);
          break;
        case 'purchase':
          var transactionAttributes = {
              Id: 'foo-transaction-id',
              Revenue: 430.00,
              Tax: 30
          };
          mParticle.eCommerce.logPurchase(
              transactionAttributes,
              cart.getCartProducts(),
              true
          );
          break;
        case 'identify-me-by-non-login-identifier':
          var other_id = Math.random().toString();
          var loginRequest = {
            userIdentities: {
              other: other_id
            }
          };
        var loginCallback = function(result) { 
          jQuery('#identify-me-by-non-login-identifier').text('<b>other id is: '+other_id+'</b>');
          // sendMpidToNewRelic()
        } 
        mParticle.Identity.login(loginRequest, loginCallback);
          break;
       case 'identify-me-by-non-login-identifier-customer-id':
          var customer_id = Math.random().toString();
          var loginRequest = {
            userIdentities: {
              customerid: customer_id
            }
          };
        var loginCallback = function(result) { 
          jQuery('#identify-me-by-non-login-identifier-customer-id').text('<b>customer id is: '+customer_id+'</b>');
          // sendMpidToNewRelic()
        } 
        mParticle.Identity.login(loginRequest, loginCallback);
          break;
       case 'categories-test':
          // send custom click event
          mParticle.logEvent(
            'categories_test',
            mParticle.EventType.Other,
            {
               "categories": "Social, Food and Dining, Restaurants, Sushi, Japanese",
               "visit_duration": "5087",
               "visit_country": "us",
               "visit_locality": "Bloomington",
               "visit_region": "IN",
               "visit_name": "A Sushi Restaurant"
            }
          );
          break;
        default:
          break;
      }
    });

    // consent auth
    jQuery(document).on('click','#consent',function() {
      var location_collection_consent = mParticle.Consent.createGDPRConsent(
          true, // Consented
          Date.now(), // Timestamp
          "test_consent_agreement", // Document
          "257 Park Ave", // Location
          "IDFA:"+mParticle.Store.deviceId // Hardware ID
      );

      var user = mParticle.Identity.getCurrentUser();
      var userConsentState = user.getConsentState();

      if(userConsentState && userConsentState.getGDPRConsentState().location_collection) {
        // remove consent
        userConsentState.removeGDPRConsentState("location_collection");
        user.setConsentState(userConsentState);
        jQuery('#consent').css('background-color', 'red');
      } else {
        var consentState = mParticle.Consent.createConsentState();
        consentState.addGDPRConsentState("location_collection", location_collection_consent);
        user.setConsentState(consentState);
        jQuery('#consent').css('background-color', 'green');
      }
    });

    // logout
    jQuery(document).on('click','#logout',function() {
      var logoutCallback = function(result) { 
        if (result.getUser()) { 
          // sendMpidToNewRelic()
        } 
      };
      mParticle.Identity.logout({}, logoutCallback);
      jQuery('#logout').css('background-color', 'red');
      jQuery('#logout').prop('disabled', true);
      jQuery('#login button').prop('disabled', false);
      jQuery('#userinfo button').prop('disabled', true);
    });
    // login form
    jQuery(document).on('click','#login button',function() {
        var user_ids = {
            email: jQuery('#login .email').val()
        };
        try {
            var customer_id = mParticle.Identity.getCurrentUser().getUserIdentities().userIdentities.customerid;
        } catch(e) {}
        if(typeof customer_id !== "undefined") {
          user_ids.customerid = customer_id;
        }
        var loginRequest = {
          userIdentities: user_ids
        };
        var loginCallback = function(result) { 
          if (result.getUser()) { 
            // sendMpidToNewRelic()

            result.getUser().setUserAttribute('$FirstName', jQuery('#login .first_name').val());
            result.getUser().setUserAttribute('$LastName', jQuery('#login .last_name').val());
            result.getUser().setUserAttribute('$Age', jQuery('#login .age').val());
            result.getUser().setUserAttribute('$Gender', jQuery('#login input[name="gender"]:checked').val());
            result.getUser().setUserAttribute('Nickname', jQuery('#login .nickname').val());
          } 
          jQuery('#logout').css('background-color', 'green');
          jQuery('#logout').prop('disabled', false);
          jQuery('#login button').prop('disabled', true);
          jQuery('#userinfo button').prop('disabled', false);
        };
        mParticle.Identity.login(loginRequest, loginCallback);
    });
    // userinfo form
    jQuery(document).on('click','#userinfo button',function() {
        var modifyRequest = {
          userIdentities: {}
        };
        var modifyCallback = function(result) { 
          if (result.getUser()) { 
            // sendMpidToNewRelic()

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

<!--   <script>
    function sendMpidToNewRelic(){
        if(typeof mParticle !== "undefined" && typeof newrelic !== "undefined"){
            var mpid = mParticle.Identity.getCurrentUser().getMPID();
            console.log('mpid is: ' + mpid);
            newrelic.setCustomAttribute("mpid", mpid);
            newrelic.interaction();
        }
        else{
            setTimeout(sendMpidToNewRelic, 250);
        }
    }
    document.onreadystatechange = function(e)
    {
        if (document.readyState === 'complete')
        {
            sendMpidToNewRelic()
        }
    }    
  </script>
 -->
  </head>
  <body>
    <div>
      <button type='button' id="logout" style="color:white;background-color:red" disabled>Logout</button>
      <button type='button' id="consent" style="color:white;background-color:red">Location Consent</button>
    </div>
    <br><br>
    <div style="float:left">
      <h3>Login</h3>
      <form id="login" style="background-color: #ccc">
        <input class="email" placeholder="email@test.com"><br>
        <input class="first_name" placeholder="First Name"><br>
        <input class="last_name" placeholder="Last Name"><br>
        <input class="age" placeholder="30"><br>
        <input class="nickname" placeholder="Nickname"><br>
        <input type="radio" class="gender-m" name="gender" value="male" checked>
        <label for="gender">Male</label><br>
        <input type="radio" class="gender-f" name="gender" value="female">
        <label for="gender">Female</label><br>
        <button type='button'>Login</button>
      </form>
    </div>
    <div style="float:right">
      <h3>Update Info</h3>
      <form id="userinfo" style="background-color: #ccc">
        <input class="first_name" placeholder="First Name"><br>
        <input class="last_name" placeholder="Last Name"><br>
        <input class="age" placeholder="30"><br>
        <input class="nickname" placeholder="Nickname"><br>
        <input type="radio" class="gender-m" name="gender" value="male" checked>
        <label for="gender">Male</label><br>
        <input type="radio" class="gender-f" name="gender" value="female">
        <label for="gender">Female</label><br>
        <button type='button' disabled>Update</button>
    </form>
    </div>
    <div style="clear:both" align="center">
      <br><br>
      <button id="add-to-cart" class="button">Add-to-cart event</button>
      <button id="purchase" class="button">purchase event</button>
      <button id="remove-from-cart" class="button">remove-from-cart event</button>
      <button id="categories-test" class="button"> custom categories event </button>
      <button id="identify-me-by-non-login-identifier" class="button">identify-me-by-non-login-identifier (other)</button>
      <button id="identify-me-by-non-login-identifier-customer-id" class="button">identify-me-by-non-login-identifier-customer-id</button> 
    </div>
  </body>
</html>
