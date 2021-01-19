source "https://rubygems.org"


#gem "github-pages", group: :jekyll_plugins
#gem "kramdown-parser-gfm", "~> 1.1.0"
gem "jekyll", ">= 4.1.0", "< 5.0"
#gem "jekyll", "~> 3.9"

# plugins
group :jekyll_plugins do
  gem "jekyll-paginate"
  gem "jekyll-redirect-from"
  gem "jekyll-seo-tag"
  gem "jekyll-archives"
  gem "jekyll-sitemap"
  gem "jekyll-coffeescript"
  gem "jekyll-default-layout"
  gem "jekyll-gist"
  gem "jekyll-github-metadata"
  gem "jekyll-optional-front-matter"
  gem "jekyll-readme-index"
  gem "jekyll-titles-from-headings"
  gem "jekyll-relative-links"
end

group :test do
  gem "html-proofer"
end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
install_if -> { RUBY_PLATFORM =~ %r!mingw|mswin|java! } do
  gem "tzinfo", "~> 1.2"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.1", :install_if => Gem.win_platform?
