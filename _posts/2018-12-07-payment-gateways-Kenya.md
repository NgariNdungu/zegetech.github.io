---
layout: blog
title: Developers getting paid online in Kenya, Whats the fuss!
author: Tom Nyongesa, Ngari Ndung'u, Melvin Atieno
blog-image: localgateways/localgateways.png
intro: With the rise in use of mobile payment in Kenya, businesses are scrambling to put their houses in order just to keep up with the fast technological pace and the adaption of online payments by Kenyans. Kenyans at large are really interested in the outcome of this - an easy payment interface that hides the complex processes of really getting this done. This process is largely a developer's task. This is a developer's journey analysing Kenyan online payment gateways and their ease of integration.
---
![Payment Gateways](/assets/images/blog/{{page.blog-image}}){:class="img-responsive center"}
{{page.intro}}

With the multiple payment gateways for Kenya, it will probably be a real hurdle for a Kenyan developer to choose the most optimal payment solution for his problem. When thinking about their choice, the very first thing that would come into their mind is the friction of onboarding - the time it would take to integrate it to an real app. Then the learning curve. They would probably think of  googling for sample integration codes and reviews  on the internet...they'll think of many other things. We would like to make it easier by outlining an analysis on payment gateways in Kenya.

It is a theoritical and technical analysis of the following Payment Gateways, in no particular order:

