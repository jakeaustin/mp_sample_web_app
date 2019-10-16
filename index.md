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
    <!-- listeners to forward button clicks to mP events -->
    <script>
      jQuery(document).on('click','.button',function() {
        console.log('clicked id:' + jQuery(this).attr('id'));
      });
    </script> 
    <!-- End mP forwarding -->
  </head>
  <body>
    <!-- Google Tag Manager (noscript) -->
    <noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-WW62FCM"
    height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
    <!-- End Google Tag Manager (noscript) -->
    <div id="add-to-cart" class="button">Add-to-cart event</div>
    <div id="purchase-button" class="button">purchase event</div>
    <div id="remove-from-cart" class="button">remove-from-cart event</div>
    <div id="checkout" class="button">checkout event</div>
  </body>
</html>
