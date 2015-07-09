# Introduction #

This package provides neat and simple method to validate the paid result with [Paypal IPN](https://www.paypal.com/ipn). It's NOT intended to make the paypal integration "plug 'n' play". It still requires the developer to understand the [Paypal Process](https://www.paypal.com/cgi-bin/webscr?cmd=p/dmo/demo_ipn_1-outside) and know the [HTML Variables](https://cms.paypal.com/cgi-bin/?cmd=_render-content&content_ID=developer/e_howto_html_Appx_websitestandard_htmlvariables) you want/need to pass to paypal to achieve what you want.

# Details #

To submit an order to paypal, have your order form POST to a file with:
```
$p = new paypal_class;
$p->add_field('business', 'somebody@domain.com');
$p->add_field('field_name', 'field_value']);
//....add all your fields in the same manor
$p->submit_paypal_post();
```

To process an IPN, have your IPN processing file contain:
```
$p = new paypal_class;
if ($p->validate_ipn()) {
	//....IPN is verified.  IPN POST Details are in the ipn_data() array
}
$p->send_report($subject);
$p->print_report(); 
//print and send the ipn validation status detial.
```

# Paypal Manual #
[Integrating Using HTML](https://cms.paypal.com/cgi-bin/?cmd=_render-content&content_ID=developer/howto_html_landing): How to integrate Paypal using simple html and receive messages when payments are made on your website or e-commerce solution using IPN.

[Instant Payment Notification (IPN) Manual](https://cms.paypal.com/cms_content/en_US/files/developer/PP_OrderMgmt_IntegrationGuide.pdf): This gives you all the information you need including the fields you can pass to paypal (using add\_field() with this class) as well as all the fields that are returned in an IPN post (stored in the ipn\_data() array in this class).  It also diagrams the entire transaction process.

[IPN Variables](https://cms.paypal.com/cgi-bin/?cmd=_render-content&content_ID=developer/e_howto_html_IPNandPDTVariables): Paypal returns related variables for each kind of IPN or PDT message.