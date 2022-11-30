# As a user, I select a language on my home page of `drifter.live`.  The content that I see is in the language that I choose.  The messages I receive are also in this language.  Without selecting a language, the language defaults to the `lang` attribute in the `<html>` tag.

* [ ] add enum in User model for language
REF - https://blog.saeloun.com/2022/01/05/how-to-use-enums-in-rails.html

... as per REF `https://www.w3.org/International/questions/qa-http-and-lang`
These language abbreviations are ISO 639-1 Language Codes

* [ ] start with this list of languages:
*They are the languages I have come across the most in the oilfield... with the addition of Albanian which is for Eneida*
```
{
  en: 0,
  sq: 10,
  ar: 20,
  zh: 30,
  hi: 40,
  id: 50,
  pt: 60,
  ro: 70,
  ru: 80,
  es: 90,
  th: 100,
  vi: 110,
},
{
  en: English,
  sq: Albanian,
  ar: Arabic,
  zh: Chinese,
  hi: Hindi,
  id: Indonesion,
  pt: Portuguese,
  ro: Romanian,
  ru: Russian,
  es: Spanish,
  th: Thai,
  vi: Vietnamese
}
```

* [ ] yml file for all text fragments throughout the page
