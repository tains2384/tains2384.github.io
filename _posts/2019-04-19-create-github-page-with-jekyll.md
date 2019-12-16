---
layout: post
title: Tạo github page với jekyll
tags: [github, github page, jekyll]
comments: true
---

<!-- Content here -->
Vài bước đơn giản để tạo github page bằng Jekyll.
![jekyll logo](/img/jekyll-logo.png)

Tạo tài khoản github và fork repository mẫu (ex: [beautiful-jekyll](https://github.com/daattali/beautiful-jekyll#readme)) với tên `<ten-tai-khoan>.github.io`.

### Run ở local
1. Clone repository về máy.
2. Cài đặt Ruby. Kiểm tra cài đặt ruby:<br>
```ruby
ruby --version
```
3. Cài đặt `gem` có tên là `bundler`:<br>
```ruby
gem install bundler
```
4. Download 1 template dựng sẵn (ex: [beautiful-jekyll](https://github.com/daattali/beautiful-jekyll#readme))
5. Chỉnh sửa config site (title, description, ...) trong file `_config.yml`.
6. Run `jekyll serve` để chạy trang ở local, `jekyll build` để build.

### Chú ý:
##### 1. Ở windows muốn run `jekyll serve` thì vào file `Gemfile` uncomment dòng<br>
```bash
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw]
```

##### 2. Nếu run `jekyll serve` bị lỗi như sau thì run `bundle exec jekyll serve`.
```console
You have already activated public_suffix 3.1.1, but your Gemfile requires public_suffix 2.0.5. Prepending `bundle exec` to your command may solve this. (Gem::LoadError)
```
