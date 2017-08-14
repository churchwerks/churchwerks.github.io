---
layout: post
title:  "Mixing Integers and Floats"
date:   2017-08-14 15:24:03 -0400
---


Ruby has a Numbers Class from which all Numbers are derived. This blog post is about my experience using two types of numbers  (Integers and Floats)

## Ruby's Numeric Class

All numbers in Ruby are derived from the Numeric class from which all higher-level numeric classes should inherit. [Numeric](http://ruby-doc.org/core-2.4.1/Numeric.html)

Ruby is a Very! forgiving language. It will allow you to mix and match numeric types to your heart's content and if it can figure out a way to do so, it will. However this may have unintended consequences if you are not aware of what is happening behind the scenes as I found ou while completing the [oo-cash-register-v-000](https://learn.co/tracks/full-stack-web-dev-with-react/object-oriented-ruby/object-labs/oo-cash-register) lab.

### OO Cash Register

So this lab had us modeling a very simple cash register. It was very test driven, (in other words not a lot of info given in the lab write up, of what the program was expected to contain; but, if you were carefull in reading the test output, you coud get all of the Rspec tests to pass. Now normally, I love the challenge of writing my program code this way. In fact I now hardly ever read the lab instructions at all in the begining. I just fork the lab, and clone it down to my local development environment, (iMac, Atom, iTerm2). Then I run Learn and read the first failing test, refactor my code and then start running single tests using the Learn --fail-fast command like so:

```Ruby
[15:59:20] (master) oo-cash-register-v-000
// ♥ learn

CashRegister
  ::new
    sets an instance variable @total on initialization to zero (FAILED - 1)
    optionally takes an employee discount on initialization (FAILED - 2)
  #total
    returns the current total (FAILED - 3)
  #add_item
    accepts a title and a price and increases the total (FAILED - 4)
    also accepts an optional quantity (FAILED - 5)
    doesn't forget about the previous total (FAILED - 6)
  #apply_discount
    the cash register was initialized with an employee discount
      applies the discount to the total price (FAILED - 7)
      returns success message with updated total (FAILED - 8)
      reduces the total (FAILED - 9)
    the cash register was not initialized with an employee discount
      returns a string error message that there is no discount to apply (FAILED - 10)
  #items
    returns an array containing all items that have been added (FAILED - 11)
  #void_last_transaction
    subtracts the last transaction from the total (FAILED - 12)

Failures:

  1) CashRegister ::new sets an instance variable @total on initialization to zero
     Failure/Error: let(:cash_register) { CashRegister.new }

     NameError:
       uninitialized constant CashRegister
     # ./spec/cash_register_spec.rb:2:in `block (2 levels) in <top (required)>'
     # ./spec/cash_register_spec.rb:7:in `block (3 levels) in <top (required)>'

  2) CashRegister ::new optionally takes an employee discount on initialization
     Failure/Error: let(:cash_register_with_discount) { CashRegister.new(20) }

     NameError:
       uninitialized constant CashRegister
     # ./spec/cash_register_spec.rb:3:in `block (2 levels) in <top (required)>'
     # ./spec/cash_register_spec.rb:11:in `block (3 levels) in <top (required)>'

  3) CashRegister #total returns the current total
     Failure/Error: let(:cash_register) { CashRegister.new }

     NameError:
       uninitialized constant CashRegister
     # ./spec/cash_register_spec.rb:2:in `block (2 levels) in <top (required)>'
     # ./spec/cash_register_spec.rb:17:in `block (3 levels) in <top (required)>'

  4) CashRegister #add_item accepts a title and a price and increases the total
     Failure/Error: let(:cash_register) { CashRegister.new }

     NameError:
       uninitialized constant CashRegister
     # ./spec/cash_register_spec.rb:2:in `block (2 levels) in <top (required)>'
     # ./spec/cash_register_spec.rb:24:in `block (4 levels) in <top (required)>'
     # ./spec/cash_register_spec.rb:24:in `block (3 levels) in <top (required)>'

  5) CashRegister #add_item also accepts an optional quantity
     Failure/Error: let(:cash_register) { CashRegister.new }

     NameError:
       uninitialized constant CashRegister
     # ./spec/cash_register_spec.rb:2:in `block (2 levels) in <top (required)>'
     # ./spec/cash_register_spec.rb:28:in `block (4 levels) in <top (required)>'
     # ./spec/cash_register_spec.rb:28:in `block (3 levels) in <top (required)>'

  6) CashRegister #add_item doesn't forget about the previous total
     Failure/Error: let(:cash_register) { CashRegister.new }

     NameError:
       uninitialized constant CashRegister
     # ./spec/cash_register_spec.rb:2:in `block (2 levels) in <top (required)>'
     # ./spec/cash_register_spec.rb:32:in `block (3 levels) in <top (required)>'

  7) CashRegister #apply_discount the cash register was initialized with an employee discount applies the discount to the total price
     Failure/Error: let(:cash_register_with_discount) { CashRegister.new(20) }

     NameError:
       uninitialized constant CashRegister
     # ./spec/cash_register_spec.rb:3:in `block (2 levels) in <top (required)>'
     # ./spec/cash_register_spec.rb:44:in `block (4 levels) in <top (required)>'

  8) CashRegister #apply_discount the cash register was initialized with an employee discount returns success message with updated total
     Failure/Error: let(:cash_register_with_discount) { CashRegister.new(20) }

     NameError:
       uninitialized constant CashRegister
     # ./spec/cash_register_spec.rb:3:in `block (2 levels) in <top (required)>'
     # ./spec/cash_register_spec.rb:50:in `block (4 levels) in <top (required)>'

  9) CashRegister #apply_discount the cash register was initialized with an employee discount reduces the total
     Failure/Error: let(:cash_register) { CashRegister.new }

     NameError:
       uninitialized constant CashRegister
     # ./spec/cash_register_spec.rb:2:in `block (2 levels) in <top (required)>'
     # ./spec/cash_register_spec.rb:55:in `block (4 levels) in <top (required)>'

  10) CashRegister #apply_discount the cash register was not initialized with an employee discount returns a string error message that there is no discount to apply
      Failure/Error: let(:cash_register) { CashRegister.new }

      NameError:
        uninitialized constant CashRegister
      # ./spec/cash_register_spec.rb:2:in `block (2 levels) in <top (required)>'
      # ./spec/cash_register_spec.rb:63:in `block (4 levels) in <top (required)>'

  11) CashRegister #items returns an array containing all items that have been added
      Failure/Error: new_register = CashRegister.new

      NameError:
        uninitialized constant CashRegister
      # ./spec/cash_register_spec.rb:70:in `block (3 levels) in <top (required)>'

  12) CashRegister #void_last_transaction subtracts the last transaction from the total
      Failure/Error: let(:cash_register) { CashRegister.new }

      NameError:
        uninitialized constant CashRegister
      # ./spec/cash_register_spec.rb:2:in `block (2 levels) in <top (required)>'
      # ./spec/cash_register_spec.rb:79:in `block (3 levels) in <top (required)>'

