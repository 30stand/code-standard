# Clarification regarding the usage of `eval()`:

I will start with Nicholas C. Zakas's [article](http://www.nczonline.net/blog/2013/06/25/eval-isnt-evil-just-misunderstood/), the main purpose of his article is to justify his use of `eval()` in the [CSSLint](https://github.com/CSSLint/parser-lib/blob/master/src/css/PropertyValuePart.js#L145), he uses `eval()` to parse CSS, a method that I agree too, he also mentioned Douglas Crockford also uses `eval()` to parse JSON to support his stand.

Which means this article is not aim for justifying the **general uses** of `eval()`, Nicholas himself don't think it's good to use `eval()`, too.

> I’m not saying you should go run out and start using `eval()` everywhere. In fact, there are **very few** good use cases for running eval() at all. There are definitely **concerns with** code **clarity**, **debugability**, and certainly **performance** that should not be overlooked. But you shouldn’t be afraid to use it when you have a case where eval() makes sense. Try not using it first, **but don’t let anyone scare you** into thinking your code is more fragile or less secure **when eval() is used appropriately**.

Then under what circumstances using `eval()` can be considered appropriate?

One, of course, is when you are using it to create a parser, using regular expressions as filters. Another is when processing data input that is not from the user according to the author.

> Once again, if you are taking user input and passing it through `eval()` in some way, then you are asking for trouble. Never ever do that. However, if your use of `eval()` has input that only you control and cannot be modified by the user, then there are no security risks.

<!--  -->

> In short, `eval()` doesn’t open you up to man-in-the-middle attacks any more than loading external JavaScript does. If you can’t trust the code from your server then you have much bigger problems than an `eval()` call here or there.

Nicholas is arguing when dealing **trusty** server inputs, `eval()` does not make your codes more dangerous, in the meantime he agrees use `eval()` with use inputs are stupid.

**I don't agree with him about this trust**.

There is one type of XSS attack called **persistent XSS**. In short the attacker does not need to use man-in-the-middle attacks to plant his bomb, the bomb can be smuggled in by a  nick name field, or an avatar url field in your website sign up form, for example. The code will be injected to the database, once the page requests the data, and `eval()` the injected field values, the code will be executed.

Why use `eval()` when we have safer options?

> One can not be too careful

Having additional wall is always better, for example, to use `JSON.parser()` instead of `eval()` to process JSON strings, even you think you can trust the inputs from that server.

Clearly, we are not writing any parsers, also I don't think those few good cases to use `eval()` exists in our development, in conclusion, we should not use `eval()` at all due to the concerns with code clarity, debug-ability, performance and security.

> Don't be eval
