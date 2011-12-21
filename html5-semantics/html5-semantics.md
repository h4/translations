# Семантика HTML5
> Оригинал статьи на английском языке: [HTML5 semantics](http://coding.smashingmagazine.com/2011/11/18/html5-semantics/).

Наибольшее волнение вокруг HTML5 возникло вокруг новых API: локальное хранилище (local storage), кеш приложения, Web workers, 2D-графика и тому подобное. Но давайте не забывать, что HTML5 принёс нам 30 новых элементов для разметки наших страниц и приложений. Таким образом, общее число имеющихся html-элементов перевалило за 100.

Даже самые навороченные, изобилующие JavaScript'ом веб-два-нольные приложения содержат текстовое содержимое, которое должно быть размечено с умом, так давайте взглянем на некоторые новые элементы, чтобы ваш следующий проект был настолько же семантичным, насколько и интерактивным.

Чтобы эта статья на разрослась до размеров книги, мы не будет рассматривать всё подробно. Вместо этого, мы коснёмся всего понемногу: вы увидите, что вам доступно в HTML5 и сможете изучить то, что вас заинтересовало подробнее, перейдя по отобранным мной ссылкам.

По пути мы увидим, что семантика HTML5 тщательно продумана - расширяя возможности HTML, она позволяет при этом получить доступ к содержимому для пользователей устаревших браузеров. Мы также увидим, что семантическая разметка это не просто ещё одна забавная игрушка, а скорее краеугольный камень веб-разработки, это то, что может повысить доступность (accessibility), улучшить положение в поисковых системах, расширить возможности интернализации и совместимости. 

Натуральные языки, такие как английский, обладая словарным объёмом в миллионы слов, подчас не могут выразить все нюансы человеческой мысли. Так что распоряжаясь только сотней элементов, доступных нам в HTML, мы часто можем оказаться в ситуации, когда не ясно, какой именно элемент использовать для того или иного фрагмента содержимого. В таких случаях выберите какой-нибудь один и используйте его во всех аналогичных ситуациях на вашем сайте, просто будьте последовательны.

## Некоторых элементов представления больше нет

Чисто визуальные (презентационные) элементы, такие как `center`, `font` или `big` окончательно устарели. Они были полностью вытеснены каскадными таблицами стилей. Но это не значит, что нужно тотчас броситься переписывать все старые страницы. В HTML5 такие элементы считаются устаревшими для использования в новых документах, но поскольку HTML5 не стремится разрушить веб, браузеры по-прежнему будут корректно показывать подобные устаревшие страницы.

По той же причине были удалены атрибуты, влияющие на отображение элементов. Такие, например, как `align` для `img` и `table`, `background` для `body` и `bgcolor` для `table`.

Гадкие элементы фреймов отстутствуют в HTML5. Фреймы вызывают огромные проблемы с юзабилити и доступностью, если вы никак не можете отказаться от их использования — используйте старый DOCTYPE, что бы  иметь возможность валидировать страницы.

Это краткий обзор, вы может найти полный список удалённых элементов и атрибутов в документации на W3C.

## Некоторым элементам представления была добавлена семантическая роль

Но не все элементы представления оказались преданы забвению. Некоторые из них получили новое семантическое назначение. Например, элемент small больше не означает "вывести текст шрифтом уменьшенного размера", хотя для него можно задать такое отображение в таблице стилей. Теперь его стоит применять для вывода различных примечаний, которые обычно печатают мелким шрифтом:

Мелким текстом обычно набирают различные дисклеймеры (отказ от ответсвености), предостережения, предостережения или информация об авторских правах. Мелким текстом также часто набирают разъяснения или лицензионные ограничения.

Some of the redefinitions feel to me to be a mop-up. While I can get behind <b> for drawing attention to product names, keywords and so forth, without any special emphasis implied, specifying the semantics for marking up ship names (<i>, if you’re so inclined) feels weirdly precise. But I get seasick, and your nautical mileage may vary. With similar niche precision:

The u element [now] represents a span of text with an unarticulated, though explicitly rendered, non-textual annotation, such as labeling the text as being a proper name in Chinese text (a Chinese proper name mark), or labeling the text as being misspelt.

You can read more about changed elements and attributes on the W3C website.

## Классная новая семантика

We all know about video and audio. And canvas is particularly popular at the moment because it allows for 3-D graphics using webGL, so game designers can port their products to the Web. Like good ol’ img, these semantics are embedded content, because they drag in content from another source — either a file, a data URI or JavaScript.

Unlike img, however, they have opening and closing tags, allowing for fallbacks. Therefore, browsers that don’t support the new semantics can be fed some content: an image could be the fallback for a canvas, for example, or a Flash movie could be the fallback for video, a technique called “video for everybody.”

The source and track elements are empty elements (with no closing tags) that are children of video or audio.

The source element gets past the codec Tower of Babel that we have. Each element points to a different source file (WebM, MP4, Ogg Theora), and the browser will play the first one it knows how to deal with:

1
<audio controls>
2
  <source src=bieber.ogg type=audio/ogg>
3
  <source src=bieber.mp3 type=audio/mp3>
4
    <!-- fallback content: -->
5
    Download <a href=bieber.ogg>Ogg</a> or <a href=bieber.mp3>MP3</a> formats.
6
</audio>
In this example, Opera, Firefox and Chrome will download the Ogg version of Master Bieber’s latest toe-tappin’ masterpiece, while Safari and IE will grab the MP3 version. Chrome can play both Ogg and MP3, but browsers will download the first source file that they understand. The fallback content between the opening and closing tags is a link to download the content to the desktop and play it via a separate media player, and it is only shown in browsers that can’t play native multimedia.

For video, you could use an embedded Flash movie hosted on YouTube:

1
<video controls>
2
  <source src=best-video-ever.webm type=video/webm>
3
  <source src=best-video-ever.mp4 type=video/mp4>
4
    <!-- fallback content: -->
5
    <iframe width="480" height="360"
6
      src="http://www.youtube.com/embed/xzMUyqmaqcw?rel=0"
7
      frameborder="0" allowfullscreen>
8
    </iframe>
9
</video>
This way, users of older browsers, such as IE 6-8, will see a YouTube movie (as long as they have the Flash Player), so they will at least be able to see the video, while users with modern browsers will get the full native-video experience. Everyone gets the content, then, which is what your website is there for, after all.

The track element is a newer addition to the HTML5 family and is being implemented by Opera, Chrome and IE at the moment. It points to a subtitle file that contains text and timing information. When implemented, it synchronizes captions with the media file to enable on-demand subtitling and captioning; useful not only for viewers who are hard of hearing, but also for those who do not speak the language used in the audio or video file.

## Семантика для интернационализации

Less woo! than the semantics for multimedia and games are the semantics for internationalization. It may surprise the cool kids in Silicon Valley to learn that a worldwide Web of people use languages other than English and even use different writing systems.

Languages such as Arabic and Hebrew are written right to left, unlike European languages, which are written left to right. On pages that use only one writing system, this doesn’t present a problem, but on pages with bi-directional (“bidi”) writing, browsers have to decide where to put punctuation, bullets, numbers and the like. Browsers usually do a pretty good job using the Unicode bidirectional algorithm, but it gets it wrong in some cases, which can seriously dent the comprehensibility of content.

HTML5 gives us a bdi element, which enables authors to override the Unicode bidirectional algorithm and make their text more comprehensible. For a further description of the problem and to see how bdi solves it, see “HTML5’s New bdi Element” by Richard Ishida, the W3C’s internationalization activity lead.

Some languages have scripts that are not alphabetic at all, but that express an idea rather than a sound. Occasionally, an author will have to assist readers with pronunciation for especially rare or awkward characters, usually by providing an alternate script in a small font above the relevant character. In print, this was traditionally done with a very small 5-point font called “ruby,” and HTML5 gives us three new elements for marking up ruby text: ruby, rt and rp.

For more information, see “The HTML5 ruby Element in Words of One Syllable or Less” by Daniel Davis.

## Структурная семантика

Most people are aware that HTML5 gives us many new elements to describe parts of a Web page, such as header, footer, nav, section, article, aside and so on. These exist because we Web developers actually wanted such semantics. How did the authors of the HTML5 specification know this? Because in 2005 Google analyzed 1 billion pages to see what authors were using as class names on divs and other elements. More recently, in 2008, Opera MAMA analyzed 3 million URLs to see the top class names and top IDs used in the wild. These analyses revealed that authors wanted to mark up these areas of the page but had no elements to do so, other than the humble and generic div, to which they then added descriptive classes and IDs.

(HTML5 Doctor has many articles about HTML5 semantics, so we won’t bloat this article by going in depth here. Warning: some were written by me.)

The new semantics were built to degrade gracefully. For example, consider what the specification has to say about the new figure element:

The figure element represents some flow content, optionally with a caption, that is self-contained and is typically referenced as a single unit from the main flow of the document.

The element can thus be used to annotate illustrations, diagrams, photos, code listings, etc…

This isn’t a new idea. HTML3 proposed a fig element (which never made it into the final HTML 3.2 specification). It looked like this:

1
<FIG SRC="nicodamus.jpeg">
2
   <CAPTION>Ground dweller: <I>Nicodamus bicolor</I> builds silk snares</CAPTION>
3
   <P>A small hairy spider.
4
   <CREDIT>J. A. L. Cooke/OSF</CREDIT></P>
5
</FIG>
There’s a big problem with this. In browsers that do not support fig (and none do), the image wouldn’t be displayed because the fig element would be completely ignored. The contents of the credit element would be displayed, because it’s just text. So you’d get a credit with no image on older browsers.

In HTML5, you would code the same example like so:

1
<figure>
2
<img src="nicodamus.jpeg">
3
   <figcaption>
4
      <p>Ground dweller: <i>Nicodamus bicolor</i> builds silk snares.</p>
5
      <p>A small hairy spider.
6
      <small>J. A. L. Cooke/OSF</small&gt</p>
7
   </figcaption>
8
</figure>
Unlike the aborted HTML3 syntax, the HTML5 version is backwards-compatible: a browser that doesn’t “know” about the figure element will still show the img and the text inside figcaption (as the HTML3 credit element would similarly display its content). Note that we’re using the redefined small element, instead of minting a new credit element. Remember that “Small print is also sometimes used for attribution.”

HTML5 also gives us a new figcaption element. Originally, the specification’s authors tried to reuse caption, as suggested in HTML3, but there were legacy problems, because caption had previously only been a child of table.

One of the design principles on which HTML5 is based is that new features should degrade gracefully. When they can’t, the language allows for fallback content. It tries to reuse elements rather than mint new ones — but it’s a pragmatic language: when minting something new is necessary, it does so.

## Интерактивная семантика

The structural elements of HTML5 currently don’t do much in visual browsers, although software that sits on top of browsers (such as screen readers) are starting to use them (see “HTML5, ARIA Roles, and Screen Readers in March 2011“ and “JAWS, IE and Headings in HTML5.”)

Other elements do have a visual effect. The details element, for example, is a groovy interactive element that functions as “a disclosure widget from which the user can obtain additional information or controls.”

Most browsers will implement it as an “expando box”: when the user clicks on some browser-generated icon (such as a triangle or downwards-pointing arrow) or the word “Details” (which can be replaced by the author’s own rubric in a child summary), the element will slide open, revealing its details within. The details could be a full description of an image or graph, a description of a complex table, advanced options for a search form, or just about anything else. This is a common need on the Web today, now made native and obviating the need for custom JavaScript.

Most of us have seen HTML5’s new form semantics. Most of these are attributes of the input element, thereby ensuring graceful degradation to <input type=text> in older browsers. New elements include datalist, output, progress and meter.

## Имеем ли мы право на семантику?

So, we have many new semantics, but are they the right ones? After all, the Google research on which they were based was conducted in 2005 — quite some time ago! Perhaps the semantics are already somewhat behind the times? Many have noted that they’re document-centric rather than application-centric. Do we need more application-centered semantics, such as a login or share element, or some kind of modal element for modal dialogue boxes?

I don’t know; I’m not an app developer. But at least HTML is a “living standard,” and so these can be added if strong enough use cases are presented to the Working Group.

I think most coders would welcome a new way to embed images that respond to the device’s context. Borrowing from the video element, which displays source video according to what media queries instruct, I can imagine a new element such as picture:

1
<picture alt="angry pirate">
2
   <source src=hires.png media="min-width:800px">
3
   <source src=midres.png media="min-width:480px">
4
   <source src=lores.png>
5
      <!-- fallback for browsers without support -->
6
      <img src=midres.png alt="angry pirate">
7
</picture>
This would pull in hires.png for widescreen devices, midres.png for devices between 480 and 800 pixels wide, and lores.png for everything else, thereby rendering moot the question that designers currently ask themselves, “Do I make every browser download a high-resolution image and then squash it down for small screens, thus wasting bandwidth, or do I send a low-resolution image to every browser and scale it up for big screens, potentially sacrificing quality?”

Taking a leaf from the other popular semantics we’ve seen, there would be a fallback in the middle — in this case, a conventional img element — so everyone would get the right content.

Sending the right-sized image to devices without wasting bandwidth is one of the knottiest problems in cross-device and responsive design at the moment. Perhaps we’ll see a solution to this in HTML6. At the moment, the best solutions, which include Matt Wilcox’s Adaptive Images and Filament Group’s Responsive Images, require JavaScript and tweaks to the server’s htaccess file. The worst solutions require old-fashioned techniques, such as browser-sniffing, now rebranded as “device detection” but still the same old user-agent string-pattern matching, which is hilariously fragile, not future-proof or scalable, and straight out of the days of “Best viewed in Netscape Navigator at 800 × 600” badges on websites.

### Кто, где, когда?

A lot of data depends on three pieces of information: when, where and who?



HTML5 has a time element (which has been a bit of a battleground lately). This enables you to annotate a human-readable date with an unambiguous machine-readable one. It doesn’t matter what goes between the tags, because that’s the content for people to read. So, you could use either of the following:

1
<time datetime="1982-07-18">The day the woman I love was born</time>
2
 
3
<time datetime="1982-07-18">Priyanka Chopra’s birthday</time>
Whichever you choose, the machine would still know the date you mean because of the datetime attribute, formatted as YYYY-MM-DD. If you wanted to add a time, you could: separate the time from the date with a T, and then put the time in 24-hour format, terminated by a Z, along with any time-zone offset. So, 2011-11-13T20:00Z would be 8:00 pm on 13 November 2011 UTC, while 2011-11-13T23:26.083Z-05.00 would be 23:26 pm and 83 milliseconds in the time zone lying 5 hours before UTC. A Sri Lankan-localised browser could use this information to automatically convert dates into Buddhist calendar. Search engines could use timestamps to help evaluate “freshness”.

It’s perhaps surprising that, even though geolocation is so prevalent now, we don’t have a location element that simply takes three attributes: latitude, longitude and (optionally) altitude. It would be great to be able to write the following:

1
<location lat=51.502064 long=-0.131981>London SW1A 4WW</location>
The browser would then offer to show you a map or give you directions from the current GPS location or any other location-based service.

(Since I gave the talk that this article is based on, Ian Hickson, the HTML5 editor, said that he expects to add a new element. If I could choose, I’d prefer place, so I could wear a T-shirt with the slogan “I’ve got the time if you’ve got the place“.)

HTML3 had a person element, “used for names of people to allow these to be extracted automatically by indexing programs,” but it was never implemented. In HTML4, the cite element could be used to wrap names of people, but this has been removed in HTML5 — controversially (see “Incite a Riot” by Jeremy Keith). In HTML5, then, we’re left with no way to unambiguously denote a person. People’s names are, however, a hard problem to solve. Whereas times and dates have well-known standardized ISO formats (YYYY-MM-DD and HH:MM:SS.mmm, respectively), and location is always latitude, longitude and altitude, personal names are harder to break down into useful parts: there are Russian patronymics, Indonesian single-word names, multiple family names, and Thai nicknames to consider. (See Richard Ishida’s excellent article “Personal Names Around the World” for more information and discussion.)

The new data element, which replaces time, has a value attribute that passes machine-readable information, but it has no required or implied format, so there is no way for a browser or search engine to know, for example, whether 1936-10-19 is a date, a part number or a postal code.

## Микроданные

HTML5, like HTML4, is extensible (but not in the oh-so-dirty eXtensibility way of XML formats, so loathed by the Working Group). You can use the tried and tested microformats, which use HTML classes, or the full RDFa specification, which doesn’t validate in HTML4 or HTML5. Because RDFa was considered to be too hard for authors to write (Google has conducted research that finds that authors make 30% more mistakes with RDFa than with other formats), HTML5 specifies microdata, a mechanism for adding common semantics via agreed-upon markup patterns. HTML5 Doctor has more information on HTML5 microdata, and Opera 11.60 supports the Microdata DOM API.

Like microformats and RDFa, the extra semantics added to the markup make sense only if you have a cheat sheet that tells you what each piece means. This means that the data has to point to a vocabulary that tells any crawler how to interpret the lump of data it finds. For microdata, there is the newly established Schema.org, which is “a collection of schemas, i.e. HTML tags, that webmasters can use to mark up their pages in ways recognized by major search providers.”

## Действительно ли так важна семантика?

Now that more and more markup is generated by JavaScript, some people are tempted to think that semantics don’t matter. We see various products marketed as HTML5 which simply make divs fly around the screen with JavaScript  —  simple DHTML techniques unchanged from 10 years ago.

I’ve even seen some Web pages with no markup at all. Some frameworks emit skeletal HTML with empty body tags and inject all the HTML with script. If you’re squirting some minified JavaScript down the wire, with no markup at all, you’re closer to Flash than you are to the Web.

In the same way that 47 minutes is (apparently) too long to to struggle making a CSS layout, at which point you should just give up and use tables, some people suggest that thinking about which element to use is a waste of time. “There are two types of developers: those who argue about div’s not being semantic and those who create epic shit” writes Thomas Fuchs, as if the two activities were mutually exclusive.

A better argument is that no software cares about or consumes semantics anyway, so why bother? This isn’t true (work is underway already to map assistive technologies to new semantics), but even if it were true, it ignores that this is a chicken-and-egg argument. It assumes that no new search engine will ever come to the market and be able to use new elements, or that browsers will never release new versions that can make use of these semantics, and that developers will write no new extensions  —  in short, it assumes that the evolution of the Web is complete.

Semantics do matter. Semantics communicate meaning, and once that is established, machines can do something meaningful with that data, without having to develop and use algorithms to guess. A browser extension might allow a user to jump straight to the nav with a single keystroke. It can do this because it looks for nav rather than having to employ heuristics to find a div with an id or class that would suggest it’s being used as navigation (assuming the author decided to use something sensible like nav, navigation, sidebar, or menu  —  and a restaurant site with a div called “menu” might be a list of foods rather than other pages…ah, the ambiguity of natural language). A crawler might dynamically assemble articles on a timeline. There are many more possibilities than my meagre imagination can dream up.

The Web is based on simple technologies, mashed up together to bring surprising results  —  results which have certainly surpassed the inventors’ original intents or expectations. The Web will continue to do so. What makes the Web so great, so flexible and so powerful is the fact that content is in open formats that can be parsed and mashed up in new and surprising ways.

These can happen if the content is marked up for meaning by the author  —  and if the language has the right markup elements for authors to use as a vocabulary. HTML5 extends our vocabulary. We’ll need more words  —  and those will come about with HTML6 etc.

If, like me, you believe the Web to be a system that works across browsers, across operating systems, across devices, across languages, that is View-sourcable, hackable, mash-uppable, accessible, indexable, reusable, then we need to ensure that we use the small number of semantic tools at our disposal properly, and we’ll all benefit.

(Статья основана на докладе с конференции [Fronteers](http://fronteers.nl/congres/2011/sessions/html5-semantics-bruce-lawson).)

### Об авторе

Bruce evangelizes Open Web Standards for Opera. He wrote the book Introducing HTML5 together with Remy Sharp. The book points out the good and bad parts of HTML5 specifications and shows you how to use the language as well as some areas of spec will be discussed theoretically as they’re not yet implemented anywhere. It’s the first full-length book on HTML5 (New Riders, appearing in the 2nd edition).