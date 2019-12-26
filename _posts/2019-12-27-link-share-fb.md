---
layout: post
title: Tạo link share website trên facebook
tags: [fb, facebook, fb-sharing, fb-seo]
comments: true
---

<!-- Content here -->
**Sử dụng các thẻ meta tag để hiển thị nội dung chia sẻ trên facebook - og (Open Graph)**

## Đăng kí facebook for developers
1. Tạo app trên facebook for developer
2. Vào `Settings > Basic > App ID` để lấy thông tin App ID

**Trong thẻ head của trang web, implement các thẻ meta sau**
```javascript
// NuxtJS
head() {
    return {
      title: 'Tiêu đề trang',
      meta: [
        {
          hid: 'description',
          property: 'description',
          content: 'Nội dung sơ lược trang web',
        },
        {
          hid: 'keyword',
          property: 'keyword',
          content: 'Từ khóa cách nhau bởi dấu phẩy',
        },
        {
          hid: 'fb:app_id',
          property: 'fb:app_id',
          content: 'App ID lấy ở trên',
        },
        {
          hid: 'og:type',
          property: 'og:type',
          content: `article`, // Tham khảo: https://ogp.me/#types
        },
        {
          hid: 'og:url',
          property: 'og:url',
          content: 'Đường link hiện tại của trang web',
        },
        {
          hid: 'og:title',
          property: 'og:title',
          content: 'Tiêu đề trang web hiển thị khi chia sẻ link trên facebook',
        },
        {
          hid: 'og:description',
          property: 'og:description',
          content: 'Nội dung sơ lược khi chia sẻ trên facebook',
        },
        {
          hid: 'og:image',
          property: 'og:image',
          content: 'Link tới ảnh, ảnh sẽ hiển thị khi chia sẻ trên link trên facebook', // Public link image
        },
        {
          hid: 'og:image:width',
          property: 'og:image:width',
          content: 400, // Thiết lập kích thước ảnh, workaround nếu ko facebook sẽ không fetch được ảnh
        },
        {
          hid: 'og:image:height',
          property: 'og:image:height',
          content: 400, // Thiết lập kích thước ảnh, workaround nếu ko facebook sẽ không fetch được ảnh
        },
      ],
    }
  },
```