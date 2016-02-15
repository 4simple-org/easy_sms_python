SMS API Client for Python
=========================

Installation
------------

> pip  install sms_api


This lib allow easily add SMS text messages to your python applications. Just create an account in
https://easysms.4simple.org for obtain your API credential.
Code Examples ::

    # Step #1 is import required API client class
    from sms_api import SMS_Easy
    
    # Step #2 is create an API client object using credential obtained from https://easysms.4simple.org/user/panel/
    api_obj = SMS_Easy(user_id=65344, auth_token='s532sa79f68fa981cf5551a')
    
    
    ##########################################################################
    #            HOW SEND AN SMS TEXT MESSAGE
    ##########################################################################
    
    # Sending an SMS in just one line
    result = api_obj.send_sms(to="15446355", body="Hello Testing SMS API")
    
    pid = -1
    # Optionally, we can verify if SMS was accepted without errors.
    if result.get("success") == "ok":
        print "SMS message was processed successfully. SMS processing id(pid) is: %s" % result.get("pid")
        pid = result.get("pid")
    elif "error" in result:
        print "Error while try to send SMS due to: %s" % result.get("error")
    
    
    ##########################################################################
    #            HOW CHECK ACCOUNT BALANCE
    ##########################################################################
    
    # Just call function get_account_balance
    result = api_obj.get_account_balance()
    
    if isinstance(result, dict) and "error" in result:
        print "Error while try get account balance due to: %s" % result.get("error")
    else:
        print "Your account balance is: %s" % result
    
    
    ##########################################################################
    #            HOW CHECK SMS PROCESSING STATUS
    ##########################################################################
    
    # Using the processing id (pid) returned when the SMS message was sent, just call this function.
    result = api_obj.get_sms_status(pid)
    
    if isinstance(result, dict) and "error" in result:
        print "Error while try get SMS processing status for pid %s, due to: %s" % (pid, result.get("error"))
    else:
        print "SMS processing status for pid %s is %s" % (pid, result.get("status"))