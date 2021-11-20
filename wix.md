# WIX
Wix is a no-code, low code tool for webdev.

## Design
- allows you to design via drag and drop.
- add animations, customize elements, modals, forms (even reCAPTCHA elements).
- could add multiple pages and even routes.

## Data
- website data is stored in collections. Mostly to fulfill the purpose of a CMS
- site elements are connected to the collection via a virtual wix element called a dataset.

## Velo backend
- velo allows the dev to add interactivity with js. can integrate apis with velo.
- each page has its own frontend file
- dev can add backend files (stored as .jsw)
- dev can use @velo and @npm packages for development of these sites.
- several wix packages are provided like
  - wix-data
  - wix-fetch
  - wix-animation
- elements on the page can be selected using the `$w("#elementID")` construct.