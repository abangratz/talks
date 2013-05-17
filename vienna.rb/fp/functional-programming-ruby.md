#Functional Programming for Ruby
---
#Authors
.fx: imageslide whiteheading

<image src="work_animals.jpg" />
---
---
#Andreas Kopecky

 @EvilBndy, <andreas.kopecky@gmail.com>

 * clean coder
 * programming language agnostic
 * mathemathics aficionado
---
#Anton Bangratz

@tony_xpro, <anton.bangratz@gmail.com>

 * XP enthusiast
 * TDDer
 * RoR nut

---
#Authors

 * working at RadarServices
 * love to learn new things

---
#Functional Programming
---
#λ calculus
---
#Why Functional Programming in Ruby
---
#Why?

 1. makes code cleared
 2. helps to decouple classes
 3. makes tests small and fast
---
#How to, then?
---
#Don't update variables
---

Don't:

    !ruby
    x = x + 1
    x += 1
	#...
    [1, 2, 3] << 4 << 5
	#...
    string.gsub!(...)

Do:

    !ruby
    y = x + 1
	#...
    [1, 2, 3] + [4, 5]
	#...
	result = string.gsub(...)
---
#Higher Order Functions
---
#Higher Order: map

Don't:

    !ruby
	words = []
	%w[some words].each do |word|
	  words << word.upcase
	end
	words #=> ["SOME", "WORDS"]

Do:

	!ruby
	words = %w[some words].map do |word|
	  word.upcase
	end #=> ["SOME", "WORDS"]
---
#Higher Order: inject

Don't:

	!ruby
	length = 0
	%w[some words].each do |word|
	  length += word.length
	end
	length #=> 9

Do:

	!ruby
	length = %w[some words].inject(0) do |sum, word|
	  sum + word.length
	end #=> 9

---
#Higher Order: select/reject

Don't:

	!ruby
	with_e = []
	%w[some words].each do |word|
	  with_e << word if word =~ /e/
	end
	with_e #=> ["some"]

Do:

	!ruby
	with_e = %w[some words].select do |word|
	  word =~ /e/
	end #=> ["some"]
	# ...

	!ruby
	without_e = %w[some words].reject do |word|
	  word =~ /e/
	end #=> ["words"]
---
#Higher Order:

Roll your own scan (prefix-sum):

    !ruby
	module Enumerable
	  def scan(initial=nil, sym=nil, &block)
		args = if initial then [initial] else [] end
		unless block_given?
		  args, sym, initial = [], initial, first unless sym
		  block = ->(acc, el) { acc.send(sym, el) }
		end
		[initial || first].tap {|res|
		  reduce(*args) {|acc, el|
			block.(acc, el).tap {|e|
			  res << e
			}
		  }
		}
	  end
	end

	p [1, 5, 8, 11, -6].scan(:+)
    # => [1, 6, 14, 25, 19]
---
#Functions as objects: Lambda and Proc

    !ruby
    square = ->(x) { x * x}
    square.(5) # => 25

	cube = Proc.new {|x| x * x * x }
	cube.(6) # => 216

---
#What's missing?
---
#Practical Usage
