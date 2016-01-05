# Factory Girl

[Factory Girl Rails](https://github.com/thoughtbot/factory_girl_rails) is a fixture replacement (not that we've learned what fixtures are). Basically what it does is allows you to define `ActiveRecord` object presets, then use the `FactoryGirl` syntax to initialize or create those object(s) at any time and with additional attribute definitions. Each preset is called a "factory". To install add the gem to the `development` and `test` environments to your `Gemfile`:

    gem "factory_girl_rails"

Add the following line within the `config` block in `spec_helper.rb`
```ruby
config.include FactoryGirl::Syntax::Methods
```
Next create a file to define your factories,

    touch spec/factories.rb

Within this file lets define our first factory for a Book model
```ruby
FactoryGirl.define do
  factory :book do
    name "House of Leaves"
    author "Mark Z. Danielewski"
    description "House of Leaves is the debut novel by the American author Mark Z. Danielewski, published by Pantheon Books. The novel quickly became a bestseller following its release on March 7, 2000. It was followed by a companion piece, The Whalestoe Letters"
  end
end
```

Now within our specs we can use the FactoryGirl syntax to create this Book object, which will be an ActiveRecord Book object that we defined in `app/models/book.rb`. FactoryGirl is just storing the default values.
```ruby
require 'spec_helper'

describe Book do

  describe "validations" do
    it "is valid" do
      expect(create(:book)).to be_valid
    end

    it "is invalid without a name" do
      expect(build(:book, name: nil)).to be_invalid
    end

  end
end
```

The `create` and `build` methods are going to be the most common FactoryGirl methods, these methods accept the same argument, but create will attempt to save the record, while build will not. The first argument is the name of the factory, which is the symbol after `factory` in the `factories.rb`, the next argument is an optional hash, where you can pass in additional attributes or attributes to override on the creation of the object.

This is a great resource to use to investigation more with Factory Girl.
[Factory Girl Getting Started](http://www.rubydoc.info/gems/factory_girl/file/GETTING_STARTED.md)