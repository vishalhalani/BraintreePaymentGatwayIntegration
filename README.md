# BraintreePaymentGatwayIntegration

Paypal Mobile Sdk now deprecated so now as per suggestion by paypal use <b>BrainTree</b> or <b>Paypal Express checkout</b> payment gateway.
<br>
<br>
So this is small example of integration with BrainTree Payment gateway. You need to create <b>sandbox</b> Account from <a href="https://www.braintreepayments.com/sandbox"> sign up here </a>



# Client Side intergration 
    
  You can easily integrate client side using official braintree docs <a href="https://developers.braintreepayments.com/start/hello-client/android/v2">here</a>
  
# Server Side intergration 
    
  You can easily integrate server side using official braintree docs <a href="https://developers.braintreepayments.com/start/hello-server/php">here</a>
  
# Step 1

I was did using <b>xampp</b> server make sure you use php version greater than 5.4 version. So first install xampp server.

you can easily download <b>Braintree library</b> from <a href="https://developers.braintreepayments.com/start/hello-server/php">here</a>  <br><b>or</b><br> you can download using <b>Composer</b>

you can download composer from <a href="https://getcomposer.org/download/">download Composer</a> and install it.

# Step 2

Create one directory <b>braintreepayment</b> inside <b>xampp->htdocs</b>

Create one file <b>composer.json</b> inside <b>xampp->htdocs->braintreepayment</b> write below code in file.


```groovy
{
  "require" : {
    "braintree/braintree_php" : "3.30.0"
  }
}
```

# Step 3

Open terminal and move to your braintreepayment directory then run command like below

`composer install`

# Step 4
Now create new directory with name <b>include</b> inside braintreepayment directory.
<br><br>
Now create new file with name <b>configuration.php</b> inside include directory with below script.


```groovy
<?php
session_start();
require_once("vendor/autoload.php");
if(file_exists(__DIR__ . "/../.env")) {
    $dotenv = new Dotenv\Dotenv(__DIR__ . "/../");
    $dotenv->load();
}

$gateway = new Braintree_Gateway([
  'environment' => 'sandbox',
  'merchantId' => 'ADD YOUR MERCHENT ID HERE',
  'publicKey' => 'ADD PUBLIC KEY HERE',
  'privateKey' => 'ADD PRIVATE KEY HERE'
]);
?>
```

# Step 5

Now create new file with name <b>getClientToken.php</b> inside braintreepayment directory with below script.

```groovy
<?php
require_once ("include/configuration.php");
require_once 'vendor/braintree/braintree_php/lib/Braintree.php';
echo ($clientToken = $gateway->clientToken()->generate());
?>
```
# Step 6

Now create new file with name <b>checkout.php</b> inside braintreepayment directory with below script.

```groovy
<?php
require_once ("include/configuration.php");
require_once 'vendor/braintree/braintree_php/lib/Braintree.php';


$nonce = $_POST['nonce'];
$amount = $_POST['amount'];

$result = $gateway->transaction()->sale([
  'amount' =>$amount,
  'paymentMethodNonce' => $nonce,
  'options' => [
    'submitForSettlement' => True
  ]
]);

echo $result;
?>
```


# You can check Example of all payment Method using Braintree Payment gatway <a href="https://github.com/braintree/braintree_android">check here</a>

