# Interface Style Guide


## Table of Contents

* [CSS Code Style](#css-code-style)
* [CSS File Organization](#css-file-organization)
* [HTML5 Code Style](#html5-code-style)
* [Cross-browser Compatibility](#cross-browser-compatibility)


## CSS Code Style

* Use soft-tabs with a two space indent.
* Put spaces after : in property declarations.
* Put spaces before { in rule declarations.
* Use hex color codes #000 unless using rgba.
* Use // for comment blocks (instead of /\* */)
* Use hyphen for naming classes.

  ```css
    // Bad
    .s_header

    // Good
    .s-header
  ```

* Use hyphen or underscore for naming css files. Do not use CamelCase.

  ```
    // Bad
    SectionName.scss.erb

    // Good
    section-name.scss.erb
  ```
* Use ERB extension when naming css file if SCSS preprocessor is used for a Ruby project. This is often needed if you want to use the asset_path for your images.

  ```
    // Bad
    application.scss

    // Good
    application.scss.erb
  ```
* Recommended: use the asset_path helper for images.

  ```css
    // Bad
    background: url('/assets/images/test.png');

    // Good
    background: url('<%= asset_path('test.png') %>');
  ```

* Use !important rule when necessary. Sometimes it is not necessary when your style definitions are ordered properly.
* Limit **depth of applicability** by using fewer selectors, avoiding ID selectors and relying less on html structure.

  ```css
    // Bad
    #main #sidebar p img {
      background: #FFF;
      border: 1px solid #DDD;
      padding: 5px;
    }

    // Good

    #sidebar img {
      background: #FFF;
      border: 1px solid #DDD;
      padding: 5px;
    }

    // Good

    Add a new class for image frame which can be applied to other images that are not within the sidebar

    .image-frame {
      background: #FFF;
      border: 1px solid #DDD;
      padding: 5px;
    }
  ```

## CSS File Organization

  ```
    app/assets/stylesheets
    ├── components
    │   ├── buttons.scss.erb
    |   ├── forms.scss.erb
    │   ├── boxes.scss.erb
    │   └── lists.scss.erb
    ├── base
    │   └── normalize.scss.erb
    ├── ie
    │   ├── ie8.scss.erb
    │   └── ie9.scss.erb
    ├── mobile
    │   └── layout.scss.erb
    ├── layouts
    │   ├── grid.scss.erb
    │   └── structure.scss.erb
    ├── themes
    │   ├── blue.scss.erb
    │   └── black.scss.erb
    ├── mixins
    │   ├── _corners.scss
    │   └── _linear-gradients.scss
    │   └── _animation.scss
    ├── sections
    │   ├── blog.scss.erb
    │   └── lists.scss.erb
    └── globals
        ├── colors.scss
        └── typography.scss
  ```

## HTML5 Code Style

* Use soft-tabs with a two space indent.

* Defining the doctype

  In ERB (Ruby) or HTML:

  ```html
    <!DOCTYPE html>
  ```

  In HAML (Ruby):

  ```ruby
    !!! 5
  ```

* Semantics

  There are a lot of well-written guides on semantics:

  * <a href="http://www.html5rocks.com/en/features/semantics" title="HTML5 Rocks" target="_blank">HTML5 Rocks </a>
  * <a href="http://diveintohtml5.info/" title="Dive into HTML5"  target="_blank">Dive into HTML5</a>
  * <a href="http://learn.shayhowe.com/html-css/elements-semantics" title="Elements and Semantics" target="_blank">Shay Howe on Elements and Semantics</a>

* Stop using and remove any of these obsolete and deprecated elements:

  **Obsolete Elements**
  * frameset
  * frame
  * noframe
  * acronym (replaced by abbr)
  * applet (replaced by object)
  * dir (replaced by ul)

  **Deprecated Elements**
  * basefont
  * big
  * center
  * font
  * s
  * strike
  * tt
  * u

* These attributes are no longer valid:
  * align
  * link, vlink, alink, and text attributes on the body tag
  * bgcolor
  * height and width
  * scrolling on the iframe element
  * valign
  * hspace and vspace
  * cellpadding, cellspacing, and border on table

* Omitting file type and media type is valid for the link tag.

  ```html
    <link href='/assets/style.css' rel='stylesheet'/>
  ```

* Omitting file type is valid for the javascript link tag.

  ```html
    <script src='/assets/application.js' />
  ```

* The header tag, footer and other new tags can be used within a section.

  ```html
    <section>
      <header>
        <h1>Change Quotation</h1>
      </header>
    <blockquote>
      To improve is to change; to be perfect is to change often.
        - Winston Churchill
    </blockquote>
    </section>
  ```

* The article tag is ideal for actual content. A section can have many articles and articles can have many sections.
  ```
    <article>
      <header>
        <h1>Redemption Song</h1>
      </header>
        <p>None but ourselves can free our minds.</p>
      <footer>
        <p>
          Song by Bob Marley.
          Released: October 1980
        </p>
      </footer>
    </article>
  ```

* Use **placeholder** attribute for providing hints and use <a href="https://github.com/mathiasbynens/jquery-placeholder" title="jQuery Placeholder">jQuery Placeholder</a> for browsers that do not support it.

   ```html
    // bad
    <input id="email" type="email" name="email" data-hint="user@example.com">

    // good
    <input id="email" type="email" name="email" placeholder="user@example.com">
  ```

## Cross-browser Compatibility

* Use conditional comments sensibly. Indicate the version of the browser by naming the file accordingly.

   ```
      // for IE 8 browsers only
      <!--[if IE 8]>
        <link href='/assets/ie8.css' media='screen' rel='stylesheet' />
      ![endif]-->

      // for IE 9 browsers and below.
      <!--[if lt IE 9]>
        <link href='/assets/lt-ie9.css' media='screen' rel='stylesheet' />
      ![endif]-->

      // for IE 9 browsers only
      <!--[if IE 9]>
        <link href='/assets/ie9.css' media='screen' rel='stylesheet' />
      ![endif]-->
   ```

* **Conditional Comments Syntax Table**

  <table cellspacing="0" cellpadding="0" border="0" class="poll-results">
    <tbody>
      <tr>
        <th>Item</th>
        <th>Example</th>
        <th>Comment</th>
      </tr>
      <tr>
        <td>!</td>
        <td>[if !IE]</td>
        <td>The NOT operator. This is placed immediately in front of the <em>feature</em>, <em>operator</em>, or <em>subexpression</em> to reverse the Boolean meaning of the expression.</td>
      </tr>
      <tr>
        <td>lt</td>
        <td>[if lt IE 5.5]</td>
        <td>The less-than operator. Returns true if the first argument is less than the second argument.</td>
      </tr>
      <tr>
        <td>lte</td>
        <td>[if lte IE 6]</td>
        <td>The less-than or equal operator. Returns true if the first argument is less than or equal to the second argument.</td>
      </tr>
      <tr>
        <td>gt</td>
        <td>[if gt IE 5]</td>
        <td>The greater-than operator. Returns true if the first argument is greater than the second argument.</td>
      </tr>
      <tr>
        <td>gte</td>
        <td>[if gte IE 7]</td>
        <td>The greater-than or equal operator. Returns true if the first argument is greater than or equal to the second argument.</td></tr>
      <tr>
        <td>( )</td>
        <td>[if !(IE 7)]</td>
        <td>Subexpression operators. Used in conjunction with boolean operators to create more complex expressions. </td>
      </tr>
      <tr>
        <td>&amp;</td><td>[if (gt IE 5)&amp;(lt IE 7)]</td>
        <td>The AND operator. Returns true if all subexpressions evaluate to true</td>
      </tr>
      <tr>
        <td>|</td>
        <td>[if (IE 6)|(IE 7)]</td>
        <td>The OR operator. Returns true if any of the subexpressions evaluates to true.</td>
      </tr>
    </tbody>
  </table>

* Isolate IE filters and hacks into new files, e.g., **ie8.css** for Internet Explorer 8. Not all internet explorer browsers have an issue so do not create an ie.css file. Specifying versions help. There'll come a day when there's no need to support these browsers and all you have to do is delete the file and references to it.

## References

<a href="https://github.com/styleguide" target="_blank">HTML5 for Web Designers by Jeremy Keith</a>

<a href="https://github.com/styleguide" target="_blank">Github Style Guide</a>

<a href="http://smacss.com" target="_blank">Scalable and Modular Architechture for CSS by Jonathan Snook</a>


## Contributors


#### <a href="http://blog.bridgeutopiaweb.com" target="_blank"> Katherine G. Pe </a>, Software Developer

This style guide was written specifically for projects I work on or help with. This is clearly written to document good style and promote it for a better web.


&copy; 2012 Katherine G. Pe. Released under the <a href="http://opensource.org/licenses/mit-license.php" target="_blank"> MIT License</a>.