### 1. Mpesa
[![Mpesa](/assets/images/blog/localgateways/mpesa.jpg){:class="img-responsive center img-standard"}](https://developer.safaricom.co.ke/docs)
Any Kenya focused business would first think of Mpesa.

M-Pesa is a mobile phone-based money transfer, financing and microfinancing service, launched in 2007 by Vodafone for Safaricom. Mpesa not so recently commercialized their APIs allowing businesses and developers to intergrate their payment services into their various solutions. This saw the launch of their first generation API which they dubbed "G2". This saw a great shift in MPESA adoption and transformed the market. G2 was however a painful and utterly unfriendly API to integate to, with VPN setups and Soap protocol on asynchronous and sychronous requests being the biggest pain points. Most recently, MPESA launched "Daraja" their new RESTful API running off of Apigee, the API management platform recently acquired by google. This promises better experience and easier integration.

There exists a documentation for Daraja Mpesa APIs and a sandbox for testing. The documentation is slightly flawed in that the paramenters are not clearly described and one would have to jump a few huddles before getting around them. There are no provided examples for the request parameters which adds to the struggle. The credentials expire in an hour so for testing one would have to constantly renew them.

[Mpesa Daraja Postman docs](https://documenter.getpostman.com/view/5951719/RzfnkSEx)

### 2. Pesapal
[![PesaPal](/assets/images/blog/localgateways/Pesapal.png){:class="img-responsive center img-standard"}](https://www.pesapal.com/)
This is one of the better known payment gateways and has been around for a while. A pesapal wallet allows a merchant to accept payments from mobile money, cards and select mobile banking accounts. The API's main integration method is via page redirection.

Official plugins are provided for Magento, Shopify and WHMCS. Code samples are provided for .NET and PHP.

An IPN (instant payment notification) endpoint together with related query endpoints are available. Pesapal also provides a demo site with both personal and merchant accounts to test integration. It is however missing direct payment endpoints typical of most API based solutions that you can call to perform action such as querying, withdrawals etc. 

### 3. iPay
[![iPay](/assets/images/blog/localgateways/ipay-logo.png){:class="img-responsive center img-standard"}](https://ipayafrica.com/)
iPay provides mobile money (Mpesa, Airtel and EazzyPay) and credit card integrations.
The API can be consumed either through ‘Web-based integration’ which is a page redirect to their website or ‘REST API integration’. Plugins for the major CMSs are provided, as well as an android library.

The documentation provided is useable though it could be done better. The test credentials are somewhat hidden. I only figured them out while taking a second read through, after enquiries went unanswered.
It wasn't immediately obvious as to the availability of a testing sandbox.

The API requires that a HMAC signature of the data be sent along in the request body. 
The parameter values have to be concatenated in a particular order to get the expected string to hash. This can be more than a slight annoyance and the shortened parameter names do not help either.

Whether because of the used secret key while testing, or a difference in the HMAC algorithm used, the hash generated was always incorrect.
The API does however respond with the expected hash and the string hashed to obtain it which made testing easier.
You can find the scripts we used to generate the signature [here.](https://gist.github.com/NgariNdungu/e8c83a03038d445488e73cefa6c42032)

### 4. Africa's Talking
[![Africa's Talking](/assets/images/blog/localgateways/africastalking.png){:class="img-responsive center img-standard"}](http://docs.africastalking.com/)
Africa's talking provides Restful APIs for integration with their various services. These services include; SMS,voice, Payments,USSD, and Airtime. Our point of focus was mainly their payment services. Customer to Business (C2B), Business to Customer (B2C), and Business to business (B2B). The services are offered over mobile, banks and cards. There are client SDKs for PHP, Python, C#, Java, JS, and Ruby. For mobile payments, Africa's talking does the hosting and one needs a dedicated pay bill with Safaricom M-Pesa (application process takes approximately 5 days). They do not offer any other mobile payment services. The bank payment and card payment services are currently only available in Nigeria. The accepted cards are MasterCard and Verve cards. Africa's talking offers a sandbox, a simulator and associated endpoints for testing. On integration one also gets a dashboard on which they can monitor transactions and carry out other maintenance services such as getting credentials for authentication and creating products.

[Africa's Talking Postman Collection](https://documenter.getpostman.com/view/5951719/RzfnkSEu )

### 5. Jambo Pay
[![Jambo Pay](/assets/images/blog/localgateways/jambopay.png){:class="img-responsive center img-standard"}](https://www.jambopay.com/)
Jambopay has two ways for integrating with their API; ‘Express Checkout’ and ‘Redirect Checkout’.
Express checkout allows the customer to complete payment within the site while redirect checkout loads a Jambopay provided page to complete payment.
For each a PHP and .NET library are provided. A pdf document in the downloaded zip file is the entirety of the documentation to be found.
Without documentation it was not possible to test out the API.

### 6. Sapama Cash
[![Sapama Cash](/assets/images/blog/localgateways/sapama.png){:class="img-responsive center img-standard"}](http://sapamacash.com/docs)
Sapama cash supports payments made via Equitel and Mpesa only. 
Getting an account with Sapama Cash can also be a hurdle. However, they provide credentials for their test account which you can use to test out their C2B, B2C and other APIs. Something else about their system once you login with their test credetials is that you are provided with html forms having fields into which you fill in your API parameters and callback urls. The probably might be usig this to cater to the less tech-savvy individuals, people who are used to html forms. It would make things easier for them and make them less concerned about the kind of language to use when interacting with their APIs. However, their form submit buttons result to error pages. 

They have a documentation that seems easy to follow the only problem being that their endpoints result to error pages that exposes too much information about their system, simply put as poor exception handling and security. 

### 7. Jenga
[![Jenga](/assets/images/blog/localgateways/jenga.png){:class="img-responsive center img-standard"}](https://developer.jengaapi.io/)
I would say Jenga is an all in one payment gateway. It has managed to integrate major payment channels used in Kenya including card payments, Mpesa, PayPal, Amex, Airtel Money, Equitel, bank payments, AliPay, Masterpass. It has also managed to go beyond the borders to countries like Tanzania, South Sudan and Uganda. Having a test account with them enables you to test their APIs for sending money within Equity, sending money across multiple banks via PesaLink, sending money from bank to mobile wallets via PesaLink, perfoming cross-border remittances with SWIFT, performing common account ops like checking account balance, getting an account's full statement; performing utility bill payments, performing loan services like credit worthiness of an individual, airtime purchases etc. 

Another added feature of Jenga System is that you can actually partner with them to become a reseller. We haven't tried this but you are free to give it a try.

The annoying thing about them is the process of getting a testing account. It requires one to fill out an application form that won't be responded to immediately. It took them 3 days to actually okay my application and this was only after I followed up. Maybe it would have taken more time that neccesary. 

Nevertheless, they have a relatively easy to follow documentation of their APIs and a Postman Collection! They also provide sample credentials on their documentation. You can actually test their APIs with their sample credentials if you don't want to apply for a test account. 
If you need to test the APIs with your test account credentials, you have to authenticate your requests. You have to generate a digital signature using RSA and sign your requests using it. Instructions for this are found on their documentation.

[Jenga Postman Collection](https://documenter.getpostman.com/view/1238477/Rzfnikkt)

### 8. Lipisha
[![Lipisha](/assets/images/blog/localgateways/lipisha.webp){:class="img-responsive center img-standard"}](https://lipisha.com/payments/accounts/index.php/app/launch)
Lipisha is a payment service provider that allows integration through webhooks, popular e-commerce Plugins, and RestAPIs. The details on integration through plugins is not available. The APIs allow integration of mobile and card payment services. The available option for mobile payment services is M-Pesa. The endpoints also allow integration of payout services to clients' mobile wallet. The documentation could be made clearer for all the services Lipisha can provide. They offer a sandbox for testing and the endpoints can be tested manually using postman.

[Lipisha Postman Collection](https://documenter.getpostman.com/view/5951719/RzfnkSEw)

### 9. Flutterwave
[![Flutterwave](/assets/images/blog/localgateways/rave.svg){:class="img-responsive center img-standard"}](https://rave.flutterwave.com/)
Also called Rave, the Flutterwave Rave API provides mobile money and card payment integration, with bank integration in Nigeria.
Nodejs and Android SDKs are provided along with plugins for the more popular CMSs.
Documentation for the API is provided, though it can be a bit of a challenge to navigate through.
The main documentation page is focused on quick integration using their javascript library and page embeds, with the reference page giving the fuller outlook of the API.
For testing, a sandbox url is provided, with test credentials, cards, bank accounts and mobile numbers included.

The API *charge* endpoints require that the request parameters be encrypted with [3DES encryption.](https://developer.flutterwave.com/v2.0/reference#rave-encryption)
Trying to perform the encryption in postman was an exercise in futility. The included `crypto-js` library's implementation of the algorithm proved incompatible with rave.
There are code examples for js, php, python, java and c#. [Here's](https://gist.github.com/NgariNdungu/2aa67db5f5a2d0c454e7b22d1c4de845) the working code for ruby.

### 10. Kopokopo
[![Kopokopo](/assets/images/blog/localgateways/kopo.png){:class="img-responsive center img-standard"}](https://app.kopokopo.com/push_api)
My experience with Kopokopo integration was unsuccessful. I couldn't create an account with them because of their business requirements. You need to send them copies of your ID and business registration documents for review before trying out their APIs. However, they support RESTful API posts and FTP file serving system - you can setup your own FTP server or use their FTP server. What happens with this kind of FTP system is that K2(KopoKopo) generates csv files having transaction details and sends them to your configured FTP server, you can then parse the csv files however you like. 

They support payments in Mpesa, Masterpass and T-Kash. 

### 11. Beyonic
[![Beyonic](/assets/images/blog/localgateways/beyonic.png){:class="img-responsive center img-standard"}](https://beyonic.com/)
Beyonic is focused on mobile money integrations. With their API you can receive money and make payments in Kenya, Uganda, Rwanda, Tanzania and Rwanda.

There are official client libraries for Python, Ruby and PHP with code samples for Java. 
There is a Woo-Commerce plugin for integrating with Wordpress sites, and beta integration with Zapier.
The API is well documented with helpful pointers for the developer to follow.

At the time of testing, the test environment seemed to be in maintenance. Being unable to load BXC(Beyonic test currency) we couldn’t test the payments endpoints.
It was still possible to test some collection endpoints using the documented test numbers.

### 12. Direct Pay
[![Direct Pay](/assets/images/blog/localgateways/dpo.png){:class="img-responsive center img-standard"}](https://www.directpay.online/)
DirectPay formerly known as 3G direct has services spanning across more than 10 countries namely Botswana, Kenya, Namibia, Zambia, Ghana, Mauritius, South Africa, Ethiopia, Malawi, Nigeria, Tanzania, Zanzibar, Zimbabwe, Rwanda and Uganda. I managed to create an account with DPO's platform, inquired whether they have a public API but am still waiting for a response from them. 

On a scale of 1-5, here are my findings based on the following features:
- Developer friendly
- Documentation
- Accessibility
- Multiple Libraries
- Testability

| Gateway | Developer friendly | Documentation | Accesibility | Multiple Libraries | Testability| Aggregate|
|:----|----|----|----|----|----|----|
| Africas Talking | 5| 5| 4 | 3 | 4 | **4** |
| Lipisha | 3 | 3 | 4 | 3 | 4 | **3** |
| pesapal | 3 | 3 | 4 | 3 | 3 | **3** |
| Sapama Cash | 3 | 2 | 2 | 3 | 2 | **2** |
| Kopokopo | 1 | 1 | 2 | 1 | 1 | **1** |
| Jenga | 4 | 4 | 4 | 4 | 4 | **4** |
| Jambopay |1 | 1 | 1 | 1 | 1| **1** |
| iPay | 3 | 3 | 2 | 3 | 2 | **2** |
| Rave | 4 | 4 | 4 | 4 | 4 | **4** |
| Beyonic | 4 | 4 | 3 | 4 | 3 | **3** |
| Direct Pay | - | - | - | - | - | - |

Here's a table that summarizes the functionality. I believe this will help you save some time:

| Gateway | Rest API | Plugins | IPN | Page Redirects | Testing bed| Payment Method supported|
|:----|----|----|----|----|----|----|
| Africas Talking |Yes| No| yes | No |yes  |Mobile(mpesa),Card(Master and verve cards, available only in nigeria)  |
| Lipisha | Yes | yes | yes | No | yes |Mpesa,visa, mastercard, airtelmoney,Discover, easywallet, EcoCash  |
| pesapal | No | Yes | Yes | Yes | Yes | M-Pesa, Airtel Money, Yu Cash, MTN money, Vodacom, Co-op Mobile, Eazzy 24/7, Visa, MasterCard |
| Sapama Cash | No | No | Yes | No | Yes | Equitel, Mpesa |
| Kopokopo | No | No | Yes | No | No | Mpesa, Masterpass, Tkash |
| Jenga | Yes | No | Yes | No | Yes | Visa, MC, JCB, Maestro, Diners club, CUP, AMEX, Paypal, Airtel Money, Mpesa, Equitel, PesaLink, RTGS, SWIFT |
| Jambopay | No | No | No | Yes | No | Mpesa, Credit/Debit card, Airtel Money, kenswitch |
| iPay | Yes | Yes | Yes | Yes | Yes | Mpesa, Credit/Debit card, Equitel, Airtel Money, kenswitch |
| Rave | Yes | Yes | Yes | Yes | Yes | Mpesa, Credit/Debit card |
| Beyonic | Yes | Yes | Yes | Yes | Yes | Mpesa, Airtel |

If there's any other payment gateway in Kenya I've left out, I will add it as I come across it. 

[Github Repo on the Payment Gateways' collections](https://github.com/zegetech/postmans-payment-gateways)

Happy development!