#Gems I Like and Use
#Presenter Notes
A short overview

---
# try_to

---
# An Alternative to 'Object#try'

---
# Advantages

---
# 1. Lexical Closures (blocks)

## Old style:

    !ruby
    object.try(:method).try(:method)...

## New (and shiny!):
    !ruby
    try_to { model.chain.method } # => nil

---
# 2. Customizable Returns

## Value:

    !ruby
    try_to(42) { 2.bar } # => 42

## Handler:

    !ruby
    try_to ( -> e { puts e.class } ) { 2.bar } # => "NoMethodError"

---
# 3. Customize Exceptions to Handle

    !ruby
    TryTo.exceptions << ZeroDivisionError
    try_to { 1/0 } # => nil ; no exception raised

---
# 4. Add Handlers for Exception Classes

    !ruby
    TryTo.add_handler( ZeroDivisionError, -> _ { puts "Sorry!" } )
    try_to { 1/0 } # prints "Sorry!"

    TryTo.add_handler( NoMethodError, 42)

    try_to { 1.bar } # => 42

---
# 5. Add Default Handler

    !ruby
    TryTo.default_handler = lambda { |_| puts "Ooooo shiny!" }
    try_to { 1.zap } # prints "Ooooo shiny!"

---
# Credits

## Michael Kohl (https://github.com/citizen428)
## Sergey Gopkalo (https://github.com/sevenmaxis/)
---
# Again, Why?

* Doesn't pollute `Object`
* Ease of use
* Easy configuration
* Sane defaults
* Covers more than 'returns nil' or `NoMethodError`

---
#Me

## https://github.com/abangratz
## https://abangratz.github.io/
## anton.bangratz@radarservices.com
## twitter: @tony_xpro

&copy; by Anton Bangratz

This work is licensed under a Creative Commons Attribution-ShareAlike 4.0 International License.
(http://creativecommons.org/licenses/by-sa/4.0/legalcode)
