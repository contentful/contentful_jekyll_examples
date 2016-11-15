# Single Content Type Example

## How to Run

Paste the following command inside your terminal:

```bash
echo "Checkout Repository"         && git clone git@github.com:contentful/contentful_jekyll_examples.git && \
echo "Go to This Example's Folder" && cd contentful_jekyll_examples/examples/single_space/example && \
echo "Install Dependencies"        && bundle install && \
echo "Fetch Contentful Data"       && bundle exec jekyll contentful && \
echo "Start Jekyll Server"         && bundle exec jekyll server
```

Then open your browser and go to: [localhost:4000](http://localhost:4000)

## Configuration

```yml
contentful:
  spaces:
    - links:
        space: 3fwy09k2gc9g
        access_token: 25f513e34e33916336bba1d740d135035d4e1d63b87fc446da374fec3aaccaca
```

In [`_config.yml`](./example/_config.yml) you will find the above cited configuration block. Let's go through it line by line:

* `contentful:`                  - Enables Contentful Extension
* `  spaces:`                    - Tells the Extension to consider the following elements as a Space
* `    - links:`                 - Creates a `links` Space reference, so that it can be used via that name on the views
* `      space: 3fwy09k2gc9g`    - Sets the Space ID
* `      access_token: 25f5...`  - Sets the Space Access Token

## Views

```django
  <ul class="post-list">
    {% for link in site.data.contentful.spaces.links.link %}
      <li>
        <h2><a href="{{ link.url | url }}">{{ link.websiteName }}</a></h2>
      </li>
    {% endfor %}
  </ul>
```

In [example/index.html](./example/index.html) you will find the above cited template code. Let's analyze the important bits:

* `site.data.contentful.spaces` - Will contain a method for each Space you have defined, in this case `links`
* Each Space will be a collection of entries fetched for it, each entry will have an ID and the Data
