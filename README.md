# css-kit

A set of standards and guidelines to follow for CSS.

## Tooling

CSS is built using Postcss with a set of plugins allowing for:

- Media Query Varibles via [postcss-custom-media](https://github.com/postcss/postcss-custom-media)
- Auto-prefixing via [autoprefixer](https://github.com/postcss/autoprefixer)
- Nesting via [postcss-nexting](https://github.com/jonathantneal/postcss-nesting)
- Minification via [nano](https://github.com/cssnano/cssnano)

See all here: https://preset-env.cssdb.org/features

## Media Queries

Styles should be written with the media queries to take affect after a minumun viewport width - commonly know an 'mobile first'.

We use postcss-custom-media to keep breakpoints defined as variables. This ensures that linked but seperate components are working from the same rule set. For example, hiding a navigation bar and showing a hamburger icon must happen at the same time - otherwise invalid states might happen.

The names only for easy reference, **don't design for separate device sizes** - this is one singular responsive site, not 5 sites delivered in one HTML file.

```scss
.HeroContainer {
	width: 100%;
	max-width: 400px;
	margin: 0 auto;
	font-size: 1.1rem;

	@media (--fromTablet) {
		width: 80%;
	}

	@media (--fromDesktop) {
		font-size: 1.2rem;
	}
}
```

## Grids
Depending on requirements for browser support, CSS Grids should be greatly prefered.

## Naming Convention
We're aiming to use the popular syntax of BEM for structuring our CSS. BEM makes creating modular styles and components easy. Read [Harry Robert's BEM Article](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) for a great primer on it's use and pros + cons.

### Components
Each module has it's own file and is kept within the `css/components` directory. The name of the file should mach the name of the module.

A component should be a reusable element on a page, e.g: a breadcrumb. Elements should only be selected by class, within a module all elements should be flat.

```scss
.Breadcrumb{
  background-color: #d0d0d2;
  height: 24px;
  position: relative;

  &__list{
    max-width: 950px;
    margin: 0 auto;
    list-style: none;
    padding-left: 1em;
    padding-right: 1em;
  }

  &__item{
    display: inline-block;
    font-size: 12px;
    line-height: 24px;
    font-weight: 500;
  }

  &__action{
    color: #ffffff;
  }
}
```

And it's markup

```html
<div class="Breadcrumb">
  <ol class="Breadcrumb__list">
    <li class="Breadcrumb__item">
      <a class="Breadcrumb__action" href="{{ news_page.permalink }}" title="{{ news_page.title }}">
        {{ news_page.title }}
      </a>
    </li>
  </ol>
</div>

```

For example, this would easily allow us to change the anchor element to a button in the future.