# SegmentTree

Ruby implementation of [segment tree](http://en.wikipedia.org/wiki/Segment_tree) data structure.
Segment tree is a tree data structure for storing intervals, or segments. It allows querying which of the stored segments contain a given point. It is, in principle, a static structure; that is, its content cannot be modified once the structure is built.

Segment tree storage has the complexity of <tt>O(n log n)</tt>.
Segment tree querying has the complexity of <tt>O(log n + k)</tt> where <tt>k</tt> is the number of reported intervals.

It's pretty fast on querying trees with ~ 10 millions segments, though building of such big tree will take long.

## Installation

Add this line to your application's Gemfile:

    gem 'segment_tree'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install segment_tree

## Usage

Segment tree consists of segments (in Ruby it's <tt>Range</tt> objects) and corresponding values. The easiest way to build a segment tree is to create it from hash where segments are keys:
```ruby
tree = SegmentTree.new(1..10 => "a", 11..20 => "b", 21..30 => "c") # => #<SegmentTree:0xa47eadc @root=#<SegmentTree::Container:0x523f3b6 @range=1..30>>
```

After that you can query the tree of which segments contain a given point:
```ruby
tree.find(5) # => [#<SegmentTree::Segment:0xa47ea8c @range=1..10, @value="a">]
```

Or fetch only one segment:
```ruby
segment = tree.find_first(5) # => #<SegmentTree::Segment:0xa47ea8c @range=1..10, @value="a">
segment.value # => "a"
```

## Real world example

Segment tree can be used in applications where IP-address geocoding is needed.

```ruby
data = [
  [IPAddr.new('87.224.241.0/24').to_range, {:city => "YEKT"}],
  [IPAddr.new('195.58.18.0/24').to_range, {:city => "MSK"}]
  # and so on
]
ip_tree = SegmentTree.new(data)

client_ip = IPAddr.new("87.224.241.66")
ip_tree.find_first(client_ip).value # => {:city=>"YEKT"}
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## TODO
1. Fix README typos and grammatical errors (english speaking contributors are welcomed)
2. Implement C binding for MRI.
3. Test on different versions of Ruby.

## LICENSE
Copyright (c) 2012 Alexei Mikhailov

MIT License

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.