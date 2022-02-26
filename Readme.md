# vue3-pagination

A vue3 component which creates a good looking UI and full Functional Pagination with a lot of customizable features.

## Installation

`npm install vue3-pagination`

## Usage

vue3-pagination is a very simple, easy to use and customizable pagination component which can create UI and provides events to handle them for the pagination usage.

### ES6

**For Local Registration**

```
import Vue3Pagination from "vue3-pagination";

export default {
    ...
    components : {
        Vue3Pagination,
        ...
    },
    ...
}
```

**For Global Registration**

Update main.js

```
import { createApp } from "vue";
import App from "./App.vue";
...
import Vue3Pagination from "vue3-pagination";

createApp(App).component("vue3-pagination", Vue3Pagination)
...
```

After importing the component, you can use it in your templates as:

```
<vue3-pagination
    :currentPage="1"
    :totalPage="50"
    @pageChange="handlePageChange"
>
</vue3-pagination>
...
</template>
<script>
...
{
    ...
    methods : {
        handlePageChange(page) {
            console.log("Intended Page :", page)
        },
    }
...
}
...
```

where currentPage is the page number of currently rendered page. And totalPage is the number of pages for pagination.

However, It won't render all pages from 1 to 50 as it has additional pageCount prop which is set to 5 by default which indicates highest number of pages options to render in component at a time.

## Preview

![Pagination Demo](./src/assets/Pagination.png?raw=true "Title")

## Props

Before defining props, Let me list the HTML Structure for Pagination Component.

```
<ul :class="paginationContainerClass">
    <li :class="paginationItemClass">
        <a :class="paginationLinkClass">#Page</a>
    </li>
    .
    .
    .
    <li :class="paginationItemClass + paginationItemActiveClass">
        <a :class="paginationLinkClass">#Page</a>
    </li>
    .
    <li :class="paginationItemClass">
        <a :class="paginationLinkClass">#Page</a>
    </li>
</ul>
```

| Property                  | Required | Type             | Default  | Decription                                              |
| ------------------------- | -------- | ---------------- | -------- | ------------------------------------------------------- |
| currentPage               | false    | Number           | 1        | currently active page number                            |
| pageCount                 | false    | Number           | 5        | maximum page count to render at a time                  |
| totalPage                 | false    | Number           | 1        | total number of pages to be rendered                    |
| height                    | false    | [String, Number] | 35px     | height of the page item in pagination                   |
| width                     | false    | [String, Number] | 35px     | width of the page item in pagination                    |
| firstTitle                | false    | String           | First    | tooltip for go to first page icon                       |
| previousTitle             | false    | String           | Previous | tooltip for go to previous page icon                    |
| nextTitle                 | false    | String           | Next     | tooltip for go to next page icon                        |
| lastTitle                 | false    | String           | Last     | tooltip for go to last page icon                        |
| paginationItemClass       | false    | String           | -        | overriding class/classes for the pagination item        |
| paginationLinkClass       | false    | String           | -        | overriding class/classes for the pagination link        |
| paginationContainerClass  | false    | String           | -        | overriding class/classes for the pagination container   |
| paginationItemActiveClass | false    | String           | -        | overriding class/classes for the active pagination item |

## Events

| Event      | Invoking Time                                 | Type     | Decription                                                       |
| ---------- | --------------------------------------------- | -------- | ---------------------------------------------------------------- |
| pageChange | When user clicks on any clickable page number | function | pass a function which contains a logic to perform on page change |

## Creator

This component has been created by [Md Dilshad Alam](https://github.com/webformulator)
