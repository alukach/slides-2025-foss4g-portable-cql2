---
title: Portable CQL2
info: |
  Portable CQL2: A Rust Core for Queries Everywhere
class: text-center
highlighter: shiki
drawings:
  persist: false
  enable: false
transition: slide-left
mdc: true
addons:
  - slidev-addon-qrcode

theme: './theme'
layout: title
image: https://images.unsplash.com/photo-1579818276659-2943e3cd4b30
---

# Portable CQL2

::subtitle::
A Rust Core for Queries Everywhere

<DecorativeRectangle
  width="50%"
  height="40%"
  :zIndex="20"
  :position="{
    bottom: '2%',
    right: '0%',
  }"
  :customStyle="{ mixBlendMode: 'multiply', borderTopRightRadius: 0, borderBottomRightRadius: 0 }"
>
  <!-- You can place content _inside_ of rectangles! -->
  <div w-full h-full relative flex flex-col items-end justify-end p-4 text-white text-right>
    <h4>
      ⚡️ Lightning Talk
    </h4>
    <h3 text-5xl>
      FOSS4G
    </h3>
    <h4 text-md font-mono>
      2025-11-19
    </h4>
    <h5 text-sm>
      <code text-primary>@alukach</code>
    </h5>
  </div>
</DecorativeRectangle>
<LogoHorPos position="top-left" height="24px" />

---
layout: iframe-right
url: https://developmentseed.org/cql2-rs
class: full-height-centered-col
---

# `cql2-rs`

<CurrentUrlQRCode
  url="https://developmentseed.org/cql2-rs"
/>

`https://developmentseed.org/cql2-rs`


## Authors

<div mt-2 flex items-center gap-2>
  <a href="https://github.com/bitnerd" target="_blank" title="@bitnerd">
    <img src="https://avatars.githubusercontent.com/u/164828?v=4" alt="@bitnerd" w-25 h-25 rounded-full />
  </a>
  <a href="https://github.com/gadomski" target="_blank" title="@gadomski">
    <img src="https://avatars.githubusercontent.com/u/58314?v=4" alt="@gadomski" w-25 h-25 rounded-full />
  </a>
</div>

<!--
cql2-rs is a small utility library created this year by DevelopmentSeed. As per the docs:

> cql2-rs is Python package, command-line interface (CLI), and Rust crate for parsing, validating, and converting Common Query Language (CQL2).

So what does that mean?
-->

---
layout: iframe
url: https://www.ogc.org/standards/cql2/
---

<!--
We should first define what CQL2 even is.

