# Custom Mapper Example

## How to Run

* Paste the following command inside your terminal:

```bash
echo "Checkout Repository"         && git clone git@github.com:contentful-labs/contentful_middleman_examples.git && \
echo "Go to This Example's Folder" && cd contentful_middleman_examples/examples/custom_mapper && \
echo "Install Dependencies"        && bundle install && \
echo "Fetch Contentful Data"       && bundle exec rake contentful && \
echo "Start Jekyll Server"         && jekyll server
```

Then open your browser and go to: [localhost:4000](http://localhost:4000)

## Configuration

For reference of basic configuration, you can look into [single_content_type example](../single_content_type/README.md)

In this case we're using a extra configuration option not described in the previous example:

```yml
  content_types:
    link: MyReverseMapper
```

This option customizes the Mapper used for fetching the entry data. In this case, mapping all `link` type entries using the [`MyReverseMapper` mapper](./example/_plugins/my_reverse_mapper.rb).
This mapper duplicates the data storing it in a field with it's name reversed:

```ruby
class MyReverseMapper < Jekyll::Contentful::Mappers::Base
  def map
    result = super
    result.keys.each do |name|
      result[name.reverse] = result[name]
    end

    result
  end
end
```

## Caveats

Jekyll itself only allows to import code as plugins only for it's recognized plugin entry points.
Therefore we are using a custom [Rakefile](./example/Rakefile) to import the mapper and required files:

```ruby
require 'jekyll'
require 'jekyll-contentful-data-import'
require './_plugins/mappers'

desc "Import Contentful Data with Custom Mappers"
task :contentful do
  Jekyll::Commands::Contentful.process([], {}, Jekyll.configuration['contentful'])
end
```

