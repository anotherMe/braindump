
# mail ( with mailx )

Send mail:

  mail -s "Mail subject" mydestination@mydomain.com < body.txt

As you can see, mail body must be provided as a text file.


Send the same email specifying sender address:

  mail -s "Mail subject" recipient@mydomain.com -f sender@mydomain.com < body.txt


Send an empty mail:

  mail -s "Mail subject" mydestination@mydomain.com < /dev/null