CQL2 stands for "Common Query Language" (don't know why the "2" is in the acronymn)

An OGC standard for describing an expression used to filter a collection of data.
-->



---
layout: image-right
# Landsat 9 Image of Western Guinea-Bissau
# https://unsplash.com/photos/ZuN44o80Bn0
image: https://images.unsplash.com/photo-1722083854982-2f1516cf263c

class: image-narrow
---

# STAC Filter Extension


> This extension expands the capabilities of Item Search and the OAFeat Items resource with Common Query Language (CQL2) by providing an expressive query language to construct more complex filter predicates using operators that are similar to those provided by SQL.

-- `https://github.com/stac-api-extensions/filter`

<LogoHorNegMono position="bottom-right" />

<!--
Why is that important to us? 

We care because CQL2 is used by the STAC Filter Extension. The STAC Filter Extension is a well-supported add-on to a STAC API that enables powerful queries on STAC APIs.
-->

---
layout: image-right
# Fjords in southeastern coast of Greenland
# https://unsplash.com/photos/blue-white-and-red-abstract-painting-3O2HJPzgkQY
image: https://images.unsplash.com/photo-1579818276659-2943e3cd4b30
class: text-center
---

# `cql2-rs`

<br my-5 />

## ... so what does it do?

<LogoHorNegMono position="bottom-right" />

<!-- 

And so back to cql2-rs. What does it do?
 -->

---
layout: image-right
# Landsat 8 Image of Ayon Island
# https://unsplash.com/photos/B-bXvd0R1bM
image: https://images.unsplash.com/photo-1722083855371-0d5a25647ce6
class: image-narrow
---

# validate

```ts {monaco-run} {autorun:true}
import { Expr } from 'cql2-wasm'

const expr = 'collection = foo'
console.log(
  new Expr(expr).is_valid()
)
```

```ts {monaco-run} {autorun:true}
import { Expr } from 'cql2-wasm'

const expr = 'blah blah blah'
console.log(
  new Expr(expr).is_valid()
)
```


<LogoHorNegMono position="bottom-right" />

---
layout: image-right
# Landsat 9 Image of Prudhoe Bay, Alaska
# https://unsplash.com/photos/a-satellite-image-of-a-body-of-water-F8BGGoayfeQ
image: https://images.unsplash.com/photo-1722082839868-d900d1a07e69
class: image-narrow
---

# text <-> json

```ts {monaco-run} {autorun:true}
import { Expr } from 'cql2-wasm'

const expr = '(avg("windSpeed") < 4)'
console.log(
  new Expr(expr).to_json()
)
```

```ts {monaco-run} {autorun:true}
import { Expr } from 'cql2-wasm'

const expr = { "op": "<", "args": [ { "op": "avg", "args": [ { "property": "windSpeed" } ] }, 4 ] }
console.log(
  new Expr( JSON.stringify(expr) ).to_text()
)
```

<LogoHorNegMono position="bottom-right" />

<!-- 

CQL2 supports both a text format and a json format. one of cql2-rs' most simple abilities is to translate between these different formats

 -->

---
layout: image-right
class: image-narrow
# Landsat 9 Image of Taklimakan Desert, China
# https://unsplash.com/photos/KGzlTHjkyZM
image: https://images.unsplash.com/photo-1722080767795-af488166033d
---

# cql2 -> sql

```ts {monaco-run} {autorun:true}
import { Expr } from 'cql2-wasm'

const expr = `T_INTERSECTS(datetime, INTERVAL('2024-01-01', '2024-06-30'))`
console.log(
  new Expr(expr).to_sql()
)
```

<LogoHorNegMono position="bottom-right" />

---
layout: image-right
class: image-narrow
# Landsat 9 Image of Taklimakan Desert, China
# https://unsplash.com/photos/KGzlTHjkyZM
image: https://images.unsplash.com/photo-1722080768196-8983bbbb5c0f
---

# matches

```ts {monaco-run} {autorun:true}
import { Expr } from 'cql2-wasm'

const expr = "eo:cloud_cover <= 9"
console.log(
  new Expr(expr).matches({ properties: {"eo:cloud_cover": 10 } })
)
```

```ts {monaco-run} {autorun:true}
import { Expr } from 'cql2-wasm'

const expr = "eo:cloud_cover <= 20"
console.log(
  new Expr(expr).matches({ properties: {"eo:cloud_cover": 10} })
)
```


<LogoHorNegMono position="bottom-right" />

---
layout: image-right
class: image-narrow
# Landsat 9 image of Bangladesh Coast
image: https://images.unsplash.com/photo-1722083854850-4a24185465ac
---

# reduce

```ts {monaco-run} {autorun:true}
import { Expr } from 'cql2-wasm'

const expr = 'foo = true AND foo = true'
const reducedExpr = new Expr(expr).reduce(null)
console.log(
  reducedExpr.to_text()
)
```

<LogoHorNegMono position="bottom-right" />

---
layout: image-right
class: image-narrow
image: https://images.unsplash.com/photo-1744968777300-210d3bb46817
---

# Rust -> Python via PyO3!

````md magic-move
```rust
// Create a struct representing a Python class, wrapping our Expr struct
#[pyclass]
struct Expr(::cql2::Expr);
```

```rust
// Add methods to that Python class struct
#[pymethods]
impl Expr {
    #[new]
    fn new(cql2: Bound<'_, PyAny>) -> Result<Self> {
        if let Ok(s) = cql2.extract::<&str>() {
            s.parse().map(Expr).map_err(Error::from)
        } else {
            let expr: ::cql2::Expr = pythonize::depythonize(&cql2)?;
            Ok(Expr(expr))
        }
    }

    fn to_json<'py>(&self, py: Python<'py>) -> Result<Bound<'py, PyAny>> {
        pythonize::pythonize(py, &self.0).map_err(Error::from)
    }

    fn to_text(&self) -> Result<String> {
        self.0.to_text().map_err(Error::from)
    }

    // ...
}
```

```rust
// Add Python magic
#[pymethods]
impl Expr {
    fn __add__(&self, rhs: &Expr) -> Result<Expr> {
        Ok(Expr(self.0.clone() + rhs.0.clone()))
    }

    fn __eq__(&self, rhs: &Expr) -> bool {
        self.0 == rhs.0
    }

    fn __str__(&self) -> Result<String> {
        self.to_text()
    }

    fn __repr__(&self) -> Result<String> {
        Ok(format!("Expr({})", self.to_text()?))
    }
}
```

```rust
/// Expose as a Python module
#[pymodule]
fn cql2(py: Python<'_>, m: &Bound<'_, PyModule>) -> PyResult<()> {
    m.add_class::<Expr>()?;
    m.add("__version__", env!("CARGO_PKG_VERSION"))?;
    Ok(())
}
```
````

---
layout: iframe-right
url: https://developmentseed.org/cql2-rs/latest/playground/
---

# Rust -> JS via wasm-bindgen!


```ts {monaco-run} {autorun:true}
import { Expr } from 'cql2-wasm'

const expr = '(avg("windSpeed") < 4)'
console.log(
  new Expr(expr).to_json()
)
```

---
layout: title
# Landsat 9 image of Apostle Islands, Lake Superior
# https://unsplash.com/photos/j7HqdQqn7Jo
image: https://images.unsplash.com/photo-1722080767251-aad7fa1796d3
---

# Thank you!

<DecorativeRectangle
  width="30%"
  height="96%"
  zIndex=11
  :position="{
    bottom: '2%',
    right: '2%',
  }"
  :customStyle="{ mixBlendMode: 'multiply' }"