Finished in 0.00642 seconds (files took 0.35046 seconds to load)
12 examples, 12 failures

Failed examples:

rspec ./spec/cash_register_spec.rb:6 # CashRegister ::new sets an instance variable @total on initialization to zero
rspec ./spec/cash_register_spec.rb:10 # CashRegister ::new optionally takes an employee discount on initialization
rspec ./spec/cash_register_spec.rb:16 # CashRegister #total returns the current total
rspec ./spec/cash_register_spec.rb:23 # CashRegister #add_item accepts a title and a price and increases the total
rspec ./spec/cash_register_spec.rb:27 # CashRegister #add_item also accepts an optional quantity
rspec ./spec/cash_register_spec.rb:31 # CashRegister #add_item doesn't forget about the previous total
rspec ./spec/cash_register_spec.rb:43 # CashRegister #apply_discount the cash register was initialized with an employee discount applies the discount to the total price
rspec ./spec/cash_register_spec.rb:49 # CashRegister #apply_discount the cash register was initialized with an employee discount returns success message with updated total
rspec ./spec/cash_register_spec.rb:54 # CashRegister #apply_discount the cash register was initialized with an employee discount reduces the total
rspec ./spec/cash_register_spec.rb:62 # CashRegister #apply_discount the cash register was not initialized with an employee discount returns a string error message that there is no discount to apply
rspec ./spec/cash_register_spec.rb:69 # CashRegister #items returns an array containing all items that have been added
rspec ./spec/cash_register_spec.rb:78 # CashRegister #void_last_transaction subtracts the last transaction from the total
```

So it looks pretty daunting so lets take it step by step. Here is what the lab instructions said:

>Follow along with the specs in `spec/cash_register_spec.rb`. Reading along with what the tests are looking for can be really helpful!

So lets take it one step at a time!

```Ruby
CashRegister
  ::new
    sets an instance variable @total on initialization to zero (FAILED - 1)

Failures:

  1) CashRegister ::new sets an instance variable @total on initialization to zero
     Failure/Error: let(:cash_register) { CashRegister.new }

     NameError:
       uninitialized constant CashRegister
     # ./spec/cash_register_spec.rb:2:in `block (2 levels) in <top (required)>'
     # ./spec/cash_register_spec.rb:7:in `block (3 levels) in <top (required)>'

Failed examples:

rspec ./spec/cash_register_spec.rb:6 # CashRegister ::new sets an instance variable @total on initialization to zero
```

So the above are the hints that the Rspec file is giving us with regards to the first failing test. So lets work on trying to get it to pass.

Here is the contents of the cash_register.rb file contents when this Rspec was run.
`require "pry"`. That's it. Obviously we need to add more code. Lets try this given the hints above.

```Ruby
require 'pry'
class CashRegister
  attr_accessor :total

  def initialize
    @total = 0.00
  end
```

