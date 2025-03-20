# Autocalling-sysytem-using-Twilio



from twilio.rest import Client
import time


fvar = open(r'phone_nums.txt','r')
phone_nums = [x.strip('\n') for x in fvar.readlines()]
fvar.close()




def call():

    account_sid = '<Your account sid>'
    auth_token = '<your auth token>'
    twilio_from  = '<your twilio number>'
    client = Client(account_sid, auth_token)

    print(phone_nums)
    
    for num in phone_nums:
        print("Num = " , num)
        call = client.calls.create(
                                url='<your twiml bin url>',
                                to=num,
                                from_=twilio_from,
                                #url = 'https://handler.twilio.com/twiml/EHfbb90737b757304c9b3cbcb81ba73770?' + urlencode({category:dict_msg[category]})
                                )

        print(call.sid)
        call_sid = call.sid

        time.sleep(30)

        call = client.calls(call_sid).fetch()
        call_status = call.status

        print(" Call status ===== > " , call_status)

        if(call_status == "completed"):
            print(" Call has been aswered by " , num)
        else:
            print(num , "dint pick the call trying the next persion in the list ")

        

callnow()
