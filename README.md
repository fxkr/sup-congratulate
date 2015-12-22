# sup-congratulate

sup-congratulate is an auxiliary tool for the mail client sup (supmua.org).
It takes a list of birthdays from a CSV file and puts drafts of congratulations
emails in your drafts folder, so that they show up in your inbox.

* Version: 0.1.0
* Author: `Felix Kaiser <felix.kaiser@fxkr.net>`
* License: revised BSD (see LICENSE)


### Doesn't this make birthday greetings less sincere, less heartfelt?

No, not at all! But glad you asked.

I actually like sending (and receiving) birthday greetings.
However, it turns out that I'm just not capable of keeping track of birthdays,
and it always annoys me greatly when I've missed yet another opportunity.

For this reason, the script doesn't *send* mails,
but just puts the draft in my inbox, where I'll see it.

(Look at it this way: it was important enough for me that I spent
some time and automated (some part of) it. ;-)


# Setup

1. Create a tab-separated CSV file of friends, for example in
   `~/.config/sup-congratulate-friends`. It needs to contain at least
   a column with dates (in `DD.MM.YYYY` or `DD.MM.` form) and a column
   with names / email adresses (`John Doe <john@example.com>`).

  ```
  01.02.	Foo
  01.02.03	Bar
  ```

2. Optionally create a template file, for example in
   `~/.config/sup-congratulate-template`.

  ```
  From: {from}
  To: {to}
  Cc:
  Bcc:
  Subject: Happy Birthday!

  Happy birthday!

  Cheers
  {by}
  ```

3. Create a cronjob (all in one line!):

  ```
  */15 * * * * sup-congratulate
    --from 'Your Name <your.name@example.com>'
    --by Your
    --date-col 1
    --email-col 2
    --template-file ~/.config/sup-congratulate-template
    ~/.config/sup-congratulate-friends
    >/dev/null 2>&1
  ```

