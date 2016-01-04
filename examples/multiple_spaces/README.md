# Multiple Spaces Example

## How to Run

* Paste the following command inside your terminal:

```bash
echo "Checkout Repository"         && git clone git@github.com:contentful/contentful_jekyll_examples.git && \
echo "Go to This Example's Folder" && cd contentful_middleman_examples/examples/multiple_spaces && \
echo "Install Dependencies"        && bundle install && \
echo "Create Catalogue Space"      && contentful_bootstrap create_space my_catalogue --json-template bootstrap_templates/catalogue.json
```

* Open `~/.contentfulrc` and copy the following information into your `_config.yml` file:

```ini
; on ~/.contentfulrc

[my_catalogue]
CONTENTFUL_DELIVERY_ACCESS_TOKEN = <YOUR_TOKEN_WILL_BE_HERE>
SPACE_ID = <YOUR_SPACE_ID_WILL_BE_HERE>
```


```yml
# on _config.yml

- catalogue:
    space: <INSERT_SPACE_ID_CREATED_BY_BOOTSTRAP_HERE>
    access_token: <INSERT_ACCESS_TOKEN_CREATED_BY_BOOTSTRAP_HERE>
    cda_query:
      include: 2
```

* Paste the following command inside your terminal:

```bash
echo "Fetch Contentful Data" && jekyll contentful && \
echo "Start Jekyll Server"   && jekyll server
```

Then open your browser and go to: [localhost:4000](http://localhost:4000)

## Configuration

For reference of basic configuration, you can look into [single_content_type example](../single_content_type/README.md)

In this case we're using a extra configuration option not described in the previous example:

```yml
  cda_query:
    include: 2
```

This option customizes the query made to the Contentful API, see [contentful.rb](https://github.com/contentful/contentful.rb) for more info (look for filter options there). Note that by default only 100 entries will be fetched, this can be configured to up to 1000 entries using the `limit` option.

In this example we'll be using [Contentful Bootstrap](https://github.com/contentful/contentful-bootstrap.rb) for setting up our own Space with multiple Content Types, and fetching
the configuration from `~/.contentfulrc`

The template used is located [here](./example/bootstrap_templates/catalogue.json)

In this example we have two `contentful` extension activations.
