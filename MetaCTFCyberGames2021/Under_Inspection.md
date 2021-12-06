# The Challenge (Web Exploitation)

Someone made this site for the Autobots to chat with each other. Seems like the Decepticons have found the site too and made accounts.

https://metaproblems.com/2841e99cee26f773b26b300acad556c4/inspect/

One of the Autobot accounts has a flag that they're trying to keep hidden from the Decepticons, can you figure out which account it is and steal it?

# Solution

inspect element -> network -> inspect/ html file has javaascript for client side authentication
Lists all of the usernames and their passwords, as well as having a check to see which one is allowed to access the flag

We see the following credentials iin plaintext:
	**{user: "Jazz", pwd: "MetaCTF{do_it_with_style_or_dont_do_it_at_all} **




