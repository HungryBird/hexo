---
title: contact
date: 2019-12-20 13:03:17
categories:
- contact
---

<ul class="contact">
    <li data-url="381548325@qq.com">
        <a>
            <image src="/contact/index/email.png" alt="邮箱" />
            <div>邮箱</div>
        </a>
    </li>
    <li data-url="https://github.com/hungryBird">
        <a href="https://github.com/hungryBird">
            <image src="/contact/index/github.png" alt="github" />
            <div>github</div>
        </a>
    </li>
    <li data-url="https://www.zhihu.com/people/he-chen-23">
        <a href="https://www.zhihu.com/people/he-chen-23">
            <image src="/contact/index/zhihu.png" alt="知乎" />
            <div>知乎</div>
        </a>
    </li>
    <li data-url="https://weibo.com/u/5693785217">
        <a href="https://weibo.com/u/5693785217">
            <image src="/contact/index/weibo.png" alt="微博" />
            <div>微博</div>
        </a>
    </li>
    <li data-url="https://hungrybird.github.io/">
        <a href="https://hungrybird.github.io/">
            <image src="/contact/index/blogger.png" alt="博客" />
            <div>博客</div>
        </a>
    </li>
</ul>
<div id="URL-wrapper">
<div>

<script>
    const URLDom = document.querySelector('#URL-wrapper');
    const uLis = document.querySelector('.contact').querySelectorAll('li');
    for (const li of uLis) {
        li.addEventListener('mouseenter', (e) => {
            URLDom.innerText = e.target.dataset.url;
        })
    }
</script>