>
  <div w-full h-full relative flex flex-col items-start justify-between p-4 text-white text-left class="[&_a]:no-underline [&_a]:text-white [&_a:hover]:text-gray-200">
    <div mb-4 flex flex-col gap-5 items-start justify-start text-sm font-mono class="[&_a]:flex [&_a]:items-center [&_a]:gap-1">
      <Logo src="/images/logos/hor--neg-mono@2x.png" height="24px" alt="DevelopmentSeed" class="!relative !top-0 !left-0" />
      <a href="mailto:anthony@developmentseed.org" title="Email">
        <EmailIcon size="20" pr-1 />
        <span>anthony@developmentseed.org</span>
      </a>
      <a href="https://github.com/alukach" target="_blank" title="GitHub">
        <GitHubIcon size="20" pr-1 />
        <span>@alukach</span>
      </a>
      <a href="https://www.linkedin.com/in/alukach" target="_blank" title="LinkedIn">
        <LinkedInIcon size="20" pr-1 />
        <span>in/alukach</span>
      </a>
      <!-- <a href="https://developmentseed.org/careers" target="_blank" class="font-sans" text-xs text-strong text-italics>
        <span pr-1>🚀</span>
        We're hiring!
      </a> -->
      <CurrentUrlQRCode
        fullWidth
        image='/images/logos/symbol--neg-mono@2x.png'
        :dotsOptions="{ type: 'classy-rounded', color: 'white' }"
      />
    </div>
    <div opacity-70 w-100 class="text-[10px]">
      <div>Attributions:</div>
      <div>
        Slide images from <a href="https://unsplash.com/@usgs?utm_source=ds-slides&utm_medium=referral" target="_blank" class="text-white hover:text-gray-200">USGS</a> on <a href="https://unsplash.com/?utm_source=ds-slides&utm_medium=referral">Unsplash</a>
      </div>
    </div>
  </div>
</DecorativeRectangle>
