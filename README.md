<p align="center">
  <a href="https://www.gatsbyjs.org">
    <img alt="Gatsby" src="https://www.gatsbyjs.org/monogram.svg" width="60" />
  </a>
</p>
<h1 align="center">
  Gatsby Starter Infinite Scroll
</h1>

This is a Gatsby starter intended for developers who need **infinite scroll** or **pagination** in their Gatsby project. 

Try out this live demo with 10k photos »»» [https://gatsby-starter-infinite-scroll.baobab.fi](https://gatsby-starter-infinite-scroll.baobab.fi)

## :zap: Get started

Fork and `npm install`. Run in dev mode with `gatsby develop`.

I intend to write an article about how this works and what you need to consider if you want to replicate similar functionality in an existing project. Until then, I recommend reading the code in the following order:

[gatsby-node.js](https://github.com/baobabKoodaa/gatsby-starter-infinite-scroll/blob/master/gatsby-node.js) » [gatsby-browser.js](https://github.com/baobabKoodaa/gatsby-starter-infinite-scroll/blob/master/gatsby-browser.js) » [templates/paginatedPageTemplate.js](https://github.com/baobabKoodaa/gatsby-starter-infinite-scroll/blob/master/src/templates/paginatedPageTemplate.js) » [components/view.js](https://github.com/baobabKoodaa/gatsby-starter-infinite-scroll/blob/master/src/components/view.js) » [components/globalState.js](https://github.com/baobabKoodaa/gatsby-starter-infinite-scroll/blob/master/src/components/globalState.js).

If you run into any difficulty, I will be happy to help.

## 🚀 To infinity and beyond!

- The default behavior is to use infinite scroll, but **fallback to pagination** if JS is disabled or an error occurs. Additionally, the demo has a **toggle** so you can test both modes without disabling JS in your browser.
- This implementation **does not fetch unnecessary metadata at initial pageload**. Instead, we only fetch the metadata that we actually need. For example, if we're showing you 120 items right now, then we only need metadata for 120 items. We can ask for more metadata as you scroll for more items. This was somewhat awkward to implement in Gatsby, which is why previously published implementations load metadata for _all_ items during initial page load, and then use client side JS to filter to the desired items. The performance hit for doing that isn't too bad for small collections of items, but it becomes unbearable for large collections, especially if the metadata contains base64 versions of images as placeholders. **This performance optimization was my main motivation for creating this starter**.
- Additionally, a minor performance improvement: **initial items shipped along with the initial page instead of separately fetched**.
- When the user navigates to another internal page and later returns to front page, **scroll position is not forgotten** (because we keep items in global state).
- **Many edge cases are considered**
    - Large screens / small pages: If initial items fit to screen before scrolling is possible, we fetch more items (this is often overlooked in infinite scroll implementations, e.g. LinkedIn and react-simple-infinite-scroll have this bug.)
    - Slow connections: the initial pageload is consistent even before the React component mounts.
    - Metadata fetching: allow fetching multiple pages of metadata concurrently (not fetching pages consecutively allows users to scroll down faster, e.g. if images are cached and metadata pages are not, or if the user wants to scroll fast to a specific location before images can load).
- Includes a script that can fetch large amounts of random images from Unsplash.

## 🎓 Attribution

- Photos are from [Unsplash](https://unsplash.com). Unfortunately I couldn't get photographer attribution, because their main API is rate limited, and the non limited API (source.unsplash.com) only gave me photos. If you can help me get photographer attribution, that would be awesome!
- Infinite scroll uses some code from Jared Palmer's [react-simple-infinite-scroll](https://github.com/jaredpalmer/react-simple-infinite-scroll).
- Image layout CSS Grid is modified from work by [LekoArts](https://www.lekoarts.de/).
- Traffic lights CSS graphics are modified from work by Azik Samarkandiy.
- Loading spinner uses icon from FontAwesome.

I would love to see what you build with this. You can [drop me a message](https://blog.baobab.fi/contact) or star this repo.
