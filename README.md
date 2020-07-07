# sharepic-generator
A simple generator for social media posts. Combine image and text. Includes WYSIWYG editor

## Features
- language support
    - [x] german
    - [ ] english
- [x] wysiwyg editor (tinyMCE)
- [x] use background images from url
- [x] download image (arbitrary resolution)
- [x] resize background
- [ ] 

## Requirements
- [parcel bundler](https://parceljs.org/) (requires node and probably yarn)

## How to build
run `parcel build src/index.html` from the repositories directory. Your results will be under `dist/` and can be hosted on some webspace. Please note that if you don't want to host from a subdirectory/suburl, you should specify some [public URL](https://parceljs.org/cli.html) during build.
