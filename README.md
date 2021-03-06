# uk-it-recruiter-domains

List of the domains of UK IT recruiters &amp; some scripts for processing it.

## Why?

I get a torrent of email from IT recruiters. Some of them contain well-targeted, intelligble specs for jobs I might actually want.  Most don't, and I don't want them clogging up my inbox.

Maintaining a list of domains they send email from makes it easy to filter messages into their own folder.  It's easy to process the list into formats suitable for different mail systems: gmail and sieve rulesets are currently supported and contributions for others are welcome.



## Google Mail

GMail support is achieved via filters, you can import [gmailFilters.xml](https://github.com/alexmbird/uk-it-recruiter-domains/blob/master/gmailFilters.xml) from the filters page in the interface.

```
# ./scripts/domains2gmail.rb
# ls -l gmailFilters.xml
-rw-r--r--  1 mock mock  13501  3 Dec 11:30 gmailFilters.xml
```

A few things worth noting:

- Filters have a max query length, so we break them up into chunks of 70.
- By default we add a "Recruitment" label and archive any matches, you'll   probably want to edit the filters created.
- If you reimport the filters, the originals remain.
- Update the XML based on domains.txt by running [scripts/domains2gmail.rb](https://github.com/alexmbird/uk-it-recruiter-domains/blob/master/scripts/domains2gmail.py).


## Contributing

There are two ways to do this.

#### Classic

Checkout the project from GitHub, add your line to domains.txt and send a pull request with it in.  Please try to keep the sorting correct and add *only* the domain, not a full email address.  `noisyrecruitmentagency.com` is good; `some-person@noisyrecruitmentagency.com` is bad.

#### Pro

Use the 'addnew.sh' script.  This takes care of duplicate checking & sorting and automatically strips any username@ portion of the string you feed it.  Also it's smart enough to push your changes back to GitHub if you ask it to.

```bash
MockAir13:uk-it-recruiter-domains mock$ ./scripts/addnew.sh shinysuit@noisyrecruiters.com
domain extracted from email address: noisyrecruiters.com
Adding 'noisyrecruiters.com' to domains.txt
Don't forget to commit & push to GitHub
```

or

```bash
MockAir13:uk-it-recruiter-domains mock$ ./scripts/addnew.sh -p shinysuit@noisyrecruiters.com
domain extracted from email address: noisyrecruiters.com
Adding 'noisyrecruiters.com' to domains.txt
...commits & pushes to GitHub
```

## Conventions

*   Domains all in lowercase (`addnew.sh` lowercases them automatically)
*   One domain per line
*   No leading/trailing whitespace
*   __Check every domain you add is really a recruitment agency.__  Consultancies, email providers (e.g. gmail) and internal recruiters at big companies don't count.



## Alternatives

[Recruiter Ham](http://recruiterham.joshuafox.com) is a fledgling project to build a reputation system for recruiters with an easy-to-use gmail interface.

