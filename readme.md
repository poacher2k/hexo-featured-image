# Hexo Featured Image

A Hexo plugin to allow adding featured images with `featured_image` in front-matter and using it in post and/or have it output in the content.json if used together with [hexo-generator-json-content](https://github.com/alexbruno/hexo-generator-json-content).

`thumbnail` is also supported, and works the same as `featured_image`.

For example:

`CoolPost.md`

    ---
    title: Cool post
    featured_image: my_img.png
    thumbnail: my_img_thumbnail.png
    ---
    What a cool blog I have!

By using the Hexo Front Featured Image plugin, you can specify a post's featured image in its front matter.

The absolute path to `my_img.png` will be available through `page.featured_image` in your templates.

For example:

`article.ejs`

    ...
    <% if (page.featured_image){ %>
        <img src="<%- page.featured_image %>">
    <% } %>
    ...

## Installation

    npm install --save hexo-featured-image

or
yarn add hexo-featured-image

## Usage

This plugin will make automatically make `page.featured_image` available in your templates when you run `hexo server` or `hexo generate`.

If you are using [hexo-generator-json-content](https://github.com/alexbruno/hexo-generator-json-content), it will automatically add the `featured_image` property to `content.json` when you run `hexo generate` and when you **exit** `hexo server`.

## Configuration

### URL

For this plugin to work correctly, you must set `url` to your URL in `_config.yml`. For example, if you are working locally using the default url (http://0.0.0.0:4000/), set it like this:

`_config.yml`

    ...
    # URL
    url: http://0.0.0.0:4000/
    ...

or enable `absolute_path_reference` in the options.

### post_asset_folder

This plugin works without configuration if you are using absolute or relative URI's, [post asset folders](https://hexo.io/docs/asset-folders.html), or you are storing your images in `source/images`.

If you are not using post asset folders, and you prefer to store your images somewhere else than in `source/images`, you must specify `image_dir` in `_config.yml` to wherever you store your images. To set your image directory to `source/assets`, you would set `image_dir: assets` in `_config.yml`. Example:

`_config.yml`

    ...
    # Directory
    source_dir: source
    public_dir: public
    ...
    image_dir: assets
    ...

### [hexo-generator-json-content](https://github.com/alexbruno/hexo-generator-json-content)

This plugin plays nicely with [hexo-generator-json-content](https://github.com/alexbruno/hexo-generator-json-content), and will output the absolute path of `featured_image` to `content.json` if `featured_image` has been set to `true` in the `jsonContent` configuration part of `_config.yml` like so:

    ...
    jsonContent: {
    	...
        posts: {
        	...
            featured_image: true
            thumbnail: true # if you want thumbnail to be added as well
        }
    }

## Options
Add or modify the following section to your root `_config.yml` file

``` yaml
featured_image:
  absolute_path_reference: true
```

- **absolute_path_reference**: Make your featured_image URL relative to the root of the website (i.e. they will not contain `url`)
  - default: false
