title: Apostrophe, Quotation Marks and Prime Symbols
date: 2016-10-24

---

# TL;DR

In this article I'll talk about the right Unicode character for apostrophes and quotation marks. This note was made when dealing with the problem on the way curly quotes are rendered in CJK character set. Please reply if there are any question, mistake or volitaiton cpoyright.

<!--more-->

# Apostrophe & Quotes

First let's define the difference between apostrophes and quotation marks:

<table class="symbols">
    <thead>
        <tr>
            <th class="no-hyphens">Glyph</th>
            <th class="no-hyphens">Name</th>
            <th class="no-hyphens">Unicode</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <glyph>'</glyph>
            </td>
            <td>Apostrophe</td>
            <td class="unicode">U+0027</td>
        </tr>
        <tr>
            <td>
                <glyph>"</glyph>
            </td>
            <td>Quotation Mark</td>
            <td class="unicode">U+0022</td>
        </tr>
        <tr>
            <td>
                <glyph>
                    <quo>
                        <squo-push></squo-push>
                        <squo-pull>‘</squo-pull>
                    </quo>
                </glyph>
            </td>
            <td>Left Single Quotation Mark</td>
            <td class="unicode">U+2018</td>
        </tr>
        <tr>
            <td>
                <glyph>’</glyph>
            </td>
            <td>Right Single Quotation Mark</td>
            <td class="unicode">U+2019</td>
        </tr>
        <tr>
            <td>
                <glyph>ʼ</glyph>
            </td>
            <td>Modifier Letter Apostrophe</td>
            <td class="unicode">U+02BC</td>
        </tr>
        <tr>
            <td>
                <glyph>
                    <quo>
                        <dquo-push></dquo-push>
                        <dquo-pull>“</dquo-pull>
                    </quo>
                </glyph>
            </td>
            <td>Left Double Quotation Mark</td>
            <td class="unicode">U+201C</td>
        </tr>
        <tr>
            <td>
                <glyph>”</glyph>
            </td>
            <td>Right Double Quotation Mark</td>
            <td class="unicode">U+201D</td>
        </tr>
        <tr>
            <td>
                <glyph>′</glyph>
            </td>
            <td>Prime</td>
            <td class="unicode">U+2032</td>
        </tr>
        <tr>
            <td>
                <glyph>″</glyph>
            </td>
            <td>Double Prime</td>
            <td class="unicode">U+2033</td>
        </tr>
    </tbody>
</table>
<style type="text/css">
    table.symbols {
        border: 0;
        font-size: 100%;
        margin: 0 auto;
        margin-bottom: 1.5em;
        border-collapse: collapse;
        width: 75%;
        text-align: center ;
        table-layout: auto;
    }
    table.symbols th {
        font-family: 'Lato';
        font-weight: normal;
        text-transform: uppercase;
        font-size: 95%;
        padding: 0.3rem 0.5rem 0.3rem 0.5rem;
        line-height: 1.05;
        text-align: center;
        border: 0;
    }
    table.symbols td{
        padding: 0.4em;
        hyphens: none;
        text-align: center;
        border: 0;
        font-family: 'Lato';
    }
    table.symbols td + td {
        border-left: 1px solid #ccc;
    }
    table.symbols glyph {
        margin-left: 0.2em;
        margin-right: 0.2em;
        position: relative;
        bottom: -0.0em;
        font-weight: bolder;
        font-size: 180%;
        line-height: .70;
        top: 0.0rem;
        font-family: "Times New Roman Bold";
    }
</style>

An apostrophe is only used within or at the very end of a word - it is part of the word. [^1]

