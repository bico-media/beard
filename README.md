Status: _idea_ → _lose draft_ → _draft_ → __proposal__ → _final review_ → _stable_

# Mustache for blockchain content

> Let's get a common way of engaging mustache templating for dynamic content from the blockchain.

This document describes the protocol "B://eard" (pronounced beard). Please share [inputs and comments](https://github.com/bico-media/beard/issues/new).

## Introduction 

Templating is a common way of merging data with structure. The [Mustache](https://mustache.github.io/) has a simple syntax and (almost) no logic but have proven tremendously useful in many areas with its simplicity and easy learning curve.



## Description

The B://eard protocol lets content creators use [Mustache](https://mustache.github.io/) as a templating engine for blockchain data and is inspired by the [B://emplate idea](http://bemplate.bico.media) model D.

In the following, we will use `main data object` to refer to the data context in which a Mustache template engine will run.

### Definition

If you provide content from the blockchain you are compatible with the B://eard protocol if you:

- Make sure content containing a key text like `{{[abc]=B://[TX]}}`
  - will have the key text removed 
  - a `main data object` will be populated with a property named `abc` containing 
    - the [HJSON](http://hjson.org/) parsed content from the target TX 
    - if HJSON parsing fails, `abc` will contain a string with the full content of the target tx.
  - Rerun until no more key texts exist in the content.

- Make sure content containing the key text `{{mustache=B://}}` 
  - Will have the key text and any similar key texts removed 
  - The templating engine [Mustache](https://mustache.github.io/) will be initiated with the `main data object` as input and the current content as template. 

All key texts are case insensitive.

### Example:

The following content 

```
{{mustache=B://}}
{{intro=B://9b2542900e789935e2810e04838de81ade72b883d66ab68a1ead91fad66ec9fb}}
{{foobar=B://9c2619fae7b5cbe8b510c1a771606a55cdf6a352e8febc936ed7de78fee4fba5}}
<h3>{{intro}}</h3>
<ul>
{{#foobar.products}}
<li>{{name}} - price: {{price}}
{{/foobar.products}}
</ul>
```

Will produce

```





<h3>My shop!</h3>

<ul>
<li>Knife - price: 2.25
<li>Spoon - price: 2.5
<li>Fork - price: 2.99
</ul>
```

## Implementations

Known implementations:

- [Bico.Media](//bico.media) supports the B://eard protocol.

----

Please share [inputs and comments](https://github.com/bico-media/beard/issues/new).
