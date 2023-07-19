# Digital Publishing System Framework

_v1.0.0_

This is a specification for requirements for a system for publishing documentation, papers, articles, books, blogs, and other content online. Its focus is on creating Open Content and Open Educational Resources that provides anyone with a free and perpetual permission to Retain, Revise, Remix, Reuse, and Redistribute it[^oer].

[^oer]: Defining the "Open" in Open Content and Open Educational Resources was written by David Wiley and published freely under a Creative Commons Attribution 4.0 license at http://opencontent.org/definition/

Its purpose is to establish a standard for building Digital Publishing Systems, based on established standards, and apply this to broad and narrow features such systems should support, and the requirements therein. It is opinionated and declarative, and not applicable to all publishing systems.

## <a name="specification"></a>Specification

The following describes functional features and technical requirements that the publishing system must supply or support, using common [imperatives](#imperatives). Feature Requirements describe high-level concepts and standards of the system, and Technical Requirements describe lower-level details of the implementations. As such, the System is:

> A _System_ is a set of doctrines, ideas, or principles usually intended to explain the arrangement or working of an organized whole -- adapted from [Merriam-Webster](https://www.merriam-webster.com/dictionary/system)

And Implementations are:

> An _Implementation_ is an act or instance of constructing something: the process of making something active or effective -- adapted from [Merriam-Webster](https://www.merriam-webster.com/dictionary/implementation)

### <a name="feature-requirements"></a>Feature Requirements

| Feature                                                                 | MUST | SHOULD | MAY |
| ----------------------------------------------------------------------- | ---- | ------ | --- |
| [Open Formats using Open Standards](#open-formats-using-open-standards) | ✖    |        |     |
| [Interoperable standards](#interoperable-standards)                     | ✖    |        |     |
| [Maintainability](#maintainability)                                     | ✖    |        |     |
| [Extensible Components](#extensible-components)                         | ✖    |        |     |
| [Flexible Layouts and templates](#flexible-layouts-and-templates)       | ✖    |        |     |
| [Structured and Responsive Styles](#structured-and-responsive-styles)   | ✖    |        |     |
| [Progressive enhancement](#progressive-enhancement)                     | ✖    |        |     |

#### <a name="open-formats-using-open-standards"></a>Open Formats using Open Standards

Digital publishing systems have always relied on standardized formats[^standardized-publishing-formats] -- everything from [TeX](#abbr-tex) to [XML](#abbr-xml) to [HTML](#abbr-html) -- but the standardization of content quickly and slowly falls apart to allow for special- or edge-cases of use. These open formats are not used uniformly even within the ecosystem of a single publishing system. The modern solution to this, supported by not so much technological as standards-focused advancement, is going back to plain text.

[^standardized-publishing-formats]: For an overview, see http://fileformats.archiveteam.org/wiki/Electronic_Publishing_formats

Implementations MUST support [Markdown](https://en.wikipedia.org/wiki/Markdown) as a format for content. It is strictly preferred for its simplicity as a standard, and flexibility and extensibility from variants that enhance but does not degrade the core of it. [CommonMark](https://commonmark.org/)[^djot] is the most applicable specification of Markdown, which for example [GitHub Flavored Markdown](https://github.github.com/gfm/) implements. Further, as plain text with a plain syntax, it is transferable between different implementations of the system.

[^djot]: An even stricter, less ambiguous, but more full-featured specification is Djot, see https://github.com/jgm/djot

#### <a name="interoperable-standards"></a>Interoperable standards

The [Open Formats using Open Standards](#open-formats-using-open-standards) and [Compatible Interoperability](#compatibile-interoperability) features implicitly prohibit vendor lock-in for content, which is the typical result when [CMS](#abbr-cms)' define and maintain their own standards for how content is implemented. An interoperable standard -- "a characteristic of a product or system to work with other products or systems", from [Wikipedia](https://en.wikipedia.org/wiki/Interoperability) -- is warranted. Being able to use the same content, structured in the same way, across implementations makes the cost of trying out new systems much lower, and [feature-parity](https://martinfowler.com/articles/patterns-legacy-displacement/feature-parity.html) can be broadly achieved. In this regard content and metadata is ephemeral, and Markdown with YAML FrontMatter becomes a de facto standard.

The implementation thereafter enhances rendering and associations between content, such that it becomes more [accessible](#accessible). This embraces and facilitates the principle "[Create Once, Publish Everywhere](https://web.archive.org/web/20170522060044/https://www.programmableweb.com/news/cope-create-once-publish-everywhere/2009/10/13)".

#### <a name="maintainability"></a>Maintainability

As digital technologies advance, so do standards and possibilities. What works today will not tomorrow, as any experienced web developer knows. However, major steps have been taken in making it easy for developers to track [feature-support](https://caniuse.com/ciu/about) in [Evergreen-browsers](#evergreen). As such, implementations MUST with each release clearly indicate the date of the release, and SHOULD describe what version of the [Browserslist](https://browsersl.ist/) it was tested with.

No requirement can be imposed on implementers for how or how long they should support and maintain their implementation, but making them [Open Source](#open-source-source-available) makes their further development possible and allows an ecosystem of other developers to contribute more easily.

#### <a name="extensible-components"></a>Extensible Components

The system for publishing a site MUST differentiate between Core and Added functionality. Given that its main purpose is publishing content digitally, this functionality mostly concerns how documents appear and behave in a web browser. These are termed _Components_, and _Core Components_ should be **general** and flexible enough to be adapted by _Added Components_ into more **specific** variants, which can further be altered by _Extra Components_ into **special** types.

##### <a name="core-components"></a>Core Components

Common Page Types that implementations MUST include:

- Default Page: A generic type of Page
- Listing: A generic type for displaying a Collection of Pages
- Index: A type for displaying a multiple Collections of Pages
- Docs: A type for rendering Documentation, especially hierarchically-structured content
- Article: A template for an article, a paper, a document, or other type of standalone content
- Search: A helper-type which implements search-fields

Additionally, nested Page Types should extend the Layout and Style through templating, such that they remain extensible and reusable in context. For example, a `Default Page` may warrant different treatment as a part of a set of documentation as opposed to a blog post.

##### <a name="added-components"></a>Added Components

Page Types that implementations SHOULD include:

- Blog: A replica of `Index`, but targeted to chronological sorting and categorical filtering
- Post: A subset of `Default Page`, but includes the option for a hero-image
- Diagram: A type type for rendering structured diagrams

##### <a name="extra-components"></a>Extra Components

Page Types that implementations MAY include:

- Book: A replica of `Listing`, used for organization of chapters
- Chapter: A replica of `Listing`, used for organization of pages
- Handout: A subset of `Article`, optimized for distributable notes -- such as [Tufte Handouts](https://edwardtufte.github.io/tufte-css/)
- CV: A type for rendering a standalone resumé

Of course, there are no limits to how much functionality implementations may offer through added Page Types, but the above describes some specific sets.

#### <a name="flexible-layouts-and-templates"></a>Flexible Layouts and templates

Implementations MUST use a [templating engine](http://www.simple-is-better.org/template/) for [Layouts](#abbr-layout). That is, a standardized method of turning data -- most often plain text -- into [HTML](#abbr-html), supporting reusable Layouts in the form of templates and template partials, variables and functions, text replacement, file inclusion, conditional evaluation and loops. This is essential for separating presentation from logic, and lowering the entry for users. [Many such engines are available](#abbr-layout), used by many Content Management Systems ([CMS](#abbr-cms)), for many programming-languages. A CMS will usually include one or more of these by default.

#### <a name="structured-and-responsive-styles"></a>Structured and Responsive Styles

Implementations MUST have separate stylesheets ([CSS](#abbr-css)) for structure and styling. One stylesheet should define all structural aspects of the semantic elements that the HTML lays out -- shaping the appearance of the overall Layout. The design MUST be [responsive](#abbr-responsive-design), to accommodate different devices viewing the same Layout in a coherent and recognizable manner. Subsequent stylesheets -- distinct Styles -- follow a basic principle: They apply color, fonts, or other rules that accentuate structural elements. Building and maintaining a consistent [Style Guide](http://styleguides.io/) makes it easier to adopt and adapt Layouts and Styles.

#### <a name="progressive-enhancement"></a>Progressive enhancement

Implementations MUST be built on the design principle of Progressive Enhancement:

> [A] strategy in web design that puts emphasis on web content first, allowing everyone to access the basic content and functionality of a web page, whilst users with additional browser features or faster Internet access receive the enhanced version" -- [Wikipedia](https://en.wikipedia.org/wiki/Progressive_enhancement)

In practice, this means that the presentation of and the content itself must be strictly separated, such that the availability of the content is not limited by how the presentation of it is built. This ties in with the [Open Formats using Open Standards](#open-formats-using-open-standards) feature: Plain text documents are maximally available to all users and clients, and [HTML](#abbr-html) enhances the presentation of these by structuring them within a Layout. [CSS](#abbr-css) further styles it to enhance how readable it is, and finally [JS](#abbr-js) adds enhanced functionality such as interactivity.[^progressive-enhancement][^graceful-degradation]

[^progressive-enhancement]: For a fuller discussion, see "[Understanding Progressive Enhancement](https://alistapart.com/article/understandingprogressiveenhancement/)", "[Progressive Enhancement with CSS](https://alistapart.com/article/progressiveenhancementwithcss/)", and "[Progressive Enhancement with JavaScript](https://alistapart.com/article/progressiveenhancementwithjavascript/)" on https://alistapart.com/ and "[The Role of Enhancement in Web Design](https://www.nngroup.com/articles/enhancement/)" on https://www.nngroup.com/
[^graceful-degradation]: In many ways, Progressive Enhancement is a reversal of the approach of Graceful Degradation, see https://www.w3.org/wiki/Graceful_degradation_versus_progressive_enhancement

### <a name="technical-requirements"></a>Technical Requirements

| Requirement                                                    | MUST | SHOULD | MAY |
| -------------------------------------------------------------- | ---- | ------ | --- |
| [Metadata-management](#metadata-management)                    | ✖    |        |     |
| [Compatible Interoperability](#compatibile-interoperability)   | ✖    |        |     |
| [Adaptable](#adaptable) to third-party systems                 |      |        | ✖   |
| [Performant](#performant)                                      | ✖    |        |     |
| [Accessible](#accessible)                                      | ✖    |        |     |
| [Evergreen](#evergreen)-browser compatibility                  | ✖    |        |     |
| [Exposure](#exposure) of content for search and API-queries    |      | ✖      |     |
| [Print-friendly](#print-friendly) Layouts and Styles           |      | ✖      |     |
| [Statically generated](#statically-generated) to host anywhere |      | ✖      |     |
| [Licensing](#licensing)                                        | ✖    |        |     |
| [Semantic Versioning](#semantic-versioning) of the code        | ✖    |        |     |
| [Calendar Versioning](#calendar-versioning) of the content     |      | ✖      |     |

#### <a name="metadata-management"></a>Metadata-management

Implementations MUST support metadata defined in the MarkDown's YAML FrontMatter, defined through this standard set of variables[^yaml-frontmatter]:

```yaml
---
title: "" # STRING Final title of the document
date: "" # STRING Using ISO 8601: YYYY-MM-DD, can include time: YYYY-MM-DDThh:mm:ss
modified: "" # STRING Using ISO 8601: YYYY-MM-DD, can include time: YYYY-MM-DDThh:mm:ss
description: "" # STRING A short summary of the content
layout: "" # STRING Page Type, the template for rendering this document
menu: "" # STRING Name in navigation
author: "" # STRING or LIST of STRINGS Simple name or structured-format: "FULL NAME <EMAIL@DOMAIN.TLD> (HTTPS://WEBSITE.TLD/)"
categories: # LIST of categories as STRINGS
tags: # LIST of tags as STRINGS
language: "" # STRING Using ISO 639-1: Two-letter language code
draft: # BOOLEAN True if not yet published publicly
image: "" # STRING Absolute or relative URL to image file, used for page thumbnail and hero-image
permalink: "" # STRING Route- and slug-override
aliases: # LIST of routes redirecting here as STRINGS
order: # NUMBER Override natural sorting when listing this and sibling documents
metadata: # DICTIONARY of overrides for OpenGraph as VALUE: KEY
---
```

These are all document-specific overrides for metadata that implementations MAY infer from a file's metadata on the filesystem, its filename, location, or other attributes. However, if explicitly definited they must take precedence.

[^yaml-frontmatter]:
    There is no pre-existing standard for variable-naming and use across Content Management Systems, this is therefore an effort to unify current usage based on a cross-section of existing systems, including:
    [Jekyll](https://jekyllrb.com/docs/front-matter/),
    [Assemble](https://assemble.io/docs/YAML-front-matter.html),
    [Zettlr](https://docs.zettlr.com/en/core/yaml-frontmatter/),
    [Obsidian](https://help.obsidian.md/Editing+and+formatting/Metadata),
    [Hugo](https://gohugo.io/content-management/front-matter/),
    [Hexo](https://hexo.io/docs/front-matter.html),
    [Grav](https://learn.getgrav.org/content/headers),
    [Astro](https://docs.astro.build/en/guides/markdown-content/),
    [Lume](https://lume.land/docs/creating-pages/page-data/),
    [Docusaurus](https://docusaurus.io/docs/create-doc), and
    [Metalsmith](https://metalsmith.io/docs/getting-started/#front-matter)

#### <a name="compatibile-interoperability"></a>Compatible Interoperability

Implementations MUST be able to read and produce output from a folder-structure for content as the following[^filenames]:

```bash
├── content
│   ├── **/*.md
│   ├── media
│   │   ├── ...
```

For example:

```bash
├── content/
│   ├── posts/
│   │   ├── index.md
│   │   ├── post-1/
│   │   │   ├── index.md
│   ├── about/
│   │   ├── about.jpg
│   │   ├── index.md
│   ├── home.jpg
│   ├── index.md
│   ├── media
│   │   ├── logo.jpg
```

Where Markdown-files (`.md`) are interpreted into their assigned Layout and converted into HTML-files (`.html`), preserving the folder-structure common to web servers. A folder-centric approach -- defining an `index.md`, rather than a file-centric one -- generating `about/index.html` from an `about.md`, is preferred because associated media and other files SHOULD co-exist in the same folder.

Which is all to say that this structure mirrors the needed output for hosting on virtually any server, as well as the expected routes when browsing a website, and keeps associated content close[^content-organization].

[^content-organization]: "[Content Organization](https://gohugo.io/content-management/organization/)" on GoHugo.io is a technical, but very practical, explainer of how folder-structures _should_ behave. A cursory glance at a number of well-known [CMS](#abbr-cms)' reveals how unordered, idiosyncratic, and not well thought through folder-structures are used -- most systems focus heavily on modern features, rather than content-production.
[^filenames]: Following RFC [3986](https://www.rfc-editor.org/rfc/rfc3986.html) and [8493](https://www.rfc-editor.org/rfc/rfc8493), all folder- and filenames should be lowercase and consist only of alphabeticals, numerals, dashes, underscores and dots -- ie., fit the pattern `[a-z0-9-_.]`.

#### <a name="adaptable"></a>Adaptable

Implementations MAY write adapters for [CMS](#abbr-cms)', which are strictly preferred to converters or importers that corrupt the [interoperability](#interoperability) of content. That is, the standards and structures laid out in this specification MUST remain in place, but the third-party system be made capable of reading the content. This includes enabling non-conforming content-standards, such as those not adopted as a part of the [CommonMark Spec](https://spec.commonmark.org/current/) or idiosyncratically defined by the [CMS](#abbr-cms), as features.

#### <a name="performant"></a>Performant

Implementations MUST optimize for performance, especially for cross-device use in browsers. As a general rule, this means between 90 and 100 score in a [Lighthouse Performance Score](https://developer.chrome.com/en/docs/lighthouse/performance/performance-scoring/) on a live prototype. It is a weighted average of metric scores, and "[t]he weightings are chosen to provide a balanced representation of the user's perception of performance".

#### <a name="accessible"></a>Accessible

Implementations MUST achieve Web Content Accessibility Guidelines (WCAG) -- meaning that the resulting published content is Perceivable, Operable, Understandable, and Robust[^wcag][^accessibility-laws] -- to the A Conformance Level[^wcag-conformance-levels]. Testing of these criteria MAY be automated[^automating-accessibility-testing].

[^wcag]: For a full explanation, see "[Understanding the Web Content Accessibility Guidelines](https://developer.mozilla.org/en-US/docs/Web/Accessibility/Understanding_WCAG)" on https://developer.mozilla.org/ and "[WCAG 2 Overview](https://www.w3.org/WAI/standards-guidelines/wcag/)" on https://www.w3.org/
[^accessibility-laws]:
    [EN 301 549](https://www.etsi.org/deliver/etsi_en/301500_301599/301549/02.01.02_60/en_301549v020102p.pdf) in the EU,
    [Section 508 of the Rehabilitation Act](https://www.section508.gov/training/) in the US, [Accessibility Regulations 2018](https://www.legislation.gov.uk/uksi/2018/952/introduction/made) in the UK are examples of laws that directly govern how accessible websites must be, see https://developer.mozilla.org/en-US/docs/Learn/Accessibility/What_is_accessibility#accessibility_guidelines_and_the_law

[^wcag-conformance-levels]: See "[Understanding Conformance](https://www.w3.org/TR/UNDERSTANDING-WCAG20/conformance.html)" on https://www.w3.org/ for an overview of WCAG Conformance
[^automating-accessibility-testing]: See "[Automating accessibility testing: Modern tooling for an imperative part of front-end development](https://olevik.me/writing/code/automating-accessibility-testing)" on https://olevik.me/ for a practical approach

#### <a name="evergreen"></a>Evergreen

Implementations MUST support Evergreen-browser compatibility, that is specifically, the [Browserslist](https://browsersl.ist/) `default`-configuration, "which is a shortcut for `> 0.5%, last 2 versions, Firefox ESR, not dead`. It matches recent versions of popular and supported browsers worldwide and includes Firefox Extended Support Release which is updated roughly annually."

This is mostly relevant for compilation of scripts and styles, but it is important that the implementation is broadly usable and tested at the time of release. Of course, this configuration should be [updated](https://github.com/browserslist/update-db) ahead of every new release to remain current.

#### <a name="exposure"></a>Exposure

Implementations SHOULD expose content in various ways. Primarily this is client-side code -- [HTML](#abbr-html), [CSS](#abbr-css), [JS](#abbr-js) -- that renders content in the browser, but secondarily there are benefits from [RSS](#abbr-rss)-feeds and [JSON](#abbr-json)-data[^create-once-publish-everywhere] being exposed to internal and external integrations. Examples include search and API-queries.

[^create-once-publish-everywhere]: For a potential integration that facilitates this, see https://github.com/OleVik/cope-static-api/

In addition, implementations SHOULD consider Search Engine Optimization ([SEO](#abbr-seo)), especially as relates to the use of semantic metadata and [structured data](https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data), OpenGraph-support for [HTML Living Standard 4.2.5.1 Standard metadata names](https://html.spec.whatwg.org/multipage/semantics.html#standard-metadata-names), as well as the [Dublin Core terms](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/) for Linked Data.

#### <a name="print-friendly"></a>Print-friendly

Implementations SHOULD endeavour to support direct printing of the content to [PDF](#abbr-pdf) via the browser, that maintain a recognizable appearance of the implementation but optimize the styling for printing and archival purposes.

##### <a name="multimedia"></a>Multimedia

Implementations SHOULD facilitate the use of graphics and media that contribute to otherwise textual content. This is straightforward for images, but audio, video, and interactive media typically requires embedding or scripts to be loaded or efficiently distributed. In cases where Progressive Enhancement is not technically viable, Graceful Degradation[^graceful-degradation] is preferred: Embed the complex media[^evaluation-of-open-content], and clearly link to its source or simpler variant -- a static version of an interactive chart or diagram, or a high-resolution copy of an image. Keeping sources locally available is stricly preferred to linking to third-parties, both for integrity and durability.

[^evaluation-of-open-content]: For an evaluation of the Openness, Availability, Development, and Implementation of content, see https://github.com/OleVik/evaluation-of-open-content

#### <a name="statically-generated"></a>Statically generated

Implementations SHOULD be capable of compiling content into client-side code and outputting code that can be opened in a browser without server-side code. That is, the static generation of browsable content without the need for hosting services. Implementations MAY use dynamic server-side code as their primary engine for rendering code, but there SHOULD be alternative methods of generating output[^static-site-generators].

[^static-site-generators]: Many programs are capable of producing static output, see https://staticsitegenerators.net/ for a list

This relates directly to [Progressive Enhancement](#progressive-enhancement): Content available at the lowest threshold has the lowest level of complexity for using it, which is paramount for accessibility and longevity. [Link rot](https://en.wikipedia.org/wiki/Link_rot) is a real concern and [websites disappear all the time](https://www.expireddomains.net/). Websites that depend entirely on their webhost tend to be lost to time unless commercialized.

#### <a name="licensing"></a>Licensing

No direct requirements are applied to implementations of this specification, other than the [CC BY-NC-SA 4.0 license](#license). Implementations SHOULD [choose a license](https://choosealicense.com/no-permission/) which covers the intended use, keeping in mind that if the implementation relies on third-party software -- including frameworks and libraries -- the license must be [compatible and often use the same license](https://choosealicense.com/community/). Even a non-free license, such as the ones described below, is better than no license at all.

##### <a name="open-source-source-available"></a>Open Source, Source Available

There's a point to be made that not all software must be or is open or free, even though the ecosystem-benefits of this are great across the world of software. _Source Available_ licensing is one such approach, broadly:

> Source-available software is software released through a source code distribution model that includes arrangements where the source can be viewed, and in some cases modified, but without necessarily meeting the criteria to be called open-source -- [Source-available software](https://en.wikipedia.org/wiki/Source-available_software) on Wikipedia

Alternatives to proper open source licenses include the [Shared Source Initiative](https://en.wikipedia.org/wiki/Shared_Source_Initiative), [Server Side Public License](https://en.wikipedia.org/wiki/Server_Side_Public_License), [Business Source License](https://mariadb.com/bsl-faq-mariadb/), [Fair Source License](https://github.com/fairsource/fairsource). See "[One Startup's Heretical Plan to Turn Open Source Code Into Cash](https://www.wired.com/2016/03/former-open-sourcers-ask-companies-pay-fair-share/)" on Wired for an explainer.

#### <a name="semantic-versioning"></a>Semantic Versioning

Implementations MUST adhere to [Semantic Versioning](https://semver.org/) in product-releases. Modern software commonly utilizes libraries and frameworks, almost regardless of which programming-language it is written in and which ecosystem it exists in. A good practice which has spread in these ecosystems is Semantic Versioning, summarized by:

> Given a version number MAJOR.MINOR.PATCH, increment the:
>
> 1. MAJOR version when you make incompatible API changes
> 2. MINOR version when you add functionality in a backward compatible manner
> 3. PATCH version when you make backward compatible bug fixes

Consistent use of versioning for the code ensures clarity in what it is compatible with, and which specific versions of dependencies it relies on[^dependency-hell].

[^dependency-hell]: For an explainer of consequences of inconsistent versioning, see "[The Nine Circles of Dependency Hell (and a roadmap out)](https://about.sourcegraph.com/blog/nine-circles-of-dependency-hell)" at https://sourcegraph.com/

#### <a name="calendar-versioning"></a>Calendar Versioning

Implementations SHOULD facilitate a separate log of substantial changes to the published content. This is recommended, rather than mixing it with changes to the code. A good standard to follow is "[keep a changelog](https://keepachangelog.com/)", using [Calendar Versioning](https://calver.org/) for headings. For example, writing in Markdown with the date-format `YYYY-0M-0D`:

```markdown
# Changelog

All notable changes to this site's content will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/),
and applies [Calendar Versioning](https://calver.org/). Changes to content
therefore applies from the date the are published. This only applies to
substantial changes to the specific document.

## 2023-07-06

### Added

- New content added at this date
```

Third-level headings would be one of:

- **Added** for new features
- **Changed** for changes in existing functionality
- **Deprecated** for soon-to-be removed features
- **Removed** for now removed features
- **Fixed** for any bug fixes
- **Security** in case of vulnerabilities

With list-items detailing what changed below these.

## <a name="evaluation-rubric"></a>Evaluation Rubric

Functional and technical features -- expressed as requirements above and in practice in implementations -- should be evaluated as to how they are implemented and what is non-compliant with this specification. The table below is an example of how to summarize this.

| Feature | YES | PARTIALLY | NO  |
| ------- | --- | --------- | --- |
|         | ✖   |           |     |
|         |     | ❔        |     |
|         |     |           | ❌  |

Further details should be thereby be written below to explain how and to what level these features are implemented. See [Evaluation Rubric](https://github.com/OleVik/Digital-Publishing-System-Framework/blob/main/Evaluation%20Rubric.md) for a fuller example.

## <a name="definitions"></a>Definitions

### <a name="imperatives"></a>Imperatives

Following [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) and [RFC 7841](https://www.rfc-editor.org/rfc/rfc8174), these key words are used to indicate requirement Levels:

1. **MUST**: This word, or the terms "REQUIRED" or "SHALL", mean that the
   definition is an absolute requirement of the specification.
2. **MUST NOT**: This phrase, or the phrase "SHALL NOT", mean that the
   definition is an absolute prohibition of the specification.
3. **SHOULD**: This word, or the adjective "RECOMMENDED", mean that there
   may exist valid reasons in particular circumstances to ignore a
   particular item, but the full implications must be understood and
   carefully weighed before choosing a different course.
4. **SHOULD NOT**: This phrase, or the phrase "NOT RECOMMENDED" mean that
   there may exist valid reasons in particular circumstances when the
   particular behavior is acceptable or even useful, but the full
   implications should be understood and the case carefully weighed
   before implementing any behavior described with this label.
5. **MAY**: This word, or the adjective "OPTIONAL", mean that an item is
   truly optional. One vendor may choose to include the item because a
   particular marketplace requires it or because the vendor feels that
   it enhances the product while another vendor may omit the same item.
   An implementation which does not include a particular option MUST be
   prepared to interoperate with another implementation which does
   include the option, though perhaps with reduced functionality. In the
   same vein an implementation which does include a particular option
   MUST be prepared to interoperate with another implementation which
   does not include the option (except, of course, for the feature the
   option provides.)

These are commonly used in describing [Best Current Practices](https://datatracker.ietf.org/doc/html/rfc1818) for the Internet community.

### <a name="acronyms-and-abbreviations"></a>Acronyms and abbreviations

- <a name="abbr-cms"></a>_CMS_ -- "A content management system (CMS) is computer software used to manage the creation and modification of digital content", from https://en.wikipedia.org/wiki/Content_management_system. For an overview of such systems, see https://curlie.org/Computers/Software/Internet/Site_Management/Content_Management/
- <a name="abbr-css"></a>_CSS_ -- "Cascading Style Sheets (CSS) is a stylesheet language used to describe the presentation of a document written in HTML [...]. CSS describes how elements should be rendered on screen, on paper, in speech, or on other media.", from https://developer.mozilla.org/en-US/docs/Web/CSS
- <a name="abbr-html"></a>_HTML_ -- "HyperText Markup Language is the standard markup language for documents designed to be displayed in a web browser", from https://en.wikipedia.org/wiki/HTML
- <a name="abbr-js"></a>_JS_ -- "JavaScript (JS) is a lightweight [...] programming language [...] well-known as the scripting language for Web pages", from https://developer.mozilla.org/en-US/docs/Web/JavaScript
- <a name="abbr-json"></a>_JSON_ -- "JavaScript Object Notation (JSON) is a data-interchange format.", from https://developer.mozilla.org/en-US/docs/Glossary/JSON
- <a name="abbr-layout"></a>_Layout_ -- Templates that achieve a specific appearance through HTML-structures and CSS-styling, and more broadly parts that make up Components. For an overview of different template-engines, see https://github.com/topics/template-engine/
- <a name="abbr-pdf"></a>_PDF_ -- "Portable Document Format (PDF), standardized as ISO 32000, is a file format [...] to present documents, including text formatting and images, in a manner independent of application software", see https://en.wikipedia.org/wiki/PDF
- <a name="abbr-responsive-design"></a>_Responsive Design_ -- "Responsive web design (RWD) is a web design approach to make web pages render well on all screen sizes and resolutions while ensuring good usability. It is the way to design for a multi-device web", from https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design
- <a name="abbr-rss"></a>_RSS_ -- "RSS (Really Simple Syndication) refers to several XML document formats designed for publishing site updates", from https://developer.mozilla.org/en-US/docs/Glossary/RSS
- <a name="abbr-seo"></a>_SEO_ -- "SEO (Search Engine Optimization) is the process of making a website more visible in search results, also termed improving search rankings", from https://developer.mozilla.org/en-US/docs/Glossary/SEO
- <a name="abbr-tex"></a>_TeX_ -- A typesetting system developed since 1978, see https://en.wikipedia.org/wiki/TeX
- <a name="abbr-xml"></a>_XML_ -- "Extensible Markup Language (XML) is a markup language and file format for storing, transmitting, and reconstructing arbitrary data", from https://en.wikipedia.org/wiki/XML

## <a name="license-and-attribution"></a>License and attribution

This document is licensed under [Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/legalcode).

Should you choose to apply this framework and specification, with permission granted under the Creative Commons Attribution 4.0 license, your attribution must include the Title, Author, Source, and License. You might choose to use the following attribution: "Digital Publishing System Framework" written by Ole Vik and published under a Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0) license at https://github.com/OleVik/Digital-Publishing-System-Framework/.

## <a name="contributions"></a>Contributions

Suggestions and feedback to the Digital Publishing System Framework are welcome, see [CONTRIBUTING](https://github.com/OleVik/Digital-Publishing-System-Framework/blob/main/CONTRIBUTING.md) for details.