>The apostrophe ( `’` or `'` ) character is a punctuation mark, and sometimes a diacritical mark, in languages that use the Latin alphabet and some other alphabets. In English it is used for several purposes:
>    * The marking of the omission of one or more letters (as in the contraction of do not to don't).
>    * The marking of possessive case (as in the eagle's feathers, or in one month's time).
>    * The marking of plurals of individual characters (e.g. p's and q's, three a's, four i's, and two u's, Oakland A's). [^2]

Single quotes are only used around words - they come in pairs, and are not part of any word.

>Single or double quotation marks denote either speech or a quotation. [^3]

Seems easy, right? And you may notice that there are 2 similar symbols `'` `’ ` both used for apostrophes. Moreover, there are more similar symbol like prime symbols `′` `″`, straight quotation marks `'` `"`, left curly quotation marks `‘` `“`, right curly quotation marks `’` `”`. Confused?

You can copy and search these symbols on [Unicode® character table](http://unicode-table.com/en/) for clearly glyphs and technical informations such as Unicode number. They are all different symbols except `'` for apostrophe and `'` for straight quotation marks. I'll talk about it in the following separate topics.

# Straight Quotation Marks & Curly Quotation Marks

Techincally, the quotation mark key left side the Enter (or Return) key in a standerd QWERTY keyboard is for straight quotation marks. There are two ways to input a curly quotation mark, using smart quotes functions in word processer such as M$ Word, or using Unicode or GBK number to input. So what's the difference between them?

In short, the straight quotation marks are created for typewriter to replace both the left and right curly quotation marks in order to reduce the number of keys. So which one should I use? Curly quotation marks PLEASE.

>Word processors are not limited in this way. You can always get curly quotes. Compared to straight quotes, curly quotes are more legible on the page and match the other characters better. Therefore, straight quotes should never, ever appear in your documents. [^4]
>
>![](https://i.imgur.com/nbeNbqg.png)

ps. This aritcle has a far more better elaboration than mine on this sub-topic, I mean it, really. Please read it, you will benift from it.

# Straight or Curly Apostrophe?

>Historically, the apostrophe has always been typeset with a curved tail (’). Here are some of the first printed apostrophes, from the 1501 Italian text Le cose volgari di messer Francesco Petrarcha, printed by Aldus Manutius (the inventor of italic type): [^5]
>
>![](https://i.imgur.com/hpsX4uy.png)
>
>and from a 16th century French text:
>
>![ (Pictures from Odlie Piton, Hélène Pignot, “Mind your p’s and q’s?”: or the peregrinations of an apostrophe in 17th century English, February 2010.)
](https://i.imgur.com/aPWdNNO.png)

Then the typewriter came out, same reason like above, the curly apostrophe was replaced by straight quotation mark. Yes, not only the curly single quotation mark is replaced by straight single quotation mark, so is curly apostrophe mark. And in fact the curly apostrophy and the curly single left quotation mark has the same glyphs and the same Unicode number (U+2019).

>Now, Unicode was designed according to ten design principles ([PDF](http://www.unicode.org/versions/Unicode6.2.0/ch02.pdf)), two of which are plain text: “Unicode characters represent plain text” (“Plain text must contain enough information to permit the text to be rendered legibly, and nothing more”), and unification: “Unicode unifies duplicate characters within scripts across language”. However, there was already a very large body of ASCII text using the same straight apostrophe character as apostrophe and as left and right single quotes, and a large body of Windows-1252 text with different codes for straight apostrophe and curly apostrophe. So these principles were overridden in this case by the more important principle of convertibility: “accurate convertibility is guaranteed between Unicode and other widely accepted standards”.
>
>Hence we have U+0027 `'`, the ASCII-compatible straight apostrophe, which is rendered with a typewriter-like neutral glyph usable as both left and right single quote, and U+2019 `’`, the curly right single quote. Since languages and legacy systems do not distinguish between how the apostrophe and the right single quote are written, encoded, or rendered,² there is no reason to include a third character for the apostrophe. It is the same character as U+2019, matching professional typographic conventions. The legacy U+0027 should really only be used to talk about programming `print 'Hello, world!'`, although outside of professional typography, [approximately nobody](https://www.quora.com/profile/Anders-Kaseorg) goes to the trouble of typing [U+2019](https://en.wikipedia.org/wiki/Quotation_mark#Typing_quotation_marks_on_a_computer_keyboard) when their editor doesn’t automatically make the replacement. [5]

# Prime Symbols

Finally, let's talk about prime symbols.

>The prime symbol `′`, double prime symbol `″`, triple prime symbol `‴`, quadruple prime symbol `⁗` etc., are used to designate units and for other purposes in mathematics, the sciences, linguistics and music. The prime symbol should not be confused with the apostrophe, single quotation mark, acute accent, or grave accent; the double prime symbol should not be confused with the double quotation mark, the ditto mark, or the letter double apostrophe. The prime symbol is very similar to the Hebrew geresh, but in modern fonts the geresh is designed to be aligned with the Hebrew letters and the prime symbol not, so they should not be interchanged. [^6]

>![](https://i.imgur.com/2005prS.png)
>Via Typographic literacy [^7]

But in some fonts these symbols are rendered to similar glyphs, such as Segoe and Microsoft YaHei which fallbacks to Segoe, which will be confused in small weight and low resolution.

![](https://i.imgur.com/tW167jd.png "From left to right: straight single quote, straight double quote, curly left single quote, curly right single quote (also for curly apostrophy), curly left double quote, curly right double quote, prime symbol, double prime symbol, triple prime symbol, quadruple symbol.")

「你学到了么？」  
「没有，滚。」

---

# References

[^1]: [punctuation - Apostrophe vs. Single Quote - English Language & Usage Stack Exchange](https://english.stackexchange.com/questions/36046/apostrophe-vs-single-quote)
[^2]: [Apostrophe - Wikiwand](https://www.wikiwand.com/en/Apostrophe)
[^3]: [Quotation mark - Wikiwand](https://www.wikiwand.com/en/Quotation_mark)
[^4]: [Straight and curly quotes | Butterick’s Practical Typography](http://practicaltypography.com/straight-and-curly-quotes.html)
[^5]: [Punctuation: Why is the right single quote (U+2019), and not the semantically distinct apostrophe (U+0027), the preferred apostrophe character in Unicode? - Quora](https://www.quora.com/Punctuation-Why-is-the-right-single-quote-U+2019-and-not-the-semantically-distinct-apostrophe-U+0027-the-preferred-apostrophe-character-in-Unicode)
[^6]: [Prime (symbol) - Wikiwand](https://www.wikiwand.com/en/Prime_(symbol))
[^7]: [KA+A | Blog : Typographic Literacy: Part Two](http://www.kaplusa.com/blog/2010/02/typographic-literacy-part-two/)
[^8]: [ASCII Codes - Table of ascii characters and symbols](http://ascii.cl/)