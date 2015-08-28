---
layout: project
title:  "NgBankParser"
date:   2015-08-20 06:30:00
language: "Ruby on Rails"
summary: "We created a parser that returns formatted data from Nigerian bank statements"
github: "https://github.com/devcenter-square/ng-bank-parser"
completed: true
color_id: 2
---

# Ng::Bank::Parser

## Installation

Add this line to your application's Gemfile:

{% highlight ruby %}
gem 'ng-bank-parser'
{% endhighlight %}

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install ng-bank-parser

## Usage

Using the gem is pretty straightforward and simple.
{% highlight ruby %}
result = NgBankParser::Router.parse(bank_key, file_path, password)
{% endhighlight %}

`bank_name` is the name key of the bank that statement is from. There's a list of supported banks and formats below.

`file_path` is obviously where the file you're trying to parse exists.

`password` *(optional)* it's only required when the file you want to parse is password protected.

`result` is a hash that contains all the information you need from your statment.

{% highlight ruby %}
result = {
    status: 1,
    data: {
        bank_name: the_bank_name,
        account_number: the_account_number,
        account_name: the_account_name,
        from_date: first_transaction_date,
        to_date: last_transaction_date,
        transactions: an_array_of_transaction_hashes
    }
}
{% endhighlight %}

`:status` can either be 1 or 0. 1 for when the parsing is succesful and 0 for when it's not. A status of 0 is accompanied with an error message that aims to clarify why it could not parse the file.

{% highlight ruby %}
result = {
    status: 0,
    message: "RELEVANT ERROR MESSAGE"
}
{% endhighlight %}

Furthermore, `:transactions` in the `result` hash is an array of hashes. Below is an example of a transaction hash

{% highlight ruby %}
transaction = {
    date: transaction_date,
    amount: transaction_amount,
    type: debit_or_credit,
    balance: balance_after_transaction,
    remarks: remarks,
    ref: reference_id, # as provided by the statment
}
    
{% endhighlight %}

## List of Supported Banks

United Bank for Africa: 
- key: uba
- supported formats: pdf

Guaranty Trust Bank: 
- key: gtb
- supported formats: xls, xlsx
    
First Bank: 
- key: firstbank
- supported formats: pdf

## Contributing

Documentation on contribution can be found in the contribution wiki

## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).


