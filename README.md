# Jquery-check-existing-email
### In functions.php
```
add_action('wp_ajax_check_user_email', 'check_user_email_function');
add_action('wp_ajax_nopriv_check_user_email', 'check_user_email_function');
function check_user_email_function()
{
	
global $wpdb;
	$users_table_name= $wpdb->prefix.'postmeta';
	$email=$_POST['c_email'];

	$email_result = $wpdb->get_row("select meta_value from $users_table_name where meta_value ='$email'");
	// print_r($email_result);
	if($email_result){
		
		 $valid='false';
	}
	else{
		if(email_exists($email)){
		  $valid='false';
		}
		else{
           $valid ='true';
		}
		// $valid='true';
	}
	
echo $valid;
die();

}
```

### In custom.js
```
 billing_email: {       
    required: true,
    email: true,
     remote: {
            url: customform.ajaxurl,
            type: "post",
            data:{
               'c_email': function() { return jQuery( ".billing-mail-class" ).val(); },
              'action': 'check_user_email'
         }
     } 
},
```
