# Spam utils

These are various tools I use for my anti-spam research and other activities.

## ticket-message-dump

`ticket-message-dump` is a quick and dirty _initial_ message dumper, useful to extract close renderings of the message that opened an RT ticket. I wrote it to assist in SpamAssassin rule creation.

This is an example of how to run it.

```
carton exec ./ticket-message-dump \
  --debug \
  --dsn 'dbi:Pg:host=localhost;user=lem;database=rt4' \
  21104 21107
```

Which would produce output similar to this due to the `--debug` command line flag:

```
root part 275469 multipart/mixed; boundary="----=_NextPart_000_0001_8C308CB1.4A91FA4F"
parts_set 275470 → 275469 multipart/alternative; boundary="----=_NextPart_001_0002_AE1BEFF0.FC07D445"
parts_set 275471 → 275470 text/plain; charset="utf-8"
parts_add 275472 → 275470 text/html; charset="utf-8"
parts_add 275473 → 275469 application/pdf; name="Bible Atonement, Blessings &   Prayers Answered_Content2.pdf"
parts_add 275474 → 275469 application/pdf; name="Bible -Faith Verses.pdf"
parts_add 275475 → 275469 application/pdf; name="Bible- Wisdom Verses.pdf"
parts_add 275476 → 275469 application/pdf; name="Bible-Happiness, Prosperity & Long   Life Verses.pdf"
* 21104: Pastoral Books
+ multipart/mixed; boundary="----=_NextPart_000_0001_8C308CB1.4A91FA4F"
     + multipart/alternative; boundary="----=_NextPart_001_0002_AE1BEFF0.FC07D445"
          + text/plain; charset="utf-8"
          + text/html; charset="utf-8"
     + application/pdf; name="Bible Atonement, Blessings &   Prayers Answered_Content2.pdf"
     + application/pdf; name="Bible -Faith Verses.pdf"
     + application/pdf; name="Bible- Wisdom Verses.pdf"
     + application/pdf; name="Bible-Happiness, Prosperity & Long   Life Verses.pdf"
root part 275485 multipart/alternative; boundary="-==AGNITASOUTER164240059B2900001A=="
parts_set 275486 → 275485 text/plain; charset="UTF-8"
parts_add 275487 → 275485 text/html; charset="UTF-8"
* 21107: Customized Solution for Website Design
+ multipart/alternative; boundary="-==AGNITASOUTER164240059B2900001A=="
     + text/plain; charset="UTF-8"
     + text/html; charset="UTF-8"
```

The file `rt-21104.eml` and `rt-21107.eml` would contain a partial reconstruction of the original email messages.

> The resulting email is not a perfect reproduction of the email that opened the ticket, because Request Tracker performs various steps in the process of creating a ticket that alter the headers and body in non-reversible ways.
