
## michyamrane.github.io

My personal website.

####  Dependencies

- **[Jekyll]**: *simple, blog-aware static site generator*
- **[Waline]**: *simple, Safe Comment System inspired by Valine*
- **[Umami]**: *simple, fast, website analytics alternative to Google Analytics*

#### Prerequisites
- [Vercel  account] : *Deploy Waline & Umami*
- [Leancloud  account] : *Database for Waline*
- [Heroku account] : *Database for Umami*

### Development

Install jekyll and bundler:
```bash
gem install jekyll bundler
```

Install gems:
```bash
bundle install
```

Build and serve locally with:
```bash
bundle exec jekyll serve --host 0.0.0.0
```

The site should now be available at http://0.0.0.0:4000/ on your local machine, and your local machine's IP address on your network—great for testing on mobile OSes.

[Jekyll]: https://github.com/jekyll/jekyll
[Waline]: https://github.com/walinejs/waline
[Umami]: https://github.com/mikecao/umami
[Leancloud  account]: https://leancloud.app
[Vercel  account]: https://vercel.com
[Heroku account]: https://www.heroku.com
