# The Human Password Manager

Version 0.1

## TL;DR

1. Choose long password connecting different words with a story (`canoe_punch_wallet_bear`)
1. Add non-dictionary salt (`canoe_RQ7831_punch_wallet_bear`)
1. Choose a non-obvious adaptable key (e.g. add first letter (+1) and last letter as capital: `canoe_RQ7831bN_punch_wallet_bear` for Amazon)

## Motivation

Inspired by [this post](http://blog.jgc.org/2016/05/two-factor-paper-passwords.html) by John Graham-Cumming I decided to document my thoughts on managing passwords. I agree with the post's author that password managers are the best way to handle individual passwords for each site, service, mail account, etc. 

However, on the one hand I also had difficulties to convince others of using such a tool in the past. On the other hand I prefer to just *know* my password by heart. I use different devices and for instance I do not trust my iPhone to keep my master password and database safe. 

So, based on my past experiences and many articles I read on the issue, I today use the following method. This gist is a general guide that will be updated whenever I have better ideas. Pull requests are welcome.

## Requirements

So what makes a password secure *and* memorable? Many people use the same password everywhere. Whenever they are forced to obey some password scheme, they will simply adapt it to the rules at hand. for instance `password` becomes `Password123$`. 

The problem with that is obvious: If the password is stolen from a site, the attacker would be able to login wherever the user has an account. If the site or company where the password was stolen did observed some basic security rules, they will not store the password as is is, but only its hash. In the `password` case that would be `5f4dcc3b5aa765d61d8327deb882cf99`. But still the attacker will be able to quickly figure out the password by using rainbow tables or even [Google](https://www.google.com/search?q=5f4dcc3b5aa765d61d8327deb882cf99). Security responsible sites will add a salt to the hash, but that is beyond the point here.

So the obvious solution is to use an individual password on each site or service. The lazy person's approach could be to use `password_ebay` for the ebay account. But the previous problem remains: If that password is stolen, it will be very easy to guess the pattern how the password was generated. It is likely that `password_amazon` will also work for the Amazon account probably with the same mail address as user name.

So what we need is a password that is:

1. Secure
2. Memorable
3. Adaptable
4. Not have an obvious adaptation pattern


## Algorithm

Get to the point already...

### 1. Choose password

Use a password of your liking. [JGC's blog post](http://blog.jgc.org/2016/05/two-factor-paper-passwords.html) has some great advice. Use some words that you like and combine them together in whatever way you want. So we can choose something like:

`canoe_punch_wallet_bear`

This should be still quite memorable. Maybe have a little story connecting these words and your brain will be happy to come up with them even after some days of not using the passphrase. 

### 2. Add salt

This is a fairly long password and therefore be reasonably secure. However, in my opinion it can never hurt to add some more random salt to a password. Adding letters / numbers / characters *that are not found in any dictionary*, will make the a [dictionary attack](https://en.wikipedia.org/wiki/Dictionary_attack) against the password much more difficult. I typically use something personal like my last phone number or initials of my last address -- make it not too hard so that you still can remember. That information should not be publicly available anywhere on the internets. Let's assume I lived in Residential Queens street and my postal code was 07831. So I could chose: `RQ7831`. Now add the salt to an arbitrary position in the existing password, like `canoe_RQ7831_punch_wallet_bear`.

### 3. Adaptability

The resulting passphrase is pretty sophisticated but it should be still personal enough to remember. The next step is to add some customisable part that can be adapted for each site. Since the processing power of the human brain (at least for these kind of things) is rather limited, it should be something quite simple. 

One idea would be to *use the first and last letter of the site*. To make it not too obvious one could *choose the next letter in the alphabet for the first letter and a capital letter for the last*. So for **A**mazo**n**.com this would be `b` and `N`. 

So the Amazon password is: `canoe_RQ7831bN_punch_wallet_bear`. For ebay it would be: `canoe_RQ7831fY_punch_wallet_bear`. And so on.

Of course there are many variations that can be applied to different parts of the password. Like: *Use a capital letter for the service name's length*. E.g. for ebay (4 letters => capital `O`): `canOe_RQ7831_punch_wallet_bear`

### Power salt

Use extra power salt. It is not always necessary to have a super long password. Criteria are the time it takes to construct the specific password in the head and typing a very long password. It is also possible to use a short version for sites you consider less critical (e.g. `canoe_RQ7831`) or a long one for very critical ones like your [GPG](https://www.gnupg.org/) private key (e.g. `canoe_RQ7831hG_punch_wallet_bear-super_$ecuritY`).

## Final words

No matter how simple your HPM algorithm is, I still recommend saving the password in a non-human password store like [KeePass](http://keepass.info/), etc.

## More reading

This is a collection of articles on the issue:

- [Blog post by John Graham-Cumming](http://blog.jgc.org/2016/05/two-factor-paper-passwords.html). He motivated me to write down my thoughts on the issue.
- [ArsTechnica article](http://arstechnica.com/security/2013/06/password-complexity-rules-more-annoying-less-effective-than-length-ones/): Password complexity rules more annoying, less effective than lengthy ones
