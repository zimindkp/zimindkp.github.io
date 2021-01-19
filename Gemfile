source "https://rubygems.org"


gem "github-pages", group: :jekyll_plugins
#gem "kramdown-parser-gfm", "~> 1.1.0"
#gem "jekyll", ">= 4.1.0", "< 5.0"
#gem "jekyll", "~> 3.9"

# plugins
group :jekyll_plugins do
  gem "jekyll-paginate"
  gem "jekyll-redirect-from"
  gem "jekyll-archives"
  gem "jekyll-sitemap"
  gem "jekyll-gist"
  gem "jekyll-github-metadata"
  gem "jekyll-optional-front-matter"
  gem "jekyll-readme-index"
  gem "jekyll-titles-from-headings"
  gem "jekyll-relative-links"
  gem "rouge", "~> 3.26.0"
  gem "jekyll-coffeescript", "~> 2.0.0"
  gem "coffee-script-source", "~> 1.12.2"
  gem "jekyll-default-layout", "~> 0.1.5"
  gem "jekyll-sass-converter", "~> 2.1.0"
  gem "jekyll-seo-tag", "~> 2.7.1"
  gem "mercenary", "~> 0.4.0"
  gem "public_suffix", "~> 4.0.6"
  gem "sassc", "~> 2.4.0"
  gem "terminal-table", "~> 2.0.0"
  gem "unicode-display_width", "~> 1.7.0"
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
